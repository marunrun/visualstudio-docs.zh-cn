---
title: 对体系结构进行分析和建模
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- diagrams - modeling
- architecture
- code visualization
- application design
- code exploration
- modeling
- application architecture
- architecture [Visual Studio ALM], modeling
- application modeling
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1db28867ea47752aa74b7898c44e797c0704594
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544217"
---
# <a name="analyze-and-model-your-architecture"></a>对体系结构进行分析和建模

通过使用 Visual Studio 体系结构和建模工具对应用进行设计和建模，确保应用满足体系结构要求。

* 通过使用 Visual Studio 来可视化代码结构、行为和关系可使你更容易理解现有程序代码。

* 让团队了解尊重体系结构依赖项的必要性。

* 作为开发过程的一部分，可以跨整个应用程序生命周期创建不同详细信息级别的模型。

请参阅[场景：通过可视化和建模来更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)。

## <a name="article-reference"></a>文章参考

|方案|项目|
|-|-|
|**可视化代码**：<br /><br />- 通过创建代码图查看代码的组织和关系。 可视化程序集、命名空间、类、方法等之间的依赖关系。<br />- 通过从代码创建类图来查看特定项目的类结构和成员。<br />- 通过创建依赖项关系图以验证代码来查找代码及其设计之间的冲突。|- [可视化代码](../modeling/visualize-code.md)<br />- [使用类和其他类型（类设计器）](../ide/class-designer/designing-and-viewing-classes-and-types.md)<br />- [视频：通过 Visual Studio 2015 代码图从代码中了解设计](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />- [视频：实时验证你的体系结构依赖项](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**定义体系结构**：<br /><br />- 通过创建依赖项关系图定义并实施对代码组件之间依赖项的约束。|- [视频：使用 Visual Studio 验证体系结构依赖项（第 9 频道）](https://channel9.msdn.com/Events/Connect/2016/170)|
|**使用要求和预期设计来验证你的系统：**<br /><br />- 利用描述预期体系结构的依赖项关系图来验证代码依赖项，并防止发生与设计产生冲突的更改。|- [视频：使用 Visual Studio 验证体系结构依赖项（第 9 频道）](https://channel9.msdn.com/Events/Connect/2016/170)|
|**自定义模型和关系图**：<br /><br />- 创建自己的域特定语言。|- [Visual Studio 的建模 SDK - 域特定语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**使用 T4 模板生成文本**：<br /><br />- 在模板内使用文本块和控制逻辑来生成基于文本的文件。<br /> - 使用 Visual Studio 中包含的 MSBuild 生成 T4 模板|- [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)|
|**使用 Team Foundation 版本控制共享模型、关系图和代码图**：<br /><br />- 将代码图、项目和依赖项关系图置于 Team Foundation 版本控制下，以便进行共享。| |

要查看支持每个功能的 Visual Studio 版本，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="types-of-models-and-typical-uses"></a>模型类型和典型用法

### <a name="code-maps"></a>代码图

代码图可帮助查看代码中的组织和关系。

**典型用法：**

- 检查程序代码，以便可以更好地了解其结构及其依赖关系以及如何对其进行更新，并估计建议更改的成本。

**请参阅：**

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

### <a name="dependency-diagrams"></a>依赖项关系图

依赖项关系图可将应用程序的结构定义为一组带有显式依赖项的层或块。 实时验证可显示代码中依赖项与依赖项关系图中所述依赖项之间的冲突。

**典型用法：**

- 通过在应用程序生命周期中进行大量更改来稳定其结构。
- 在签入对代码的更改之前发现无意的依赖项冲突。

**请参阅：**

- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)
- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>域特定语言 (DSL)

DSL 是为特定目的而设计的一种表示法。 在 Visual Studio 中，通常为图形。

**典型用法：**

- 生成或配置应用程序的各部分。 若要开发表示法和工具，则需要进行工作。 其产生的结果，与 UML 自定义相比，会更好地适应你的域。
- 适用于大型项目或在某些产品系列中（其中 DSL 及其工具的开发投资会通过该产品在多个项目中的使用而回收）。

**请参阅：**

- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="see-also"></a>另请参阅

- [Visual Studio 2017 中建模的新增功能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps 和应用程序生命周期管理](/azure/devops/user-guide/devops-alm-overview)
