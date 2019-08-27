---
title: 嵌套项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 289062a15c35641d5558409c7643301e346b6e65
ms.sourcegitcommit: f42b5318c5c93e2b5ecff44f408fab8bcdfb193d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69976695"
---
# <a name="nesting-projects"></a>嵌套项目
使用 VS 包的企业应用程序开发人员可以通过使用*项目嵌套*, 在中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]轻松地将相似类型的项目组合在一起。 例如, 企业模板项目使用嵌套项目将项目分组到类别中。 业务外观项目、Web UI 项目等在一个类别中组合在一起。

 在此方案中, 开发人员可以在每个父项目下嵌套的项目数没有限制, 尽管开发人员可以通过编程方式提供限制。 这种类型的分组也可以是递归的, 在这种情况下, 与子项目属于同一类型的项目可以嵌套在子项目下, 以成为作为父项的子项目的子项目。

 项目嵌套不是的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]内部部分。 您必须编写代码, 以便在子项目中启用嵌套和子项目嵌套。 父项目是一种特殊的 VSPackage 或项目类型, 使用其自己的 GUID 创建并注册, 其中包含实现项目嵌套所需的代码。

 有关如何在[如何: 中嵌套项目的示例, 请查看如何:实现嵌套项目](../../extensibility/internals/how-to-implement-nested-projects.md)。

## <a name="nested-projects-example"></a>嵌套项目示例
 ![嵌套项目解决方案](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects")嵌套项目示例

## <a name="see-also"></a>请参阅
- [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [实现嵌套项目的命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [筛选嵌套项目的 AddItem 对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
