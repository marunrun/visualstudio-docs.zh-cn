---
title: 扩展依赖项关系图
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, creating extensions
- layer models
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a8297ede4ce703c738133952bb13669ef6a6637
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645672"
---
# <a name="extend-dependency-diagrams"></a>扩展依赖项关系图

您可以编写代码来创建和更新依赖关系图，并针对 Visual Studio 中的依赖项关系图验证程序代码的结构。 可以添加显示在关系图的快捷（上下文）菜单上的命令、自定义拖放笔势并从文本模板访问层模型的命令。 可以将这些扩展打包到 Visual Studio 集成扩展 (VSIX) 中，并将其分发给其他 Visual Studio 用户。

## <a name="requirements"></a>要求

必须在想要开发层扩展的计算机上安装了以下内容：

- Visual Studio

- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)

- Visual Studio 的建模 SDK

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

你必须在要运行层扩展的计算机上安装合适版本的 Visual Studio。 若要查看支持依赖关系图的 Visual Studio 版本，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="see-also"></a>请参阅

- [依赖项关系图：参考](../modeling/layer-diagrams-reference.md)
- [依赖项关系图：指南](../modeling/layer-diagrams-guidelines.md)
- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)
- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)
