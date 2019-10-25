---
title: 嵌套项目的向导支持 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e498f21499f4b07bf77bb79829fc6d92227f1f2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721423"
---
# <a name="wizard-support-for-nested-projects"></a>嵌套项目的向导支持
IDE 运行可实现嵌套项目的父项目的两个向导： "**新建项目**" 向导和 "**添加项**向导"。

 如果用户通过选择 "**添加项目**"，然后在 "文件" 菜单上单击 "**新建项目**"，或在解决方案资源管理器中选择 "**添加**" 并右键单击 "**新建项目**" 来启动 "**新建项目**" 向导，则 IDE 将运行**AddProject**命令和父项目的**AddProject**命令实现返回一个模板项目文件或一个向导（.vsz）文件，该文件具有一组上下文参数。

 同样，一个父项目的**AddItem**向导实现返回一个 .vsz 文件，该文件具有一组不同的上下文参数。

 有关向导的详细信息，请参阅[向导（.Vsz）文件](../../extensibility/internals/wizard-dot-vsz-file.md)、[上下文参数](../../extensibility/internals/context-parameters.md)和[注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)