---
title: 进行分析和建模您的体系结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, exploring code
- Visual Studio Ultimate, visualizing code
- diagrams - modeling
- Visual Studio ALM, modeling
- application, design
- architecture
- code visualization
- application design
- applications, architecture
- code exploration
- Visual Studio ALM, exploring code
- modeling
- application architecture
- application, modeling
- applications, modeling
- architecture [Visual Studio ALM], modeling
- application modeling
- Visual Studio Ultimate, modeling
- architecture [Visual Studio Ultimate], modeling
- application, architecture
- Visual Studio ALM, visualizing code
- applications, designing
ms.assetid: c9f04cfa-72bd-419d-a952-616eed01472e
caps.latest.revision: 129
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 59cb744b64137a3ccf34e87d89abcba22e2afc9b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65680996"
---
# <a name="analyze-and-model-your-architecture"></a>对体系结构进行分析和建模
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用 Visual Studio 体系结构和建模工具对应用进行设计和建模确保应用满足用户要求。 通过使用 Visual Studio 来可视化代码结构、行为和关系可使你更容易理解现有程序代码。  
  
 作为开发过程的一部分，可以跨整个应用程序生命周期创建不同详细信息级别的模型。 可通过将模型元素链接到 Team Foundation Server 工作项和开发计划来跟踪要求、任务、测试用例、Bug 和其他与模型关联的工作。 请参阅[方案：使用可视化和建模更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)。  
  
 若要查看支持每个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)  
  
## <a name="to"></a>若要  
  
