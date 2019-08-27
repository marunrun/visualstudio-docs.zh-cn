---
title: 建模 SDK 的 API 参考
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
ms.assetid: 590c9a69-4e22-4841-bb23-f32e80ec1e76
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6a290227b120958b5bb3407393dcff33b247b20d
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68872021"
---
# <a name="api-reference-for-modeling-sdk-for-visual-studio"></a>Visual Studio 的建模 SDK 的 API 参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 可视化和建模 SDK 提供了用于构建域特定语言 (DSL) 和 UML 工具的平台。

> [!NOTE]
> 有关 UML 建模 API 的信息, 请参阅[用于 Uml 建模扩展性的 API 参考](../modeling/api-reference-for-uml-modeling-extensibility.md)。 有关文本转换的信息, 请参阅[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)。

 本部分包含具有以"Microsoft.VisualStudio.Modeling"开头的名称的命名空间的参考资料。

|命名空间|内容|
|---------------|-------------|
|<xref:Microsoft.VisualStudio.Modeling?displayProperty=fullName>|如 ModelElement，是在 DSL 中定义的所有域类的基类的类。|
|<xref:Microsoft.VisualStudio.Modeling.Design?displayProperty=fullName>|形成 DSL 定义的一部分的类。|
|<xref:Microsoft.VisualStudio.Modeling.Diagnostics?displayProperty=fullName>|模型存储查看器和性能的评定工具。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams?displayProperty=fullName>|如 ShapeElement，是在 DSL 中定义的所有形状的基类的类。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement?displayProperty=fullName>|手势和选择的方法。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition?displayProperty=fullName>|DSL 定义设计器的 API。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.Design?displayProperty=fullName>|在 DSL 定义设计器的内部类。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement?displayProperty=fullName>|允许你通过命令、手势和验证扩展 DSL 设计器的特性。|
|<xref:Microsoft.VisualStudio.Modeling.Extensibility?displayProperty=fullName>|实现 DSL 可扩展性的扩展方法的模型元素。|
|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement?displayProperty=fullName>|扩展属性|
|<xref:Microsoft.VisualStudio.Modeling.Immutability?displayProperty=fullName>|能让你的模型部分只读的。|
|[VisualStudio 集成](/previous-versions/ee904412(v=vs.140))|Modelbus API，它可以帮助您将集成不同的模型。|
|[VisualStudio (& e)](/previous-versions/ee904394(v=vs.140))|对话框中，可让用户导航到的模型和元素来创建 Modelbus 引用。|
|`Microsoft.VisualStudio.Modeling.Integration.Picker.Hosting`|选取器服务中。|
|[VisualStudio 命令行界面](/previous-versions/ee869435(v=vs.140))|Modelbus 的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]适配器框架。|
|[VisualStudio (如果选择)](/previous-versions/ee886769(v=vs.140))|选取器对话框中，可让用户导航到的模型和元素来创建 Modelbus 引用。|
|<xref:Microsoft.VisualStudio.Modeling.Shell?displayProperty=fullName>|Dsl 和[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]之间的接口。|
|<xref:Microsoft.VisualStudio.Modeling.Shell.ExtensionEnablement?displayProperty=fullName>|你可以定义快捷 （上下文） 菜单命令。|
|<xref:Microsoft.VisualStudio.Modeling.Validation?displayProperty=fullName>|你可以定义验证约束。|

## <a name="see-also"></a>请参阅

- [UML 建模扩展性的 API 参考](../modeling/api-reference-for-uml-modeling-extensibility.md)
- [自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)
