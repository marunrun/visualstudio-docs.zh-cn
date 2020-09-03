---
title: 支持源代码管理 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 84de3120783528d209b1475477aee5087edac42b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704734"
---
# <a name="supporting-source-control"></a>支持源代码管理
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持项目或编辑器的文件签出、签入和其他源代码管理操作。 作为源代码管理客户端， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 旨在与源代码管理包交互，如 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ，后者为动态定义的文件集提供存档、版本控制和控制功能。

## <a name="in-this-section"></a>本节内容
- [源代码管理包的模型](../../extensibility/internals/model-for-source-control-packages.md)

 描述项目类型为支持源代码管理而必须实现的接口。

- [设计决策](../../extensibility/internals/source-control-design-decisions.md)

 提供其答案更改了项目类型实现方式的问题。

- [配置详细信息](../../extensibility/internals/source-control-configuration-details.md)

 描述支持源控件如何更改项目类型的实现。

- [项目和编辑器的其他指南](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)

 讨论项目类型和编辑器的最佳实践。

- [运行时详细信息](../../extensibility/internals/source-control-runtime-details.md)

 描述如何在用户将项目添加到源代码管理系统时注册项目。

## <a name="reference"></a>参考
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 向环境或源代码管理包指示要在内存中更改或保存文件。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 允许项目和层次结构自行向源代码管理注册，并获取有关源代码管理状态的信息。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 在项目系统中实现，以提供项目文件和项目项的源代码管理。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 由项目用于查询环境，以获得在解决方案中添加、删除或重命名文件或目录的权限。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 通知客户端对项目文件或目录所做的更改。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 提供项目概述，作为集成开发环境的基本构建基块 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (IDE) 。 向说明项目如何控制生成和编译代码的其他主题提供了链接。
