---
layout: post
title: Android keystore
categories: Android
---

# **Android Keystore Service**

Android Keystore 시스템을 사용하면 암호화 키를 "컨테이너"에 저장하여 기기에서 추출하기 어렵게 할 수 있습니다. 키 저장소에 키가 저장되면, 키 자료는 내보낼 수 없는 상태로 유지하면서 키를 암호화 작업에 사용할 수 있습니다. 이 시스템에서는 키 사용 시기와 사용 방법을 제한하는 기능도 제공합니다. 예를 들어 키 사용을 위해 사용자 인증을 요구하거나, 특정 암호화 모드에서만 키를 사용하도록 제한할 수 있습니다.

→ 여기서 '컨테이너'는 시스템만 접근 가능한 영역이다.

### 추출 차단

Android Keystore 키의 키 자료 추출을 차단하기 위해 두 가지 보안 조치가 사용됩니다.

- 키 자료는 애플리케이션 프로세스에 포함되지 않습니다. 애플리케이션에서 Android Keystore 키를 사용하여 암호화 작업을 수행하는 경우, 백그라운드 작업을 통해 서명하거나 확인할 일반 텍스트, 암호 텍스트 및 메시지가 암호화 작업을 수행하는 시스템 프로세스로 공급됩니다. 앱 프로세스가 손상된 경우 공격자가 앱 키를 사용할 수 있지만 Android 기기 외부에서 사용하기 위해 키 자료를 추출할 수는 없습니다.
- 키 자료를 Android 기기의 보안 하드웨어(예: TEE(신뢰할 수 있는 실행 환경), SE(보안 요소))에 바인딩할 수 있습니다. 이 기능을 키에 사용하면, 키 자료가 보안 하드웨어 외부에 노출되지 않습니다. Android OS가 손상되거나 공격자가 기기의 내부 저장소를 읽을 수 있는 경우 Android 기기에 있는 모든 앱의 Android Keystore 키를 사용할 수 있지만 기기에서 키를 추출할 수는 없습니다. 이 기능은 기기의 보안 하드웨어에서 키 사용이 승인된 키 알고리즘, 차단 모드, 패딩 스키마, 다이제스트 등의 특정한 조합을 지원하는 경우에만 사용할 수 있습니다. 키에 기능을 사용할 수 있는지 확인하려면 키에 대한 **`[KeyInfo](https://developer.android.com/reference/android/security/keystore/KeyInfo.html)`**를 가져와 **`[KeyInfo.isInsideSecurityHardware()](https://developer.android.com/reference/android/security/keystore/KeyInfo.html#isInsideSecureHardware())`**의 반환 값을 검사합니다.

“Inside Android Security” 의 저자 Nicolay Elenkov 에 의하면 Android M 이전의 Software-backed KeyStore 는 root 된 기기에서 유출 가능하다고 합니다.
즉, (Android KeyStore)를 쓰더라도 Android M 이전의 기기에서는 우리 앱의 데이터가 100% 안전하다는 장담을 할 수는 없습니다.

KeyInfo API 로 키가 하드웨어로 안전하게 보호되고 있는지를 확인하는 방법

    val privKey = (keyEntry as KeyStore.PrivateKeyEntry).privateKey
    val factory = KeyFactory.getInstance(privKey.getAlgorithm(), "AndroidKeyStore")
    val keyInfo: KeyInfo
    try {
        keyInfo = factory.getKeySpec(privKey, KeyInfo::class.java)
        println("HARDWARE-BACKED KEY???? " + keyInfo.isInsideSecureHardware)
    } catch (e: InvalidKeySpecException) {
        // Not an Android KeyStore key.
        e.printStackTrace()
    }

## **지원되는 알고리즘**

- `[Cipher](https://developer.android.com/training/articles/keystore?hl=ko#SupportedCiphers)`
- `[KeyGenerator](https://developer.android.com/training/articles/keystore?hl=ko#SupportedKeyGenerators)`
- `[KeyFactory](https://developer.android.com/training/articles/keystore?hl=ko#SupportedKeyFactories)`
- `[KeyPairGenerator](https://developer.android.com/training/articles/keystore?hl=ko#SupportedKeyPairGenerators)`
- `[Mac](https://developer.android.com/training/articles/keystore?hl=ko#SupportedMacs)`
- `[Signature](https://developer.android.com/training/articles/keystore?hl=ko#SupportedSignatures)`
- `[SecretKeyFactory](https://developer.android.com/training/articles/keystore?hl=ko#SupportedSecretKeyFactories)`

---

## 새 비공개 키 생성

    		/*
         * Generate a new EC key pair entry in the Android Keystore by
         * using the KeyPairGenerator API. The private key can only be
         * used for signing or verification and only with SHA-256 or
         * SHA-512 as the message digest.
         */
        val kpg: KeyPairGenerator = KeyPairGenerator.getInstance(
                KeyProperties.KEY_ALGORITHM_EC,
                "AndroidKeyStore"
        )
        val parameterSpec: KeyGenParameterSpec = KeyGenParameterSpec.Builder(
                alias,
                KeyProperties.PURPOSE_SIGN or KeyProperties.PURPOSE_VERIFY
        ).run {
            setDigests(KeyProperties.DIGEST_SHA256, KeyProperties.DIGEST_SHA512)
            build()
        }

        kpg.initialize(parameterSpec)

        val kp = kpg.generateKeyPair()

## 데이터 서명 및 확인

    		/*
         * Use a PrivateKey in the KeyStore to create a signature over
         * some data.
         */
        val ks: KeyStore = KeyStore.getInstance("AndroidKeyStore").apply {
            load(null)
        }
        val entry: KeyStore.Entry = ks.getEntry(alias, null)
        if (entry !is KeyStore.PrivateKeyEntry) {
            Log.w(TAG, "Not an instance of a PrivateKeyEntry")
            return null
        }
        val signature: ByteArray = Signature.getInstance("SHA256withECDSA").run {
            initSign(entry.privateKey)
            update(data)
            sign()
        }

    		/*
         * Verify a signature previously made by a PrivateKey in our
         * KeyStore. This uses the X.509 certificate attached to our
         * private key in the KeyStore to validate a previously
         * generated signature.
         */
        val ks = KeyStore.getInstance("AndroidKeyStore").apply {
            load(null)
        }
        val entry = ks.getEntry(alias, null) as? KeyStore.PrivateKeyEntry
        if (entry == null) {
            Log.w(TAG, "Not an instance of a PrivateKeyEntry")
            return false
        }
        val valid: Boolean = Signature.getInstance("SHA256withECDSA").run {
            initVerify(entry.certificate)
            update(data)
            verify(signature)
        }