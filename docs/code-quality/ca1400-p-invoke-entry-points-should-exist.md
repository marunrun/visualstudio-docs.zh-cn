---
title: CA1400:P-Invoke 入口点应该存在
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1400
- PInvokeEntryPointsShouldExist
helpviewer_keywords:
- PInvokeEntryPointsShouldExist
- CA1400
ms.assetid: 1d64e470-7b2f-4cca-8fb0-ac92829e6332
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b292c58e666c11130fb25f67c234bfd2282fe463
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922260"
---
# <a name="ca1400-pinvoke-entry-points-should-exist"></a>CA1400:P/Invoke 入口点应该存在

|||
|-|-|
|TypeName|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|类别|Microsoft.Interoperability|
|是否重大更改|不间断|

## <a name="cause"></a>原因
公共或受保护的方法使用<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>进行标记。 未能找到非托管库，或者未能将方法与库中的函数匹配。 如果规则找不到指定的方法名称, 它将通过使用 "A" 或 "W" suffixing 方法名称来查找方法的 ANSI 或宽字符版本。 如果未找到匹配项, 则规则将尝试使用 __stdcall 名称格式 (_MyMethod@12, 其中12表示参数的长度) 查找函数。 如果未找到匹配项, 并且方法名称以 "#" 开头, 则规则会搜索函数作为序号引用而不是名称引用。

## <a name="rule-description"></a>规则说明
无编译时检查可用于确保用<xref:System.Runtime.InteropServices.DllImportAttribute>标记的方法位于引用的非托管 DLL 中。 如果库中没有具有指定名称的函数, 或者该方法的参数与函数参数不匹配, 则公共语言运行时将引发异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请更正具有<xref:System.Runtime.InteropServices.DllImportAttribute>特性的方法。 请确保非托管库存在并且与包含该方法的程序集位于同一目录中。 如果库存在并且引用正确, 请验证方法名称、返回类型和参数签名是否与库函数匹配。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
当非托管库与引用它的托管程序集位于同一目录中时, 请勿禁止显示此规则发出的警告。 如果无法定位非托管库, 则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则的类型。 Kernel32.dll 中不存在名`DoSomethingUnmanaged`为的函数。

[!code-csharp[FxCop.Interoperability.DLLExists#1](../code-quality/codesnippet/CSharp/ca1400-p-invoke-entry-points-should-exist_1.cs)]

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>