---
title: 链接模型元素和工作项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.common.removeworkitemsdialog
- vs.teamarch.common.linkworkitemsdialog
helpviewer_keywords:
- UML - extending, linking to TFS work items
- UML - extending, linking work items
- work items, creating from UML models
- UML model, creating work items
- work items, linking to UML models
- UML model, linking work items
ms.assetid: e687a490-0f93-412c-a1ff-eea83cf7ba07
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ee4fea9e3fb1d5b4d27b1d520ac2ab036747f73d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657633"
---
# <a name="link-model-elements-and-work-items"></a>链接模型元素和工作项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过链接 Visual Studio 中的模型元素和 Team Foundation Server 或 Visual Studio Team Services 中的工作项，可以跟踪任务、测试案例、Bug、需求、问题和其他与你的模型相关的工作。 将文档附加到链接的工作项可将其与模型元素关联。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

> [!NOTE]
> 必须使用 Team Explorer 才能创建和打开链接。 确保你的建模项目和关系图已签入到版本控制中，以便其他人可打开链接的关系图。

 例如，你可以链接：

- 用户情景工作项和活动图，以演示如何将情景作为一个操作序列实现

- 用例图上的用例和测试用例工作项，以确保正确实现用例

- UML 类图中类的特性和 Bug 工作项，以显示实现特性的过程中出现的错误。

- 组件图中的组件和任务工作项，以跟踪组件的开发。 此类任务通常将细分为更小的任务

  你可以将工作项链接到你可以在建模关系图上或 UML 模型资源管理器中选择的任何元素，如下列项：

- UML 模型中的所有元素，例如 UML 类、生命线、用例、子系统、活动、对象节点、组件和接口

- UML 模型中的所有关系，例如关联、泛化、依赖项、流和消息

- 元素的各个部分，例如类的特性和操作、生命线的执行次数、活动的输入插针和输出插针、以及组件的各个部件和端口

- 层和层依赖项

- 注释和注释链接

- 关系图。 若要选择关系图，请选择关系图的空白部分。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

