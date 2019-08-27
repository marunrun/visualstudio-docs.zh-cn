---
title: 扩展 UML 模型和关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending
- UML model, extending
ms.assetid: b5bfa61e-ea59-4c3b-b5af-53475d7d13cd
caps.latest.revision: 39
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 917c88056709cfbeb89ce3f19d9c8da9866feb4e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182871"
---
# <a name="extend-uml-models-and-diagrams"></a>扩展 UML 模型和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题汇总了扩展 Visual Studio 包含的 UML 建模工具可使用的不同方法。 若要查看支持每个模型类型和工具的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
 在下面的示例方案中，Fabrikam 设计并安装机场行李处理系统。 从一个机场项目到下一个机场项目，基本设备及其控制软件有许多相似之处。 但也有若干因素大不相同，例如传送带、签入服务台、行李箱和其他行李处理设备的配置。  
  
 在开始一个新项目时，Fabrikam 团队创建了一个 UML 模型来帮助他们在他们之间以及与客户讨论这些需求。 他们使用活动图来表示行李流，对象节点表示每件设备。 UML 模型不直接表示系统的代码。  
  
 Fabrikam 的工具团队进行了一系列改进来帮助开发团队。 下面各节描述了可以定义的不同种类的扩展。 可以将其中一些技术组合到一个 Visual Studio 扩展中。  
  
 有关详细信息，请观看此视频：![链接至视频](../data-tools/media/playvideo.gif "播放视频")[MSDN 如何实现系列：UML 工具和扩展性](http://go.microsoft.com/fwlink/?LinkId=214467)。  
  
## <a name="Requirements"></a> 要求  
  
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
- [Visual Studio 2015 的建模 SDK](http://www.microsoft.com/download/details.aspx?id=48148)。  
  
## <a name="profiles"></a>配置文件  
 配置文件用于对 UML 元素定义构造型和其他属性。  
  
 Fabrikam 的工具开发人员对活动图的对象节点（如 «conveyor belt» 和 «checkin desk»）定义构造型。 现在，团队成员在使用活动图创建行李处理方案时，即可设置构造型来指示每个节点表示的设备类型。 工具开发人员对某些构造型定义附加属性，这样用户就可以记录一些值，例如传送带的容量和签入服务台的左右手使用习惯。  
  
 有关详细信息，请参阅[定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)。  
  
## <a name="custom-toolbox-items"></a>自定义工具箱项  
 自定义工具箱项将根据你在关系图中定义的原型创建一个元素或一组元素。 例如，你可以创建一个工具来创建具有特定颜色或构造型的用例，或者创建一组类和关联来表示设计模式。 可以将这些工具箱项添加到 Visual Studio 扩展并将它们分发给其他用户。  
  
 有关详细信息，请参阅[定义一个自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)。  
  
## <a name="validation"></a>验证  
 你可以定义规则来确保 UML 模型符合指定的约束。  
  
 Fabrikam 的工具开发人员通过定义规则来帮助团队成员避免行李处理模型中的简单错误。 例如，签入服务台不能直接连接到行李箱。 它们之间必须至少有一个传送带。  
  
 有关详细信息，请参阅[为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)。  
  
## <a name="menu-commands"></a>菜单命令  
 可以通过右键单击 UML 关系图上的元素来定义用户可以调用的命令。 这些命令可以更新模型和关系图，或在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]中执行其他操作。  
  
 Fabrikam 通过定义菜单命令来自动化经常执行的操作，例如创建签入服务台并将其连接到所选传送带或根据公司的布局规则来重排关系图。  
  
 请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。  
  
## <a name="gestures"></a>笔势  
 你可以定义命令，用户通过双击关系图元素或者拖动到关系图上或关系图上的元素可启动这些命令。 还可以定义命令，用于处理从其他 UML 关系图、从 Visual Studio 的其他部分或者从其他应用程序或 Windows 资源管理器（或文件资源管理器）拖动的项。  
  
 Fabrikam 团队成员可通过从 Windows 桌面拖动文件（如规范）来将该文件与任何模型元素相关联。 工具开发人员定义了一个构造型，它为任何元素提供文件路径属性，以及在将文件拖放到元素上时设置构造型和文件路径的笔势。  
  
 有关详细信息，请参阅[建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)。  
  
## <a name="responding-to-changes"></a>响应更改  
 可以在模型中编写响应更改的代码，而无论其是否由用户操作或其他程序代码所引起。  
  
 Fabrikam 的开发人员创建可依赖元素构造型自动设置其颜色的代码。 这可让用户轻松区分模型中各元素扮演的不同角色。  
  
 有关详细信息，请参阅[如何：响应 UML 模型中的更改](../misc/how-to-respond-to-changes-in-a-uml-model.md)。  
  
## <a name="model-bus"></a>模型总线  
 使用模型总线可以从一个关系图或 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展访问另一个关系图或模型。 它的其中一个优点是，你可以将信息传播到多个模型，从而多人可以同时处理组合模型。  
  
 Fabrikam 使用活动图上的元素表示行李处理设备。 每个设备项可以在其他关系图（可在其他模型中）中有更详细的规范。 对行李流关系图的验证约束可以从其他关系图检索设备的相关属性。 对其他关系图的引用存储在构造型中定义的附加属性中。  
  
 有关详细信息，请参阅[与其他模型和工具集成 UML 模型](../modeling/integrate-uml-models-with-other-models-and-tools.md)。  
  
## <a name="generation"></a>代  
 可以从模型生成程序代码、脚本、配置、文档、新模型或其他项目。  
  
 在 Fabrikam 设计的行李系统中，大部分程序代码在不同项目中都是相同的。 主要的可变因素是行李流环绕机场的规划。 设计团队在拥有首批数个项目的经验后，由工具开发人员创建一个模板，该模板从行李流模型生成大部分可变程序代码和其他文件（如用户文档）。 这样可大大减少每个新项目的开发时间和错误率。  
  
 有关详细信息，请参阅[从 UML 模型生成文件](../modeling/generate-files-from-a-uml-model.md)。  
  
## <a name="team-foundation-server-integration"></a>Team Foundation Server 集成  
 可以将工作项链接到模型元素并以编程方式访问这些链接项。  
  
 Fabrikam 的工具开发人员编写一个工具来为每个机场项目生成工作计划。 将计划中的工作项链接到模型元素。  
  
 有关详细信息，请参阅[定义工作项链接处理程序](../modeling/define-a-work-item-link-handler.md)。  
  
## <a name="tools-that-update-models"></a>更新模型的工具  
 你可以创建可加载 UML 模型的独立应用程序和 Visual Studio 扩展。  
  
 Fabrikam 的开发人员创建一种工具，它可读取模型并对模型的每个元素生成工作进度报告。  
  
 有关详细信息，请参阅[读取程序代码中的 UML 模型](../modeling/read-a-uml-model-in-program-code.md)。  
  
## <a name="domain-specific-languages"></a>域特定语言  
 在经常使用某个特定类型的模型的情况下，创建域特定语言会很有用。 域特定语言比 UML 模型更能符合你的业务需求，只不过你需要进行更多的工作来生成和维护它。 有关详细信息，请参阅[Visual Studio-域特定语言的建模 SDK](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)。  
  
## <a name="external-resources"></a>外部资源  
  
|**类别**|**链接**|  
|------------------|---------------|  
|**视频**|![视频链接](../data-tools/media/playvideo.gif "播放视频") [MSDN 如何实现系列：UML 工具和扩展性](http://go.microsoft.com/fwlink/?LinkId=214467)<br /><br /> ![视频链接](../data-tools/media/playvideo.gif "播放视频")[第 9 频道：使用 Visual Studio 的 UML](http://go.microsoft.com/fwlink/?LinkId=199957)|  
|**论坛**|-   [Visual Studio 可视化和建模工具](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](http://go.microsoft.com/fwlink/?LinkId=184721)|  
|**博客**|[Visual Studio ALM + Team Foundation Server 博客](http://go.microsoft.com/fwlink/?LinkID=201340)|  
|**技术文章和日志**|[MSDN 体系结构中心](http://go.microsoft.com/fwlink/?LinkId=201343)|  
  
## <a name="see-also"></a>请参阅  
 [为您的应用程序创建模型](../modeling/create-models-for-your-app.md)   
 [UML 建模扩展性的 API 参考](../modeling/api-reference-for-uml-modeling-extensibility.md)
