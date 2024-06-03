# RSA-шифрование

```C#
using System.Security.Cryptography;
using System.Text;

var rsa = new RSACryptoServiceProvider();

var privateKey = rsa.ToXmlString(true);
var publicKey = rsa.ToXmlString(false);

Console.WriteLine("PRIVATE:");
Console.WriteLine(privateKey);
Console.WriteLine("PUBLIC:");
Console.WriteLine(publicKey);

// Шифрование
rsa.FromXmlString(publicKey);
var cryptoResult = Convert.ToBase64String(
    rsa.Encrypt(new UnicodeEncoding().GetBytes("HELLOW WORLD"), false).ToArray()
);

Console.WriteLine("CRYPTO:");
Console.WriteLine(cryptoResult);

// Дешифровка
rsa.FromXmlString(privateKey);
var decryptedByte = rsa.Decrypt(Convert.FromBase64String(cryptoResult), false);
var decryptResult = new UnicodeEncoding().GetString(decryptedByte);
Console.WriteLine("DECRYPT:");
Console.WriteLine(decryptResult);
```