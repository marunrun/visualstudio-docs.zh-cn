---
title: 在其他 Visual Studio 版本中读取模型和关系图
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- models, versions of Visual Studio
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 29c190115836972f86590233e331f172422efbd6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747427"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>在其他 Visual Studio 版本中读取模型和关系图

如果你在一个不支持创建模型的 Visual Studio 中打开模型，该模型将以只读模式打开。 在此模式下，你可以更改的关系图的布局，但不能更改该模型。

若要查看支持模型创建的版本，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>获取对某一模型和关系图的访问权限

若要读取依赖关系图，必须首先使用 Visual Studio 打开建模项目，然后打开该项目中的关系图。

出于此原因，如果想要读取依赖关系关系图，则还必须具有对在其中创建它的建模项目的访问权限。 为此，可以从源代码管理访问项目，或通过获取项目文件的副本。

> [!NOTE]
> 这不适用于从代码生成的代码图和 .NET 类图。 这些关系图可以独立建模项目中查看。

若要读取依赖关系图，所需的最小文件集如下所示：

- 要读取的关系图的两个关系图文件，例如**MyDiagram. .classdiagram 和 MyDiagram**。

    > [!NOTE]
    > 对于依赖关系图，还应具有名为_MyDiagram_ **. microsoft.visualstudio.teamarchitect.layerdesigner.diagrams.layerdiagram.show**的文件。

- 建模项目文件（**mymodel>. .modelproj**）

- 根模型文件（**ModelDefinition\MyModel.uml**）

- 关系图中引用的任何包的包文件（**ModelDefinition\MyPackage.uml**）

## <a name="changes-that-you-can-make-in-read-only-mode"></a>在只读模式下可执行的更改

如果你在一个不支持创建模型的 Visual Studio 中打开模型及其关系图，则你无法更改模型。 也就是说，你无法更改显示在关系图或模型资源管理器上的元素和关系。 但是，你可以对关系图的布局进行某些更改：

- 重新排列关系图上的形状和连接符。

- 展开和折叠形状

你可以保存这些更改。 如果要使您的更改对其他用户可见，则至少必须发送更新后的 **. layout**文件。

## <a name="see-also"></a>请参阅

- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [为应用程序创建模型](../modeling/create-models-for-your-app.md)