|||  
|-|-|  
|**可视化代码**：<br /><br /> -通过创建代码图，请参阅代码的组织和关系。 可视化程序集、命名空间、类、方法等之间的依赖关系。<br />-通过从代码创建类关系图，请参阅类结构和针对特定项目的成员。<br />-通过创建层关系图验证代码来查找你的代码和它的设计之间的冲突。<br /><br /> **说明**：在此版本的 Visual Studio 中，术语*代码图*用来代替*依赖项关系图*。 术语 *关系图* 在独立使用时，一般指定向关系图或 DGML 关系图（或文档）。 代码图是 DGML 关系图的专用类型。|-   [可视化代码](../modeling/visualize-code.md)<br />-   [使用类和其他类型 （类设计器）](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [视频：了解代码依赖项通过可视化 (通道 9)](http://go.microsoft.com/fwlink/?LinkID=252065)<br />-   [视频：可视化 (通道 9) 将更改的影响](http://go.microsoft.com/fwlink/?LinkID=252068)|  
|**描述和沟通用户需求**：<br /><br /> -阐明用户情景、 业务规则和其他要求，帮助通过绘制 UML 关系图，如用例、 活动和类关系图来确保其一致性。|-   [为您的应用程序创建模型](../modeling/create-models-for-your-app.md)<br />-   [建立用户需求模型](../modeling/model-user-requirements.md)<br />-   [视频：通过建模 (通道 9) 改进体系结构](http://go.microsoft.com/fwlink/?LinkID=252078)|  
|**定义体系结构**：<br /><br /> -模型对软件系统和设计模式进行大规模结构通过绘制 UML 组件、 类和序列图。<br />-定义和强制执行你的代码通过创建层关系图的组件之间的依赖关系的约束。|-   [为您的应用程序创建模型](../modeling/create-models-for-your-app.md)<br />-   [应用程序的体系结构建模](../modeling/model-your-app-s-architecture.md)<br />-   [视频：通过建模 (通道 9) 改进体系结构](http://go.microsoft.com/fwlink/?LinkID=252078)<br />-   [视频：使用层关系图设计和验证体系结构 (通道 9)](http://go.microsoft.com/fwlink/?LinkID=252073)|  
|**使用要求和预期设计来验证你的系统：**<br /><br /> -定义验收测试或系统测试基于要求模型。 这将在测试和用户要求之间建立一种稳固的关系，并有助于在要求更改时更轻松地更新系统。<br />验证代码依赖项的描述预期体系结构层关系图和防止可能与设计发生冲突的更改。|-   [在开发过程中验证您的系统](../modeling/validate-your-system-during-development.md)<br />-   [视频：使用层关系图设计和验证体系结构 (通道 9)](http://go.microsoft.com/fwlink/?LinkID=252073)|  
|**使用 Team Foundation 版本控制共享模型、关系图和代码图**：<br /><br /> -将代码图，以便可以共享这些建模项目、 UML 关系图和层关系图置于 Team Foundation 版本控制之下。|当多个用户使用 Team Foundation 版本控制下的这些项时，使用这些指南会有助于避免版本控制问题：<br /><br /> -   [管理模型和版本控制下的关系图](../modeling/manage-models-and-diagrams-under-version-control.md)|  
|**从 UML 或域特定语言生成或配置应用程序的各部分**：<br /><br /> -使你的设计更好地响应要求更改和轻松变量跨产品系列。|-   [生成并配置你的应用模型](../modeling/generate-and-configure-your-app-from-models.md)|  
|**自定义模型和关系图**：<br /><br /> -调整模型中，以你的项目如何通过定义 UML 元素，验证约束，以确保模型符合业务规则和其他菜单命令和工具箱项的其他属性来使用它们。<br />-创建你自己的域特定语言。|-   [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)<br />-   [Visual Studio 域特定语言的建模 SDK](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|  
|**使用 T4 模板生成文本**：<br /><br /> -使用文本块和深入了解模板的控制逻辑生成基于文本的文件。|-   [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)|  
  
## <a name="types-of-models-and-their-uses"></a>模型类型和用法  
  
|**模型类型和典型用法**|  
|-------------------------------------|  
|**代码图**<br /><br /> 代码图可帮助查看代码中的组织和关系。<br /><br /> 典型用法：<br /><br /> -检查程序代码以便您可以更好地了解其结构和其依赖项，如何更新它，并估算的成本建议的更改。<br /><br /> 请参阅：<br /><br /> -   [映射解决方案之间的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />-   [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [使用代码图分析器发现潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)|  
|**层关系图**<br /><br /> 层关系图可将应用程序的结构定义为一组带有显式依赖项的层或块。 可以运行验证来发现代码中依赖项和层关系图中所述依赖项之间的冲突。<br /><br /> 典型用法：<br /><br /> -其生命周期来稳定其结构的应用程序通过大量更改。<br />签入的代码更改之前发现无意的依赖项冲突。<br /><br /> 请参阅：<br /><br /> -   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：引用](../modeling/layer-diagrams-reference.md)<br />-   [使用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|  
|**UML 模型**<br /><br /> UML 模型包含多个视图，其中包括类、组件、用例、活动和序列图。 可以自定义 UML 以满足自己的应用程序域。 例如，可以将标记、其他信息和约束附加到模型元素。 还可以定义在模型上操作的工具。 请参阅[为您的应用程序创建模型](../modeling/create-models-for-your-app.md)。<br /><br /> 典型用法：<br /><br /> -描述要求和设计。 可以将 UML 快速地应用于任何应用程序的开发中。 请参阅[在您的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)。<br />-生成或配置测试或应用程序的各个部分。 若要自定义表示法并开发生成模板或可配置应用程序，则需要进行一些工作。 请参阅[生成和配置将应用程序模型从](../modeling/generate-and-configure-your-app-from-models.md)。<br />-对于一般的说明和代码生成或配置中较小的项目。|  
|**域特定语言 (DSL)**<br /><br /> DSL 是为特定目的而设计的一种表示法。 在 Visual Studio 中通常表示为图形。<br /><br /> 典型用法：<br /><br /> 生成或配置应用程序的各部分。 若要开发表示法和工具，则需要进行工作。 其产生的结果，与 UML 自定义相比，会更好地适应你的域。<br />-对于大型项目或开发 DSL 和其工具方面的投资由多个项目中使用该产品行。<br /><br /> 请参阅：<br /><br /> -   [Visual Studio 域特定语言的建模 SDK](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|  
  
## <a name="where-can-i-get-more-information"></a>在何处可以获取详细信息？  
  
|||  
|-|-|  
|**论坛**|-   [Visual Studio 可视化和建模工具](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](http://go.microsoft.com/fwlink/?LinkId=184721)|  
  
## <a name="see-also"></a>请参阅  

- [什么是 Visual Studio 2015 中建模的新增功能](../modeling/what-s-new-for-design-in-visual-studio.md)   
- [DevOps 和应用程序生命周期管理](https://msdn.microsoft.com/library/74a1f71d-7f23-4c71-8fd7-89ede614fab6)
