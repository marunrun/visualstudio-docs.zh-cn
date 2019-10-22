---
title: 有关类设计器错误的附加信息 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.CPlusPlusViewInDiagramNoTypeFound
- vs.classdesigner.CPlusPlusNoTypeFound
- vs.classdesigner.CannotShowBaseType
- vs.classdesigner.MatchOrphanTypesAtLoad
- vs.classdesigner.CannotShowType
- vs.classdesigner.AssociationTypeNotFoundError
- vs.classdesigner.ViewInDiagramNoTypesFound
- vs.classdesigner.CannotImplementInterface
- vs.classdesigner.CannotShowImplementedInterface
- vs.classdesigner.ViewInDiagramUnparsableTypeFound
- vs.classdesigner.AssociationTypeNotFound
- vs.classdesigner.CPlusPlusTypeCannotBeAdded
helpviewer_keywords:
- errors, class diagrams
- errors, Class Designer
- error messages, Class Designer
- Class Designer [Visual Studio], errors
- error messages, class diagrams
- class diagrams, errors
ms.assetid: 79d70e70-704c-4255-ab68-c10d6949470e
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7500782a1d935c08ae95e26764c9476c63f36660
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72620394"
---
# <a name="additional-information-about-class-designer-errors"></a>有关类设计器错误的附加信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类设计器不会跟踪源文件的位置，因此修改项目结构或移动项目中的源文件就可能导致类设计器无法继续对类型（尤其是 typedef 的源类型、基类或关联类型）进行跟踪。 可能会收到错误，如“类设计器无法显示此类型”  。 如果收到错误，要将修改过的或被重新定位的源代码再次拖到类图中以重新显示。

 你在以下资源中找到关于其他错误和警告的协助：

 [使用 Visual C++ Code （类设计器）](../ide/working-with-visual-cpp-code-class-designer.md)包括有关在类图中C++显示的疑难解答信息。

 [Visual Studio 类设计器论坛](http://go.microsoft.com/fwlink/?LinkId=160754)提供一个有关类设计器相关问题的论坛。

## <a name="see-also"></a>另请参阅
 [设计和查看类与类型](../ide/designing-and-viewing-classes-and-types.md)
