---
title: 扩展层关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, creating extensions
- layer models
ms.assetid: 83fca301-b008-485a-87eb-218050e71451
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: af191c929b88f1bda76896061359b7315517beb5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182873"
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
  
- [Visual Studio 2015 建模 SDK](http://www.microsoft.com/download/details.aspx?id=48148)  
  
  在想要运行层扩展的计算机上必须安装合适版本的 Visual Studio。 有关详细信息，请参阅[部署层模型扩展](../modeling/deploy-a-layer-model-extension.md)。  
  
  若要查看支持层关系图的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
## <a name="in-this-section"></a>本节内容  
 [向层关系图添加命令和笔势](../modeling/add-commands-and-gestures-to-layer-diagrams.md)  
  
 [向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)  
  
 [向层关系图添加自定义属性](../modeling/add-custom-properties-to-layer-diagrams.md)  
  
 [在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)  
  
 [部署层模型扩展](../modeling/deploy-a-layer-model-extension.md)  
  
 [层关系图扩展疑难解答](../modeling/troubleshoot-extensions-for-layer-diagrams.md)  
  
## <a name="see-also"></a>请参阅  
 [定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)   
 [层关系图：引用](../modeling/layer-diagrams-reference.md)   
 [层关系图：指导原则](../modeling/layer-diagrams-guidelines.md)   
 [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)   
 [使用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)   
 [从 UML 模型生成文件](../modeling/generate-files-from-a-uml-model.md)   
 [使用 Visual Studio API 打开 UML 模型](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)
