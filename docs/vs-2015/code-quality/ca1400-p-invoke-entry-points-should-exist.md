---
title: CA1400： P-调用入口点应该存在 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1400
- PInvokeEntryPointsShouldExist
helpviewer_keywords:
- PInvokeEntryPointsShouldExist
- CA1400
ms.assetid: 1d64e470-7b2f-4cca-8fb0-ac92829e6332
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 15b63e49f89e17db631772c48765cc610f47ed29
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548299"
---
# <a name="ca1400-pinvoke-entry-points-should-exist"></a>CA1400：P/Invoke 入口点应该存在
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|Category|Microsoft. 互操作性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 公共或受保护的方法使用进行标记 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 。 未能找到非托管库，或者未能将方法与库中的函数匹配。 如果规则找不到指定的方法名称，它将通过使用 "A" 或 "W" suffixing 方法名称来查找方法的 ANSI 或宽字符版本。 如果未找到匹配项，则规则将尝试使用 __stdcall 名称格式（ _MyMethod@12 ，其中12表示参数的长度）查找函数。 如果未找到匹配项，并且方法名称以 "#" 开头，则规则会搜索函数作为序号引用而不是名称引用。

## <a name="rule-description"></a>规则描述
 无编译时检查可用于确保用标记的方法 <xref:System.Runtime.InteropServices.DllImportAttribute> 位于引用的非托管 DLL 中。 如果库中没有具有指定名称的函数，或者该方法的参数与函数参数不匹配，则公共语言运行时将引发异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更正具有特性的方法 <xref:System.Runtime.InteropServices.DllImportAttribute> 。 请确保非托管库存在并且与包含该方法的程序集位于同一目录中。 如果库存在并且引用正确，请验证方法名称、返回类型和参数签名是否与库函数匹配。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 当非托管库与引用它的托管程序集位于同一目录中时，请勿禁止显示此规则发出的警告。 如果无法定位非托管库，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。 kernel32.dll 中不存在名为的函数 `DoSomethingUnmanaged` 。

 [!code-csharp[FxCop.Interoperability.DLLExists#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DLLExists/cs/FxCop.Interoperability.DLLExists.cs#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>
