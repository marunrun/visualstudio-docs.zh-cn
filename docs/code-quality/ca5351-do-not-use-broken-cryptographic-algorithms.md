---
title: CA5351 不使用损坏的加密算法
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 483f51b3-e186-4433-b48e-5ca24a9a9c94
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9af307158ecd8d5a1f93ebd1f8575cad5cf51e5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62540854"
---
# <a name="ca5351-do-not-use-broken-cryptographic-algorithms"></a>CA5351 不使用损坏的加密算法

|||
|-|-|
|TypeName|DoNotUseBrokenCryptographicAlgorithms|
|CheckId|CA5351|
|类别|Microsoft.Cryptography|
|是否重大更改|非重大更改|

> [!NOTE]
> 此警告上次更新于 2015 年 11 月。

## <a name="cause"></a>原因

哈希函数（如 <xref:System.Security.Cryptography.MD5> ）和加密算法（如 <xref:System.Security.Cryptography.DES> 和 <xref:System.Security.Cryptography.RC2> ）可能会带来重大风险，并可能通过普通的攻击技术（如暴力攻击和哈希冲突）导致暴露敏感信息。

下面的加密算法列表受到已知加密攻击。 加密哈希算法 <xref:System.Security.Cryptography.MD5> 受到哈希冲突攻击。  根据使用情况，哈希冲突可能会使依赖哈希函数这一唯一加密输出的系统受到假冒、篡改或其他类型的攻击。 加密算法 <xref:System.Security.Cryptography.DES> 和 <xref:System.Security.Cryptography.RC2> 受到加密攻击，可能会导致加密数据的意外泄露。

## <a name="rule-description"></a>规则说明

损坏的加密算法不安全，不鼓励继续使用。 尽管具体的漏洞因使用环境的不同而异，但 MD5 哈希算法仍易遭到已知的冲突攻击。  哈希算法用于确保数据完整性 （例如，文件签名或数字证书） 尤其易被攻击。  在这种情况下，攻击者可能会生成两个独立的数据块，以便在不更改哈希值或使相关数字签名无效的情况下，将良性数据替换为恶意数据。

对于加密算法：

- <xref:System.Security.Cryptography.DES> 加密使用的密钥强度较低，可能在一天内被暴力破解。

- <xref:System.Security.Cryptography.RC2> 加密容易遭受与密钥相关的攻击，攻击者可以通过这些攻击找出所有密钥值之间的数学关系。

当在源代码中找到上述任何加密函数时，将触发此规则并向用户发出警告。

## <a name="how-to-fix-violations"></a>如何解决冲突

使用更强大的加密选项：

- 对于 MD5，请使用哈希[sha-2](/windows/desktop/SecCrypto/hash-and-signature-algorithms)系列 (例如， <xref:System.Security.Cryptography.SHA512>， <xref:System.Security.Cryptography.SHA384>， <xref:System.Security.Cryptography.SHA256>)。

- 对于 DES 和 RC2，请使用 <xref:System.Security.Cryptography.Aes> 加密。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

除非经过加密专家审查，否则不要禁止显示此规则的警告。

## <a name="pseudo-code-examples"></a>伪代码示例

下面的伪代码示例演示了此规则和可能的替代检测到的模式。

### <a name="md5-hashing-violation"></a>MD5 哈希冲突

```csharp
using System.Security.Cryptography;
...
var hashAlg = MD5.Create();
```

解决方案：

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();
```

### <a name="rc2-encryption-violation"></a>RC2 加密冲突

```csharp
using System.Security.Cryptography;
...
RC2 encAlg = RC2.Create();
```

解决方案：

```csharp
using System.Security.Cryptography;
...
using (AesManaged encAlg = new AesManaged())
{
  ...
}
```

### <a name="des-encryption-violation"></a>DES 加密冲突

```csharp
using System.Security.Cryptography;
...
DES encAlg = DES.Create();
```

解决方案：

```csharp
using System.Security.Cryptography;
...
using (AesManaged encAlg = new AesManaged())
{
  ...
}
```