---
title: Extend layer diagrams | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, creating extensions
- layer models
ms.assetid: 83fca301-b008-485a-87eb-218050e71451
caps.latest.revision: 41
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bfcec64f9401fdbf79e67bee5fe8430452632fbc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301032"
---
# <a name="extend-layer-diagrams"></a>Extend layer diagrams
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以编写代码以创建和更新层关系图，并针对 Visual Studio 中的层关系图验证程序代码的结构。 可以添加显示在关系图的快捷（上下文）菜单上的命令、自定义拖放笔势并从文本模板访问层模型的命令。 可以将这些扩展打包到 Visual Studio 集成扩展 (VSIX) 中，并将其分发给其他 Visual Studio 用户。

 有关层关系图的详细信息，请参阅：

- [层关系图：参考](../modeling/layer-diagrams-reference.md)

- [层关系图：指南](../modeling/layer-diagrams-guidelines.md)

- [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)

- [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

## <a name="prereqs"></a> 要求
 必须在想要开发层扩展的计算机上安装了以下内容：

- Visual Studio

- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)

- [Modeling SDK for Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48148)

  在想要运行层扩展的计算机上必须安装合适版本的 Visual Studio。 For more information, see [Deploy a layer model extension](../modeling/deploy-a-layer-model-extension.md).

  若要查看支持层关系图的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="in-this-section"></a>本节内容
 [向层关系图添加命令和笔势](../modeling/add-commands-and-gestures-to-layer-diagrams.md)

 [向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)

 [向层关系图添加自定义属性](../modeling/add-custom-properties-to-layer-diagrams.md)

 [在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)

 [部署层模型扩展](../modeling/deploy-a-layer-model-extension.md)

 [层关系图扩展疑难解答](../modeling/troubleshoot-extensions-for-layer-diagrams.md)

## <a name="see-also"></a>请参阅
 [Define and install a modeling extension](../modeling/define-and-install-a-modeling-extension.md) [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md) [Layer Diagrams: Guidelines](../modeling/layer-diagrams-guidelines.md) [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md) [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md) [Generate files from a UML model](../modeling/generate-files-from-a-uml-model.md) [Open a UML model by using the Visual Studio API](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)
