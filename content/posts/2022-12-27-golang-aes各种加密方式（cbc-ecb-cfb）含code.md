---
title: '[Golang] aes各种加密方式（CBC/ECB/CFB）含Code'
author: Bocky
type: post
date: 2022-12-27T10:12:09+00:00
url: /2022/12/27/golang-aes各种加密方式（cbc-ecb-cfb）含code/
categories:
  - golang

---
<ul class="wp-block-list">
  <li>
    Code
  </li>
  <li>
    輸出結果
  </li>
  <li>
    線上驗證(網站)
  </li>
</ul>

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "bytes"
    "crypto/aes"
    "crypto/cipher"
    "crypto/rand"
    "encoding/base64"
    "encoding/hex"
    "io"
    "log"
)

func main() {
    origData := []byte("Hello World") // 待加密數據(明文)
    key := []byte("ABCDEFGHIJKLMNOP") // 密鑰，長度必為16
    log.Println("原文：", string(origData))

    log.Println("------------------ CBC模式 --------------------")
    encrypted := AesEncryptCBC(origData, key)
    log.Println("密文(hex)：", hex.EncodeToString(encrypted))
    log.Println("密文(base64)：", base64.StdEncoding.EncodeToString(encrypted))
    decrypted := AesDecryptCBC(encrypted, key)
    log.Println("解密结果：", string(decrypted))

    log.Println("------------------ ECB模式 --------------------")
    encrypted = AesEncryptECB(origData, key)
    log.Println("密文(hex)：", hex.EncodeToString(encrypted))
    log.Println("密文(base64)：", base64.StdEncoding.EncodeToString(encrypted))
    decrypted = AesDecryptECB(encrypted, key)
    log.Println("解密结果：", string(decrypted))

    log.Println("------------------ CFB模式 --------------------")
    encrypted = AesEncryptCFB(origData, key)
    log.Println("密文(hex)：", hex.EncodeToString(encrypted))
    log.Println("密文(base64)：", base64.StdEncoding.EncodeToString(encrypted))
    decrypted = AesDecryptCFB(encrypted, key)
    log.Println("解密结果：", string(decrypted))
}

// =================== CBC ======================
func AesEncryptCBC(origData []byte, key []byte) (encrypted []byte) {
    // 分组秘钥
    // NewCipher该函数限制了输入k的长度必须为16, 24或者32
    block, _ := aes.NewCipher(key)
    blockSize := block.BlockSize()                              // 获取秘钥块的长度
    origData = pkcs5Padding(origData, blockSize)                // 补全码
    blockMode := cipher.NewCBCEncrypter(block, key[:blockSize]) // 加密模式
    encrypted = make([]byte, len(origData))                     // 创建数组
    blockMode.CryptBlocks(encrypted, origData)                  // 加密
    return encrypted
}
func AesDecryptCBC(encrypted []byte, key []byte) (decrypted []byte) {
    block, _ := aes.NewCipher(key)                              // 分组秘钥
    blockSize := block.BlockSize()                              // 获取秘钥块的长度
    blockMode := cipher.NewCBCDecrypter(block, key[:blockSize]) // 加密模式
    decrypted = make([]byte, len(encrypted))                    // 创建数组
    blockMode.CryptBlocks(decrypted, encrypted)                 // 解密
    decrypted = pkcs5UnPadding(decrypted)                       // 去除补全码
    return decrypted
}
func pkcs5Padding(ciphertext []byte, blockSize int) []byte {
    padding := blockSize - len(ciphertext)%blockSize
    padtext := bytes.Repeat([]byte{byte(padding)}, padding)
    return append(ciphertext, padtext...)
}
func pkcs5UnPadding(origData []byte) []byte {
    length := len(origData)
    unpadding := int(origData[length-1])
    return origData[:(length - unpadding)]
}

// =================== ECB ======================
func AesEncryptECB(origData []byte, key []byte) (encrypted []byte) {
    cipher, _ := aes.NewCipher(generateKey(key))
    length := (len(origData) + aes.BlockSize) / aes.BlockSize
    plain := make([]byte, length*aes.BlockSize)
    copy(plain, origData)
    pad := byte(len(plain) - len(origData))
    for i := len(origData); i &lt; len(plain); i++ {
        plain[i] = pad
    }
    encrypted = make([]byte, len(plain))
    // 分组分块加密
    for bs, be := 0, cipher.BlockSize(); bs &lt;= len(origData); bs, be = bs+cipher.BlockSize(), be+cipher.BlockSize() {
        cipher.Encrypt(encrypted[bs:be], plain[bs:be])
    }

    return encrypted
}
func AesDecryptECB(encrypted []byte, key []byte) (decrypted []byte) {
    cipher, _ := aes.NewCipher(generateKey(key))
    decrypted = make([]byte, len(encrypted))
    //
    for bs, be := 0, cipher.BlockSize(); bs &lt; len(encrypted); bs, be = bs+cipher.BlockSize(), be+cipher.BlockSize() {
        cipher.Decrypt(decrypted[bs:be], encrypted[bs:be])
    }

    trim := 0
    if len(decrypted) &gt; 0 {
        trim = len(decrypted) - int(decrypted[len(decrypted)-1])
    }

    return decrypted[:trim]
}
func generateKey(key []byte) (genKey []byte) {
    genKey = make([]byte, 16)
    copy(genKey, key)
    for i := 16; i &lt; len(key); {
        for j := 0; j &lt; 16 && i &lt; len(key); j, i = j+1, i+1 {
            genKey[j] ^= key[i]
        }
    }
    return genKey
}

