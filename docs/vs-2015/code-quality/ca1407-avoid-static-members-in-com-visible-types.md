---
title: CA1407:避免在 COM 可见类型中的静态成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
helpviewer_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
ms.assetid: bebd0776-ad04-453c-bca8-8c124c2d7840
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 93c56c17998bbe672ed5816fc950eec5cc56b1c3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705736"
---
# <a name="ca1407-avoid-static-members-in-com-visible-types"></a>CA1407:避免在 COM 可见类型中使用静态成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidStaticMembersInComVisibleTypes|
|CheckId|CA1407|
|类别|Microsoft.Interoperability|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 专门标记为可见组件对象模型 (COM) 到某个类型包含`public``static`方法。

## <a name="rule-description"></a>规则说明
 COM 不支持`static`方法。

 此规则将忽略属性和事件访问器中，运算符重载方法或通过使用标记的方法<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>属性或<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>属性。

 默认情况下，以下是对 COM 可见： 程序集、 公共类型、 公共类型中的公共实例成员和公共值类型的所有成员。

 此规则发生程序集级别<xref:System.Runtime.InteropServices.ComVisibleAttribute>必须设置为`false`和类-<xref:System.Runtime.InteropServices.ComVisibleAttribute>必须设置为`true`，如下面的代码所示。

```csharp
using System;
using System.Runtime.InteropServices;

[assembly: ComVisible(false)]
namespace Samples
{
    [ComVisible(true)]
    public class MyClass
    {
        public static void DoSomething()
        {
        }
    }
}
```

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改设计以使用提供的相同功能与实例方法`static`方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 则可以安全地禁止显示此规则的警告，如果 COM 客户端不需要对提供的功能的访问`static`方法。

## <a name="example-violation"></a>冲突的示例

### <a name="description"></a>描述
 下面的示例演示`static`违反此规则的方法。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComVisibleStaticMembersViolation/cs/FxCop.Interoperability.ComVisibleStaticMembersViolation.cs#1)]

### <a name="comments"></a>注释
 在此示例中， **Book.FromPages**方法不能从 COM 调用

## <a name="example-fix"></a>解决冲突的示例

### <a name="description"></a>描述
 若要在前面的示例中解决冲突，可以将方法更改为实例方法，但是，在这种情况不难理解。 更好的解决方案是显式应用`ComVisible(false)`给方法，以将其清除给其他开发人员，该方法不能看到从 com。

 下面的示例应用<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>方法。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComVisibleStaticMembersFixed/cs/FxCop.Interoperability.ComVisibleStaticMembersFixed.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

 [CA1406:避免对 Visual Basic 6 客户端的 Int64 参数](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)

 [CA1413:避免在 COM 可见值类型中的非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

## <a name="see-also"></a>请参阅
 [与非托管代码交互操作](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
