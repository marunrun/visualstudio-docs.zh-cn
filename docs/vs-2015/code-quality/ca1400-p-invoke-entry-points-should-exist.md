---
title: CA1400:-Invoke 入口点应该存在 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0e5696689d0aa40f4af2e11970c81b47737a3d80
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200369"
---
# <a name="ca1400-pinvoke-entry-points-should-exist"></a>CA1400:P/Invoke 入口点应该存在
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|类别|Microsoft.Interoperability|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共或受保护的方法标记为<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>。 未能找到非托管库，或者未能将方法与库中的函数匹配。 如果指定它的样子，规则找不到方法名称，它会查找 ANSI 或方法的宽字符版本后缀 A 或 W 的方法名。 如果不找到任何匹配项，则该规则将尝试使用 __stdcall 名称格式来定位函数 (_MyMethod@12，其中，12 表示参数的长度)。 如果未找到匹配，并且方法名称以 '#' 开头，该规则会搜索该函数作为引用而不是名称引用的序号。

## <a name="rule-description"></a>规则说明
 不进行编译时检查是可用于确保使用标记的方法<xref:System.Runtime.InteropServices.DllImportAttribute>位于引用的非托管 DLL。 如果没有具有指定的名称的函数是在库中，或该方法的参数不匹配函数自变量，公共语言运行时将引发异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更正的方法具有<xref:System.Runtime.InteropServices.DllImportAttribute>属性。 请确保非托管的库存在并处于与包含该方法的程序集相同的目录。 如果库已存在且正确引用，请验证方法名称、 返回类型和参数签名匹配的库函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 在引用它的托管程序集所在的目录中的非托管的库时，不要禁止显示此规则的警告。 它可以安全地禁止显示在其中的非托管的库无法找到的情况下此规则的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。 名为没有函数`DoSomethingUnmanaged`kernel32.dll 中发生。

 [!code-csharp[FxCop.Interoperability.DLLExists#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DLLExists/cs/FxCop.Interoperability.DLLExists.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>
