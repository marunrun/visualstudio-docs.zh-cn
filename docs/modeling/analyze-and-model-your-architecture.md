---
title: 对体系结构进行分析和建模
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be731ea81baaaa6e9f04b7546bc26ccea0549389
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476633"
---
# <a name="analyze-and-model-your-architecture"></a>对体系结构进行分析和建模

请确保您的应用程序通过使用 Visual Studio 体系结构和建模工具来设计和建模应用程序满足架构要求。

* 通过使用 Visual Studio 来可视化代码结构、行为和关系可使你更容易理解现有程序代码。

* 对您需要为遵循体系结构依赖项的团队进行培训。

* 作为开发过程的一部分，可以跨整个应用程序生命周期创建不同详细信息级别的模型。

请参阅[方案：使用可视化和建模更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)。

## <a name="article-reference"></a>项目引用

|||
|-|-|
|**可视化代码**：<br /><br />-通过创建代码图，请参阅代码的组织和关系。 可视化程序集、命名空间、类、方法等之间的依赖关系。<br />-通过从代码创建类关系图，请参阅类结构和针对特定项目的成员。<br />-通过创建依赖项关系图验证代码来查找你的代码和它的设计之间的冲突。|- [可视化代码](../modeling/visualize-code.md)<br />- [使用类和其他类型 （类设计器）](../ide/class-designer/designing-and-viewing-classes-and-types.md)<br />- [视频：了解使用 Visual Studio 2015 代码图的代码设计](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />- [视频：验证你在真实时间中的体系结构依赖关系](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**定义体系结构**：<br /><br />-定义和强制执行你的代码通过创建依赖项关系图的组件之间的依赖关系的约束。|- [视频：验证使用 Visual Studio (通道 9) 的体系结构依赖关系](https://channel9.msdn.com/Events/Connect/2016/170)|
|**使用要求和预期设计来验证你的系统：**<br /><br />验证使用描述预期体系结构的依赖项关系图的代码依赖项和防止可能与设计发生冲突的更改。|- [视频：验证使用 Visual Studio (通道 9) 的体系结构依赖关系](https://channel9.msdn.com/Events/Connect/2016/170)|
|**自定义模型和关系图**：<br /><br />-创建你自己的域特定语言。|- [Visual Studio 域特定语言的建模 SDK](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**使用 T4 模板生成文本**：<br /><br />-使用文本块和深入了解模板的控制逻辑生成基于文本的文件。<br /> 的使用 Visual Studio 中包含 MSBuild T4 模板生成|- [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)|
|**使用 Team Foundation 版本控制共享模型、关系图和代码图**：<br /><br />-将代码图、 项目和 Team Foundation 版本控制下的依赖项关系图以便可以共享它们。| |

若要查看哪些版本的 Visual Studio 支持每个功能，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="types-of-models-and-typical-uses"></a>类型的模型和典型用法

### <a name="code-maps"></a>代码图

代码图可帮助查看代码中的组织和关系。

**典型用法：**

- 检查程序代码，以便可以更好地了解其结构及其依赖关系以及如何对其进行更新，并估计建议更改的成本。

**请参阅：**

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

### <a name="dependency-diagrams"></a>依赖项关系图

依赖项关系图，可以为一系列层或显式依赖关系的块中定义应用程序的结构。 实时验证会显示在代码中的依赖关系和依赖项关系图上所述的依赖项之间的冲突。

**典型用法：**

- 通过在应用程序生命周期中进行大量更改来稳定其结构。
- 在签入对代码的更改之前发现无意的依赖项冲突。

**请参阅：**

- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)
- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>域特定语言 (DSL)

DSL 是为特定目的而设计的一种表示法。 在 Visual Studio 中，通常表示为图形。

**典型用法：**

- 生成或配置应用程序的各部分。 若要开发表示法和工具，则需要进行工作。 其产生的结果，与 UML 自定义相比，会更好地适应你的域。
- 适用于大型项目或在某些产品系列中（其中 DSL 及其工具的开发投资会通过该产品在多个项目中的使用而回收）。

**请参阅：**

- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="see-also"></a>请参阅

- [什么是 Visual Studio 2017 中建模的新增功能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps 和应用程序生命周期管理](/azure/devops/user-guide/devops-alm-overview)
