---
title: 嵌套项目 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 814780fa8e7e57a022a75b2e09115cfa55a1b8be
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707031"
---
# <a name="nesting-projects"></a>嵌套项目
使用 VS 包的企业应用程序开发人员可以使用*项目嵌套*来方便地将类似类型的项目[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]分组在一起。 例如，企业模板项目使用嵌套项目将项目分组到类别中。 业务外观项目、Web UI 项目等被分组到一个类别中。

 在这种情况下，开发人员可以嵌套在每个父项目下的项目数量没有限制，尽管开发人员可以以编程方式提供限制。 这种类型的分组也可以递归，在这种情况下，与子项目类型相同的项目可以嵌套在子项下，成为子项的子项，该子项目是父项的子项目。

 项目嵌套不是 的固有部分[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 您必须编写代码才能在子项目中启用嵌套和子项目嵌套。 父项目是使用其自己的 GUID 创建和注册的特殊的 VSPackage 或项目类型，其中包括实现项目嵌套所需的代码。

 您可以在["如何：实现嵌套项目](../../extensibility/internals/how-to-implement-nested-projects.md)"中找到有关如何嵌套项目的示例。

## <a name="nested-projects-example"></a>嵌套项目示例
 ![嵌套项目解决方案](../../extensibility/internals/media/vsnestedprojects.gif "vs 嵌套项目")嵌套项目示例

## <a name="see-also"></a>请参阅
- [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [实现嵌套项目的命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [筛选嵌套项目的 AddItem 对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
