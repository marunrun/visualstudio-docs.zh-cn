---
title: 类设计器错误
ms.date: 11/04/2016
ms.topic: troubleshooting
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
- error messages, class diagrams
- Class Designer [Visual Studio], errors
- class diagrams, errors
ms.assetid: 79d70e70-704c-4255-ab68-c10d6949470e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aadc0cfb66226f463ff8a2049d4dbf81e7bcf62b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975569"
---
# <a name="class-designer-errors"></a>类设计器错误

“类设计器”不会跟踪源文件的位置，因此修改项目结构或移动项目中的源文件就可能导致“类设计器”无法继续对类型进行跟踪，例如通常会修改 typedef 的源类型、基类或关联类型。 可能会收到错误，如“类设计器无法显示此类型”。 若要解决此错误，将修改过的或被重新定位的源代码再次拖到类图中以显示它。

## <a name="resources"></a>资源

你在以下资源中找到关于其他错误和警告的协助：

- [使用 Visual C++ 代码](working-with-visual-cpp-code.md)包括有关在类图中显示 C++ 的疑难解答信息。
- [Visual Studio 类设计器论坛](http://go.microsoft.com/fwlink/?LinkId=160754)提供一个有关“类设计器”问题的论坛。

## <a name="see-also"></a>请参阅

- [设计和查看类和类型](designing-and-viewing-classes-and-types.md)
