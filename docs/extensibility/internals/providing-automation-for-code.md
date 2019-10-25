---
title: 为代码提供自动化 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 874446aa6bf2e40a120aac49e7d91fd3d861d1d4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724965"
---
# <a name="providing-automation-for-code"></a>提供适用于 Code 的自动化
不需要为代码创建自动化模型。 环境 SDK 并不提供用于执行此操作的示例。 若要深入了解代码模型，请参阅 <xref:EnvDTE.CodeModel> 对象。

 若要实现代码模型，必须实现由您的内部数据结构确定的任何接口。 对象必须从 `IDispatch` 类派生。

 您扩展的对象 <xref:EnvDTE.CodeModel> 和 <xref:EnvDTE.FileCodeModel> 可从 <xref:EnvDTE.Project> 对象获取，如下所示：

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 您可以选择只在从 `Project` 和 <xref:EnvDTE.ProjectItem> 对象中返回的对象中实现 `CodeModel` 或 `FileCodeModel` 接口。 提供此接口中适用于你的项目系统的任何功能。

 如果要添加无法从标准 `CodeModel` 和 `FileCodeModel` 接口中获得的功能，如方法或属性，请创建从标准继承的你自己的接口。 请确保将它与您的项目系统一起记录起来，以便最终用户能够找到它。 返回标准接口，但用户可以调用 `QueryInterface` 方法或强制转换为接口（如果已知存在）。

## <a name="see-also"></a>请参阅
- [自动化模型概述](../../extensibility/internals/automation-model-overview.md)