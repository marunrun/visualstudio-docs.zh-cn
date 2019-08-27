---
title: CA2232:使用 STAThread 标记 Windows 窗体的入口点
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MarkWindowsFormsEntryPointsWithStaThread
- CA2232
helpviewer_keywords:
- CA2232
- MarkWindowsFormsEntryPointsWithStaThread
ms.assetid: a3c95130-8e7f-4419-9fcd-b67d077e8efb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: dd3f5b76015a3a54ee085b5cc2dd532920ff0795
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920178"
---
# <a name="ca2232-mark-windows-forms-entry-points-with-stathread"></a>CA2232:使用 STAThread 标记 Windows 窗体的入口点

|||
|-|-|
|TypeName|MarkWindowsFormsEntryPointsWithStaThread|
|CheckId|CA2232|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
程序集引用<xref:System.Windows.Forms>命名空间, 并且没有<xref:System.STAThreadAttribute?displayProperty=fullName>用特性标记其入口点。

## <a name="rule-description"></a>规则说明
 <xref:System.STAThreadAttribute>指示应用程序的 COM 线程模型是单线程单元。 使用 Windows 窗体的任何应用程序的入口点上必须存在此特性；如果没有此特性，则 Windows 组件可能无法正常工作。 如果该属性不存在, 则应用程序将使用多线程单元模型, 这不受 Windows 窗体支持。

> [!NOTE]
> [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]使用应用程序框架的项目不必使用 STAThread 标记**Main**方法。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]编译器会自动执行此功能。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请<xref:System.STAThreadAttribute>将特性添加到入口点。 如果该<xref:System.MTAThreadAttribute?displayProperty=fullName>属性存在, 则将其删除。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果要针对 .NET Compact Framework 进行开发, 而该属性是不必要的<xref:System.STAThreadAttribute>且不受支持, 则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
以下示例演示了的<xref:System.STAThreadAttribute>正确用法:

[!code-csharp[FxCop.Usage.StaThread#1](../code-quality/codesnippet/CSharp/ca2232-mark-windows-forms-entry-points-with-stathread_1.cs)]
[!code-vb[FxCop.Usage.StaThread#1](../code-quality/codesnippet/VisualBasic/ca2232-mark-windows-forms-entry-points-with-stathread_1.vb)]