- [连接到团队项目](#ConnectTFS)

- [将模型元素链接到新工作项](#LinkNew)

- [将模型元素链接到现有工作项](#LinkExisting)

- [查看已链接到模型元素的工作项](#OpenWorkItem)

- [查看已链接到工作项的模型元素](#ViewLinkedModels)

- [删除模型元素和工作项之间的链接](#RemoveLinks)

- [故障排除](#Troubleshooting)

## <a name="connect-to-a-team-project"></a><a name="ConnectTFS"></a> 连接到团队项目
 必须先连接到团队项目才能创建、查看或删除链接。

1. 在“团队” **** 菜单上，选择“管理连接” **** ，以显示“团队资源管理器”窗口。

2. 如果未显示正确的项目，则在团队资源管理器中选择“管理连接” **** ，然后选择“连接到团队项目” ****。 然后选择正确的项目或服务器（如有必要）。

3. 在 **“团队资源管理器”** 中，选择要在其中创建、链接或查看工作项的项目。

## <a name="link-a-model-element-to-a-new-work-item"></a><a name="LinkNew"></a> 将模型元素链接到新工作项

1. 确保连接到想要使用的 TFS 实例。

2. 在建模图上或 **“UML 模型资源管理器”** 中，打开模型元素的快捷菜单。

3. 选择 **“创建工作项”** 和要创建的工作项类型。

4. 在工作项窗体中，填写字段。 选择 **“保存工作项”**。

     Visual Studio 将模型元素链接到新的工作项。 模型元素上或其附近将显示一个图标。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

## <a name="link-a-model-element-to-an-existing-work-item"></a><a name="LinkExisting"></a> 将模型元素链接到现有工作项
 将模型元素链接到工作项时，从模型元素而不是工作项开始。

1. 确保连接到想要使用的 TFS 实例。

2. 在建模图上或 **“UML 模型资源管理器”** 中，打开模型元素的快捷菜单。 选择 **“链接到工作项”**。 然后在 **“项目”** 字段中选择你的项目。

3. 通过执行下列步骤之一，选择要链接到模型元素的一个或多个工作项：

    - 在 **“已保存查询”** 中选择一个查询。

    - 在 **“ID”** 中键入一个或多个工作项的 ID（用空格分隔）。

    - 在 **“标题包含”** 中键入一个词或词组。

4. 选择 **“查找”**。

5. 在工作项列表中，选择要链接的一个或多个工作项。

     完成后，模型元素的 **“工作项”** 属性将显示一个比之前更大的数字。 模型元素上或其附近还将显示一个图标。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

## <a name="view-work-items-linked-to-a-model-element"></a><a name="OpenWorkItem"></a> 查看链接到模型元素的工作项

1. 在“团队资源管理器” **** 中，确保你已连接团队项目，该团队项目中的工作项已链接到模型元素。

2. 在建模图上或 **“UML 模型资源管理器”** 中，打开模型元素的快捷菜单。 选择 **“查看工作项”** 以查看链接工作项的列表。

    > [!NOTE]
    > 仅显示当前连接的服务器中的工作项。 如果你未看到任何工作项，请确保你已连接到 **“团队资源管理器”** 中的正确服务器。

## <a name="view-model-elements-linked-to-a-work-item"></a><a name="ViewLinkedModels"></a> 查看链接到工作项的模型元素
 你可在 Visual Studio Team Services 和 Team Foundation Server 2012 或更高版本中查看建模图和已链接到工作项的元素。 例如，一个工作项可能已链接到类模型，这些类模型显示要实现的新类的设计。

1. 在“团队资源管理器” **** 中，确保你已连接团队项目，该团队项目中的模型元素已链接到工作项。

    > [!NOTE]
    > 你只能使用团队资源管理器（而不是 Team Web Access）查看链接的模型元素。 确保你的工作区已映射到包含建模图或元素的建模项目。 如果你没有工作区，则必须创建它。 请参阅 [疑难解答](#Troubleshooting) 和 [创建和使用工作区](https://msdn.microsoft.com/library/1d7f6ed8-ec7c-48f8-86da-9aea55a90d5a)。

2. 打开工作项，选择 **“链接”**。 在 **“模型链接”** 下，打开链接的模型元素的快捷菜单。 选择 **“打开链接项”**。

     ![打开工作项中链接的模型元素](../modeling/media/workitem-openlinkedmodelelement.png "WorkItem_OpenLinkedModelElement")

## <a name="delete-links-between-model-elements-and-work-items"></a><a name="RemoveLinks"></a> 删除模型元素和工作项之间的链接
 通过从模型元素开始来移除链接的工作项。 这将正确移除从工作项至模型元素的反向链接。 否则，如果你从工作项开始，则将不会移除从模型元素到工作项的反向链接。

1. 在建模图上或 **“UML 模型资源管理器”** 中，打开模型元素的快捷菜单。

2. 选择 **“移除工作项”**。

     \- 或 -

    1. 选择 **“属性”**，然后选择 **“工作项”** ，此处将会显示链接工作项的数量。

    2. 在 **“工作项”** 属性中，选择省略按钮 **[…]**。

        > [!NOTE]
        > 将仅显示当前服务器上的工作项。 如果列表为空，但工作项的数量不为零，则确保你已连接到 **“团队资源管理器”** 中的正确服务器。

3. 在 **“移除指向工作项的链接”** 下，清除要取消链接的选定项。 选择“确定”。

## <a name="troubleshooting"></a><a name="Troubleshooting"></a> 故障排除

|**问题**|可能的原因 |**分辨率**|
|---------------|------------------------|--------------------|
|无法找到要链接的模型元素。|此元素可能位于 [!INCLUDE[esprscc](../includes/esprscc-md.md)]中某建模项目的某个关系图上。 您可能没有映射到该关系图的工作区。|将您的工作区映射到该建模项目和关系图。 如果您没有工作区，则必须创建它。<br /><br /> 针对此问题显示的错误消息包含的路径可用来映射您的工作区。<br /><br /> 请参阅 [创建和使用工作区](https://msdn.microsoft.com/library/1d7f6ed8-ec7c-48f8-86da-9aea55a90d5a)。|
|无法找到链接的模型元素。|链接元素可能位于已移动、重命名或删除的关系图上。|1. 在工作项中，删除指向模型元素的链接。<br />2. 创建从工作项到模型元素的新链接。|
|工作项没有你需要的链接模型元素。|仅在链接是从工作项创建的情况下，工作项才显示链接的层元素。 如果您的团队不使用 [!INCLUDE[esprscc](../includes/esprscc-md.md)]，则使用关系图的本地路径创建链接。 如果建模项目及其关系图位于 [!INCLUDE[esprscc](../includes/esprscc-md.md)]中，则能够访问项目的所有团队成员都可以查看工作项中链接的元素。|尝试刷新工作项。|
|删除从工作项到模型元素的链接并不会删除从模型元素到工作项的链接。||从模型元素开始删除与工作项的链接。|

## <a name="see-also"></a>另请参阅
 [编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)[为您的应用程序创建模型](../modeling/create-models-for-your-app.md)
