---
title: 在其他 Visual Studio 版本中读取模型和关系图
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- models, versions of Visual Studio
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebe4cdcefb7b823090cca8976055de5a3ebb9b1a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595405"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>在其他 Visual Studio 版本中读取模型和关系图

如果你在一个不支持创建模型的 Visual Studio 中打开模型，该模型将以只读模式打开。 在此模式下，你可以更改的关系图的布局，但不能更改该模型。

若要查看哪些版本的 Visual Studio 支持创建模型，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>获取对某一模型和关系图的访问权限

若要读取依赖项关系图，必须首先使用 Visual Studio 打开建模项目中，并打开关系图中。

出于此原因，如果你想要读取依赖项关系图中，您还必须在其中创建建模项目的访问权限。 您可以执行此操作通过访问从源代码管理项目或获取项目文件的副本。

> [!NOTE]
> 这不适用于从代码生成的代码图和 .NET 类图。 这些关系图可以独立建模项目中查看。

若要读取依赖项关系图，所需的文件的最小集如下所示：

- 两个关系图文件为你想要读取，例如，该关系图**MyDiagram.classdiagram 和 MyDiagram.classdiagram.layout**。

    > [!NOTE]
    > 有关依赖项关系图，还应具有名为的文件_MyDiagram_ **。 layerdiagram.suppressions**。

- 建模项目文件 (**MyModel.modelproj**)

- 根模型文件 (**ModelDefinition\MyModel.uml**)

- 在关系图中引用的任何包的包文件 (**ModelDefinition\MyPackage.uml**)

## <a name="changes-that-you-can-make-in-read-only-mode"></a>在只读模式下可执行的更改

如果你在一个不支持创建模型的 Visual Studio 中打开模型及其关系图，则你无法更改模型。 也就是说，你无法更改显示在关系图或模型资源管理器上的元素和关系。 但是，你可以对关系图的布局进行某些更改：

- 重新排列关系图上的形状和连接符。

- 展开和折叠形状

你可以保存这些更改。 如果你想要使所做的更改对其他用户可见，则必须至少发送已更新 **.layout**文件。

## <a name="see-also"></a>另请参阅

- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [为应用程序创建模型](../modeling/create-models-for-your-app.md)
