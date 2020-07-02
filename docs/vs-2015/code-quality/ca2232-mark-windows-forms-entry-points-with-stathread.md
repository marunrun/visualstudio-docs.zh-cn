---
title: CA2232：用 STAThread 标记 Windows 窗体入口点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkWindowsFormsEntryPointsWithStaThread
- CA2232
helpviewer_keywords:
- CA2232
- MarkWindowsFormsEntryPointsWithStaThread
ms.assetid: a3c95130-8e7f-4419-9fcd-b67d077e8efb
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 42bb554f8e57c036d41a89fdc2657a25ecc74e20
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540278"
---
# <a name="ca2232-mark-windows-forms-entry-points-with-stathread"></a>CA2232:使用 STAThread 标记 Windows 窗体的入口点
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|MarkWindowsFormsEntryPointsWithStaThread|
|CheckId|CA2232|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 程序集引用 <xref:System.Windows.Forms> 命名空间，并且没有用特性标记其入口点 <xref:System.STAThreadAttribute?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 <xref:System.STAThreadAttribute>指示应用程序的 COM 线程模型是单线程单元。 使用 Windows 窗体的任何应用程序的入口点上必须存在此特性；如果没有此特性，则 Windows 组件可能无法正常工作。 如果该属性不存在，则应用程序将使用多线程单元模型，这不受 Windows 窗体支持。

> [!NOTE]
> [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]使用应用程序框架的项目不必使用 STAThread 标记**Main**方法。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]编译器会自动执行此功能。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 <xref:System.STAThreadAttribute> 特性添加到入口点。 如果该 <xref:System.MTAThreadAttribute?displayProperty=fullName> 属性存在，则将其删除。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果要针对 .NET Compact Framework 进行开发，而该 <xref:System.STAThreadAttribute> 属性是不必要的且不受支持，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示正确使用 <xref:System.STAThreadAttribute> 。

 [!code-csharp[FxCop.Usage.StaThread#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.StaThread/cs/FxCop.Usage.StaThread.cs#1)]
 [!code-vb[FxCop.Usage.StaThread#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.StaThread/vb/FxCop.Usage.StaThread.vb#1)]
