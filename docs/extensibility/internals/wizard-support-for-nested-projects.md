---
title: 嵌套项目的向导支持 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f7f37700d908167ebef8c071021558822bdce173
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703190"
---
# <a name="wizard-support-for-nested-projects"></a>嵌套项目的向导支持
IDE 运行嵌套项目的父项目可以实现的两个向导：**新项目**向导和 **"添加项目**"向导。

 如果用户通过选择 **"添加项目**"并单击"文件"菜单上**的"新项目**"，或者通过选择"解决方案资源管理器中的 **"添加**和右键单击**新项目**"来启动**新项目**向导，则 IDE 将运行**AddProject**命令，父项目的**AddProject**命令的实现返回模板项目文件，或返回具有一组上下文参数的向导 （.vsz） 文件。

 同样，父项目的**AddItem**向导的实现返回具有一组不同上下文参数的 .vsz 文件。

 有关向导的详细信息，请参阅[向导 （。Vsz） 文件](../../extensibility/internals/wizard-dot-vsz-file.md)、[上下文参数](../../extensibility/internals/context-parameters.md)和[注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
