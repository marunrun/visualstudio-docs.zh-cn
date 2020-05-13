---
title: 提供代码自动化 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bd13b7db2065069ff1540dbfc921570c2b230b8a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705995"
---
# <a name="providing-automation-for-code"></a>提供适用于 Code 的自动化
不需要为代码创建自动化模型。 环境 SDK 不提供执行此操作的示例。 有关代码模型的见解，请参阅对象<xref:EnvDTE.CodeModel>。

 要实现代码模型，必须实现由内部数据结构确定的任何接口。 对象必须派生自类`IDispatch`。

 扩展<xref:EnvDTE.CodeModel>的对象 和<xref:EnvDTE.FileCodeModel>可从 对象<xref:EnvDTE.Project>获得，如下所示：

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 `CodeModel`您可以选择仅实现从`FileCodeModel``Project`和<xref:EnvDTE.ProjectItem>对象返回的对象中的 或 接口。 提供适合项目系统的任何接口功能。

 如果要添加标准和`CodeModel``FileCodeModel`接口中不可用的功能（如方法或属性），请创建从标准继承自己的接口。 请务必使用项目系统进行文档记录，以便最终用户知道查找它。 返回标准接口，但用户可以调用`QueryInterface`方法或强制转换到您的接口（如果已知存在）。

## <a name="see-also"></a>请参阅
- [自动化模型概述](../../extensibility/internals/automation-model-overview.md)
