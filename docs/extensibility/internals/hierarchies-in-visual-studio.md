---
title: 在 Visual Studio 中的层次结构 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 29eb35e807c467b64a89f48705c555d4083ceef7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328842"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio 中的层次结构
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE) 显示为一个项目*层次结构*。 在 IDE 中，层次结构是的节点，其中每个节点都有一组相关联的属性的树。 一个*项目层次结构*是保存项目的项目、 项目的关系和相关联的项目的属性和命令的容器。

 在中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，使用层次结构界面管理项目层次结构<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口将重定向到适当的层次结构窗口而不是标准命令处理程序调用从项目项的命令。

## <a name="project-hierarchies"></a>项目层次结构
 每个项目层次结构包含你可以查看和编辑的项。 这些项会有所不同，具体取决于项目类型。 例如，存储的过程、 数据库视图和数据库表可能包含数据库项目。 但是，编程语言项目中，将可能包括源文件和的位图和对话框资源文件。 可以嵌套层次结构，后者可提供一些更灵活地创建项目层次结构时。

 在创建新项目类型时，项目类型控制可以在其中编辑的项的完整集合。 但是，项目可以包含为其无权编辑支持的项。 例如，视觉对象C++项目可以包含 HTML 文件，即使 VisualC++不提供任何自定义的编辑器输入 HTML 文件类型。

 层次结构管理它们所包含的项的暂留。 层次结构的实现必须控制任何特殊属性，它们会影响层次结构中的项的持久性。 例如，如果项表示的对象而不是文件的存储库中，层次结构实现必须控制这些对象的持久性。 IDE 本身指示要保存符合用户输入的项的层次结构，但 IDE 不保存这些项所需的任何操作进行控制。 相反，该项目是在控件中。

 当用户在编辑器中打开某个项时，控制该项目的层次结构处于选中状态，而将成为活动的层次结构。 所选层次结构确定命令，可用于对项的集。 跟踪用户焦点以这种方式使层次结构，以反映用户的当前上下文。

## <a name="see-also"></a>请参阅
- [项目类型](../../extensibility/internals/project-types.md)
- [所选内容和 IDE 中的货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [VSSDK 示例](https://aka.ms/vs2015sdksamples)