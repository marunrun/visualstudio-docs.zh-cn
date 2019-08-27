---
title: 支持源代码管理 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b4f12790de00cc835f7268830bf6d9a4734b839
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331244"
---
# <a name="supporting-source-control"></a>支持源代码管理
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持文件签出、 签入和你的项目或编辑器的其他源代码管理操作。 作为源控制客户端[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]旨在与源代码管理包，如交互[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]，后者提供存档、 版本控制和一组动态定义的文件的控件功能。

## <a name="in-this-section"></a>本节内容
- [源代码管理包的模型](../../extensibility/internals/model-for-source-control-packages.md)

 描述一种项目类型必须实现的接口以支持源控件。

- [设计决策](../../extensibility/internals/source-control-design-decisions.md)

 提供的问题答案更改如何实现一种项目类型。

- [配置详细信息](../../extensibility/internals/source-control-configuration-details.md)

 描述如何支持源代码管理更改的项目类型的实现。

- [项目和编辑器的其他指南](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)

 讨论项目类型和编辑器的最佳实践。

- [运行时详细信息](../../extensibility/internals/source-control-runtime-details.md)

 描述如何注册一个项目，当用户将其添加到源代码管理系统。

## <a name="reference"></a>参考
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 指示对环境或一个文件是要在内存中更改或已保存的源代码管理包。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 允许项目和层次结构，以与源控件自行注册并获取有关源代码管理状态信息。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 在为项目文件和项目项提供源代码管理的项目系统中实现。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 使用项目来查询用于添加、 删除或重命名文件或在解决方案中的目录的权限的环境。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 通知客户端的对项目文件或目录所做的更改。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 基本构建块的形式提供的项目概述[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE)。 提供了指向介绍项目生成和编译代码的控制的其他主题的链接。