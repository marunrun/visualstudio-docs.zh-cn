---
title: 在其他 Visual Studio 版本中读取模型和关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- models, versions of Visual Studio
ms.assetid: 46eee279-a9e4-4742-a024-5bd2cf032b86
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a6a7c944eb3d5378ad0fc1542b90ad182f7eb976
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671277"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>在其他 Visual Studio 版本中读取模型和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你在一个不支持创建模型的 Visual Studio 中打开模型，该模型将以只读模式打开。 在此模式下，你可以更改的关系图的布局，但不能更改该模型。

 若要查看支持模型创建的版本，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>获取对某一模型和关系图的访问权限
 若要读取 UML 关系图或层关系图，必须首先使用 Visual Studio 打开建模项目，然后打开该项目中的关系图。

 出于此原因，如果你想要读取 UML 关系图或层关系图，则必须有权限访问创建它的建模项目。 可以通过从 [!INCLUDE[esprscc](../includes/esprscc-md.md)] 来获得访问权限，也可以通过获取项目文件的副本来获得访问权限。

> [!NOTE]
> 这不适用于从代码生成的代码图和 .NET 类图。 这些关系图可以独立建模项目中查看。

 若要读取 UML 关系图或层关系图，你所需的最小文件集如下：

- 要读取的关系图的两个关系图文件，例如**MyDiagram. .classdiagram 和 MyDiagram**。

    > [!NOTE]
    > 对于层关系图，还应具有名为_MyDiagram_ **. microsoft.visualstudio.teamarchitect.layerdesigner.diagrams.layerdiagram.show**的文件。

- 建模项目文件（**mymodel>. .modelproj**）

- 根模型文件（**ModelDefinition\MyModel.uml**）

- 关系图中引用的任何包的包文件（**ModelDefinition\MyPackage.uml**）

## <a name="changes-that-you-can-make-in-read-only-mode"></a>在只读模式下可执行的更改
 如果你在一个不支持创建模型的 Visual Studio 中打开模型及其关系图，则你无法更改模型。 也就是说，你无法更改显示在关系图或模型资源管理器上的元素和关系。 但是，你可以对关系图的布局进行某些更改：

- 重新排列关系图上的形状和连接符。

- 展开和折叠形状

  你可以保存这些更改。 如果要使您的更改对其他用户可见，则至少必须发送更新后的 **. layout**文件。

## <a name="RelatedTopics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[层关系图：参考](../modeling/layer-diagrams-reference.md)|层关系图显示现有或建议的体系结构的结构。 写入代码后，可以自动依照层关系图对代码进行验证。|
|[UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)|活动图显示业务流程或软件中的工作流。|
|[UML 类图：参考](../modeling/uml-class-diagrams-reference.md)|类图显示许多上下文中（如代码、数据库架构、通讯协议或用于描述业务域的术语的词汇表）使用的类型和关系。|
|[UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)|组件图显示软件设计中可分离的部分及其接口。|
|[UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)|序列图显示软件设计中元素之间的交互。|
|[UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)|用例图显示系统用户以及他们为实现特定目标可以执行的活动。|

## <a name="see-also"></a>请参阅
 [为应用程序创建模型](../modeling/create-models-for-your-app.md)
