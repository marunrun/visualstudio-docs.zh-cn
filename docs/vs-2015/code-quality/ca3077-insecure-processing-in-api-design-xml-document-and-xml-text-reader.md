---
title: CA3077:不安全的 API 设计、 XML 文档和 XML 文本读取器中处理 |Microsoft Docs
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 7f33771b-f3c8-4c02-bef6-f581b623c303
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d8f1e04483c486add9940bf3a78ec4c35eb2317d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65693370"
---
# <a name="ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader"></a>CA3077:API 设计、XML 文档和 XML 文本读取器中的不安全处理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|InsecureDTDProcessingInAPIDesign|
|CheckId|CA3077|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 当设计派生自 XMLDocument 和 XMLTextReader 的 API 时，请注意 <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>。  当引用或解析外部实体源或设置 XML 中的不安全值时，使用不安全的 DTDProcessing 实例可能会导致信息泄露。

## <a name="rule-description"></a>规则说明
 XML 分析器可以通过两种方式确定文档有效性， [文档类型定义 (DTD)](https://msdn.microsoft.com/library/aa468547.aspx) 是其中一种（根据  [万维网联合会 (W3C) 可扩展标记语言 (XML) 1.0](http://www.w3.org/TR/2008/REC-xml-20081126/)的定义）。 此规则查找接受不受信任数据的某些属性和实例以提醒开发人员有关的潜在 [Information Disclosure](https://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) 威胁，该威胁可能会导致 [拒绝服务 (DoS)](https://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) 攻击。 在以下情况下触发此规则：

- <xref:System.Xml.XmlDocument> 或<xref:System.Xml.XmlTextReader>类使用默认冲突解决程序值进行 DTD 处理。

- 没有为 XmlDocument 或 XmlTextReader 派生类定义的构造函数或没有用于 <xref:System.Xml.XmlResolver>的安全值。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 捕获和处理所有 XmlTextReader 异常正确以避免路径信息泄露。

- 使用 <xref:System.Xml.XmlSecureResolver>而不是 XmlResolver 来限制 XmlTextReader 可以访问的资源。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 除非确信已知道输入是来自受信任的源，否则请勿禁止显示此警告的规则。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    class TestClass : XmlDocument
    {
        public TestClass () {} // warn
    }

    class TestClass2 : XmlTextReader
    {
        public TestClass2() // warn
        {
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    class TestClass : XmlDocument
    {
        public TestClass ()
        {
            XmlResolver = null;
        }
    }

    class TestClass2 : XmlTextReader
    {
        public TestClass2()
        {
               XmlResolver = null;
        }
    }
}
```
