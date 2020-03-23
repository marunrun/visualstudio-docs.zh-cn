---
title: 扩展图层图 |微软文档
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
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301253"
---
# <a name="extend-layer-diagrams"></a>Extend layer diagrams
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以编写代码以创建和更新层关系图，并针对 Visual Studio 中的层关系图验证程序代码的结构。 可以添加显示在关系图的快捷（上下文）菜单上的命令、自定义拖放笔势并从文本模板访问层模型的命令。 可以将这些扩展打包到 Visual Studio 集成扩展 (VSIX) 中，并将其分发给其他 Visual Studio 用户。

 有关层关系图的详细信息，请参阅：

- [层关系图：参考](../modeling/layer-diagrams-reference.md)

- [层关系图：指南](../modeling/layer-diagrams-guidelines.md)

- [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)

- [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

## <a name="requirements"></a><a name="prereqs"></a>要求
 必须在想要开发层扩展的计算机上安装了以下内容：

- Visual Studio

- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)

- [2015 年可视化工作室建模 SDK](https://www.microsoft.com/download/details.aspx?id=48148)

  在想要运行层扩展的计算机上必须安装合适版本的 Visual Studio。 有关详细信息，请参阅[部署图层模型扩展](../modeling/deploy-a-layer-model-extension.md)。

  若要查看支持层关系图的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="in-this-section"></a>本节内容
 [向层关系图添加命令和笔势](../modeling/add-commands-and-gestures-to-layer-diagrams.md)

 [向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)

 [向层关系图添加自定义属性](../modeling/add-custom-properties-to-layer-diagrams.md)

 [在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)

 [部署层模型扩展](../modeling/deploy-a-layer-model-extension.md)

 [层关系图扩展疑难解答](../modeling/troubleshoot-extensions-for-layer-diagrams.md)

## <a name="see-also"></a>另请参阅
 [定义并安装建模扩展层](../modeling/define-and-install-a-modeling-extension.md)[关系图：参考](../modeling/layer-diagrams-reference.md)[层图：指南](../modeling/layer-diagrams-guidelines.md)[从代码创建图层关系图](../modeling/create-layer-diagrams-from-your-code.md)[使用层关系图 验证代码](../modeling/validate-code-with-layer-diagrams.md)使用 UML 模型 使用 Visual Studio API 打开[UML 模型 打开 UML 模型](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)[Generate files from a UML model](../modeling/generate-files-from-a-uml-model.md)