// =================== CFB ======================
func AesEncryptCFB(origData []byte, key []byte) (encrypted []byte) {
    block, err := aes.NewCipher(key)
    if err != nil {
        panic(err)
    }
    encrypted = make([]byte, aes.BlockSize+len(origData))
    iv := encrypted[:aes.BlockSize]
    if _, err := io.ReadFull(rand.Reader, iv); err != nil {
        panic(err)
    }
    stream := cipher.NewCFBEncrypter(block, iv)
    stream.XORKeyStream(encrypted[aes.BlockSize:], origData)
    return encrypted
}
func AesDecryptCFB(encrypted []byte, key []byte) (decrypted []byte) {
    block, _ := aes.NewCipher(key)
    if len(encrypted) &lt; aes.BlockSize {
        panic("ciphertext too short")
    }
    iv := encrypted[:aes.BlockSize]
    encrypted = encrypted[aes.BlockSize:]

    stream := cipher.NewCFBDecrypter(block, iv)
    stream.XORKeyStream(encrypted, encrypted)
    return encrypted
}</code></pre>

執行結果

<pre class="wp-block-code"><code lang="bash" class="language-bash">2022/12/27 18:03:51 原文： {"http_method": "POST", "http_service": "openapi", "http_uri": "/app/openapi/loginweb", "uri_params": {}, "body": {"app_id": "bens", "app_userid": "101a"}}
2022/12/27 18:03:51 ------------------ CBC模式 --------------------
2022/12/27 18:03:51 密文(hex)： 15cc9814d9c06fd3816ba2a4f842f6124a9dfd653c6ceb427377484541e680fe7c040613389f2233f0c505968d4c791cd29ef6c2c189e4f8b60543459bf31c2bebb3b3cb2e6341ffa0d0c44f3c29e04f7f5bd367472a5a1d9c78014b44e2584cf058f2abbc31913d46acc451d3459e13e021b4cf9df0bb5eb5d9982cca8a4897f99f18b9e3c4c355584888ebd1270a3368e908b2c15c1ba4095aa07d6cd59038
2022/12/27 18:03:51 密文(base64)： FcyYFNnAb9OBa6Kk+EL2Ekqd/WU8bOtCc3dIRUHmgP58BAYTOJ8iM/DFBZaNTHkc0p72wsGJ5Pi2BUNFm/McK+uzs8suY0H/oNDETzwp4E9/W9NnRypaHZx4AUtE4lhM8Fjyq7wxkT1GrMRR00WeE+AhtM+d8LtetdmYLMqKSJf5nxi548TDVVhIiOvRJwozaOkIssFcG6QJWqB9bNWQOA==
2022/12/27 18:03:51 解密结果： {"http_method": "POST", "http_service": "openapi", "http_uri": "/app/openapi/loginweb", "uri_params": {}, "body": {"app_id": "bens", "app_userid": "101a"}}
2022/12/27 18:03:51 ------------------ ECB模式 --------------------
2022/12/27 18:03:51 密文(hex)： 860ca9b68b3684b287af3375bad0c97377acef832b6693c2d97c74c2c563f2c498b645673d4724d3c5a41e3fde6741b5d176c17b1c94b36283b7f9c6f860c487ea7b03124c2418bb73607fe684bf93c2f6890d0e195b3316140f6595c02403b47b15f4c0a58ad794ad6f98a626a0e0df4bc3fc72249ed196c663a9b06545ba71d25ee921fbf01f8e924e110f6aabea60d256a104e57174ff3fd725a6aeb57638
2022/12/27 18:03:51 密文(base64)： hgyptos2hLKHrzN1utDJc3es74MrZpPC2Xx0wsVj8sSYtkVnPUck08WkHj/eZ0G10XbBexyUs2KDt/nG+GDEh+p7AxJMJBi7c2B/5oS/k8L2iQ0OGVszFhQPZZXAJAO0exX0wKWK15Stb5imJqDg30vD/HIkntGWxmOpsGVFunHSXukh+/AfjpJOEQ9qq+pg0lahBOVxdP8/1yWmrrV2OA==
2022/12/27 18:03:51 解密结果： {"http_method": "POST", "http_service": "openapi", "http_uri": "/app/openapi/loginweb", "uri_params": {}, "body": {"app_id": "bens", "app_userid": "101a"}}
2022/12/27 18:03:51 ------------------ CFB模式 --------------------
2022/12/27 18:03:51 密文(hex)： b326c923ef88752f4f604b41722fd1b3a0dced22a81b206237ff3055d5ebebca0456b6bdcaae9816e29247822ec42dbdaea560fe5d5643f40f0f4a55d5528f97c5bd59e55b0881345bf60f17a2da37c0d7d63dea5da337491314155480c045d448cf66089a506ade54b0e0ac34fc0136de3230432c1a8e159a1b150802147f225d9f8aebb7b67e45959c2b018240f5d121b7d619686630e152d83ab20a7847cf81811bc0183d574acb496a
2022/12/27 18:03:51 密文(base64)： sybJI++IdS9PYEtBci/Rs6Dc7SKoGyBiN/8wVdXr68oEVra9yq6YFuKSR4IuxC29rqVg/l1WQ/QPD0pV1VKPl8W9WeVbCIE0W/YPF6LaN8DX1j3qXaM3SRMUFVSAwEXUSM9mCJpQat5UsOCsNPwBNt4yMEMsGo4VmhsVCAIUfyJdn4rrt7Z+RZWcKwGCQPXRIbfWGWhmMOFS2DqyCnhHz4GBG8AYPVdKy0lq
2022/12/27 18:03:51 解密结果： {"http_method": "POST", "http_service": "openapi", "http_uri": "/app/openapi/loginweb", "uri_params": {}, "body": {"app_id": "bens", "app_userid": "101a"}}</code></pre>

驗證網站:  
[AES在線加密解密工具][1]

 [1]: https://totools.site/AES