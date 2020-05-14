---
title: 视觉工作室中的层次结构 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cdbb8a0e58f6b1e5bc6e32f8c319d1480c4db4b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708188"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio 中的层次结构
集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]开发环境 （IDE） 将项目显示为*层次结构*。 在 IDE 中，层次结构是节点树，其中每个节点都有一组关联的属性。 *项目层次结构*是一个容器，用于保存项目的项、项的关系以及项的关联属性和命令。

 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中，使用 层次结构接口 管理项目层次结构<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>。 接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>将调用的命令从项目项重定向到相应的层次结构窗口，而不是标准命令处理程序。

## <a name="project-hierarchies"></a>项目层次结构
 每个项目层次结构都包含可以查看和编辑的项目。 这些项目因项目类型而异。 例如，数据库项目可能包含存储过程、数据库视图和数据库表。 另一方面，编程语言项目可能包括位图和对话框的源文件和资源文件。 层次结构可以嵌套，这在创建项目层次结构时为您提供了一些更大的灵活性。

 创建新项目类型时，项目类型控制可在其中编辑的完整项集。 但是，项目可以包含它们不支持的项目。 例如，Visual C++ 项目可以包含 HTML 文件，即使 Visual C++ 不为 HTML 文件类型提供任何自定义编辑器。

 层次结构管理它们包含的项的持久性。 层次结构的实现必须控制影响层次结构中项持久性的任何特殊属性。 例如，如果项表示存储库中的对象而不是文件，则层次结构实现必须控制这些对象的持久性。 IDE 本身指示层次结构按照用户输入保存项，但 IDE 不控制保存这些项目所需的任何操作。 相反，项目处于控制之下。

 当用户在编辑器中打开项时，将选择控制该项的层次结构，并成为活动层次结构。 所选层次结构确定可用于对项执行操作的命令集。 以这种方式跟踪用户焦点使层次结构能够反映用户的当前上下文。

## <a name="see-also"></a>请参阅
- [项目类型](../../extensibility/internals/project-types.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)
