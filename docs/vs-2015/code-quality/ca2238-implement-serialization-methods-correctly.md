---
title: CA2238:正确实现序列化方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
helpviewer_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
ms.assetid: 00882cf9-e10d-4d40-9126-3e6753e3c934
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cff617adf2b31ef773de3bc41db7245346795bee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142374"
---
# <a name="ca2238-implement-serialization-methods-correctly"></a>CA2238:正确实现序列化方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[CA2238:正确实现序列化方法](https://docs.microsoft.com/visualstudio/code-quality/ca2238-implement-serialization-methods-correctly)。  
  
|||  
|-|-|  
|TypeName|ImplementSerializationMethodsCorrectly|  
|CheckId|CA2238|  
|类别|Microsoft.Usage|  
|是否重大更改|是-如果方法为程序集外部可见。<br /><br /> 无间断-如果此方法不是程序集外部可见。|  
  
## <a name="cause"></a>原因  
 处理序列化事件的方法的签名、返回类型或可见性不正确。  
  
## <a name="rule-description"></a>规则说明  
 一种方法是通过应用以下序列化事件属性之一指定序列化事件处理程序：  
  
- <xref:System.Runtime.Serialization.OnSerializingAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnSerializedAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnDeserializingAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnDeserializedAttribute?displayProperty=fullName>  
  
  序列化事件处理程序采用一个参数的类型<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>，则返回`void`，并且具有`private`可见性。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 若要修复此规则的冲突，请更正签名、 返回类型或序列化事件处理程序的可见性。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 不禁止显示此规则发出的警告。  
  
## <a name="example"></a>示例  
 下面的示例演示正确声明的序列化事件处理程序。  
  
 [!code-csharp[FxCop.Usage.SerializationEventHandlers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.SerializationEventHandlers/cs/FxCop.Usage.SerializationEventHandlers.cs#1)]
 [!code-vb[FxCop.Usage.SerializationEventHandlers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.SerializationEventHandlers/vb/FxCop.Usage.SerializationEventHandlers.vb#1)]  
  
## <a name="related-rules"></a>相关的规则  
 [CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)  
  
 [CA2240:正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)  
  
 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)  
  
 [CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)  
  
 [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)  
  
 [CA2239:提供反序列化方法为可选字段](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)  
  
 [CA2120:安全的序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
