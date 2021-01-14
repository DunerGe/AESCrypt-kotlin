# AESCrypt-kotlin
kotlin语言的AES加密解密
## AES与DES的区别
DES明文长度最低为8位   
AES明文长度最低为16位   
DES加密时前7位参与加密，最后一位作为校验码不参与加密   
AES加密时16位全部参与加密
## 下面是AES加密解密的代码
```
object AESCrypt{

    //AES加密
    fun encrypt(input:String,password:String): String{

        //初始化cipher对象
        val cipher = Cipher.getInstance("AES")
        // 生成密钥
        val keySpec:SecretKeySpec? = SecretKeySpec(password.toByteArray(),"AES")
        cipher.init(Cipher.ENCRYPT_MODE,keySpec)
        //加密解密
        val encrypt = cipher.doFinal(input.toByteArray())
        val result = Base64.getEncoder().encode(encrypt)

        return String(result)
    }

    //AES解密
    fun decrypt(input: String,password: String): String{

        //初始化cipher对象
        val cipher = Cipher.getInstance("AES")
        // 生成密钥
        val keySpec:SecretKeySpec? = SecretKeySpec(password.toByteArray(),"AES")
        cipher.init(Cipher.DECRYPT_MODE,keySpec)
        //加密解密
        val encrypt = cipher.doFinal(Base64.getDecoder().decode(input.toByteArray()))
        //AES解密不需要用Base64解码
        val result = String(encrypt)

        return result
    }

}

fun main(args: Array<String>) {

    //一个英文字节占8bit,AES需要128bit，也就是需要16位长度
    val password = "1234567887654321"//密钥
    val input = "AES加密解密测试"

    val encrypt = AESCrypt.encrypt(input, password)
    val decrypt = AESCrypt.decrypt(encrypt, password)

    println("AES加密结果:"+encrypt)
    println("AES解密结果:"+decrypt)

}
```
