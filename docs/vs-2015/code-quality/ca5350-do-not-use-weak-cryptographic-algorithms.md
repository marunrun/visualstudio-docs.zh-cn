---
title: CA5350：不要使用弱加密算法 |Microsoft Docs
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 4c51bb8a-fcfa-46aa-ab61-634be84c4a7a
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b9c2c996c383c8834e44e16f382c14b695c83f26
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669000"
---
# <a name="ca5350-do-not-use-weak-cryptographic-algorithms"></a>CA5350：请勿使用弱加密算法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotUseWeakCryptographicAlgorithms|
|CheckId|CA5350|
|类别|Microsoft.Cryptography|
|是否重大更改|非重大更改|

> [!NOTE]
> 此警告上次更新于 2015 年 11 月。

## <a name="cause"></a>原因
 <xref:System.Security.Cryptography.TripleDES> 等加密算法和 <xref:System.Security.Cryptography.SHA1> 及 <xref:System.Security.Cryptography.RIPEMD160> 等哈希算法被视为弱加密算法。

 这些加密算法不能与更现代的对应算法提供同样多的安全保证。 与更现代的哈希算法相比，加密哈希算法 <xref:System.Security.Cryptography.SHA1> 和 <xref:System.Security.Cryptography.RIPEMD160> 提供的冲突抗性较低。 与更现代的加密算法相比，加密算法 <xref:System.Security.Cryptography.TripleDES> 提供的安全位数更少。

## <a name="rule-description"></a>规则说明
 现今出于多种原因而使用弱加密算法和哈希函数，但不应将其用于保证其所保护数据的保密性。

 该规则在代码中发现 3DES、SHA1 或 RIPEMD160 算法时将触发并向用户发送警告。

## <a name="how-to-fix-violations"></a>如何解决冲突
 使用更强大的加密选项：

- 对于 TripleDES 加密，请使用 <xref:System.Security.Cryptography.Aes> 加密。

- 对于 SHA1 或 RIPEMD160 哈希函数，请从 [SHA-2](https://msdn.microsoft.com/library/windows/desktop/aa382459.aspx) 系列（例如 <xref:System.Security.Cryptography.SHA512>、 <xref:System.Security.Cryptography.SHA384>、 <xref:System.Security.Cryptography.SHA256>）中选择使用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 当数据所需的保护级别不需要安全保证时，请禁止显示此规则的警告。

## <a name="pseudo-code-example"></a>伪代码示例
 到本文撰写时为止，下面的伪代码示例说明了此规则检测到的模式。

### <a name="sha-1-hashing-violation"></a>SHA-1 哈希冲突

```
using System.Security.Cryptography;
...
var hashAlg = SHA1.Create();

```

### <a name="solution"></a>解决方案

```
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();

```

### <a name="ripemd160-br-br-hashing-violation"></a>RIPEMD160 <br /><br />哈希冲突

```
using System.Security.Cryptography;
...
var hashAlg = RIPEMD160Managed.Create();

```

### <a name="solution"></a>解决方案

```
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();

```

### <a name="tripledes-encryption-violation"></a>TripleDES 加密冲突

```
using System.Security.Cryptography;
...
using (TripleDES encAlg = TripleDES.Create())
{
  ...
}
```

### <a name="solution"></a>解决方案

```
using System.Security.Cryptography;
...
using (AesManaged encAlg = new AesManaged())
{
  ...
}
```