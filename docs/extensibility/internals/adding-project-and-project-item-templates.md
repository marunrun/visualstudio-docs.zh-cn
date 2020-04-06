---
title: 添加项目和项目项目模板 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 14eb1a9e2e63fa6e63d3ba2efa4426421e6b5593
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710198"
---
# <a name="add-project-and-project-item-templates"></a>添加项目和项目项目模板
创建自己的项目类型时，必须使用标准[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 对话框支持添加新项目和项目项。 以下主题讨论添加项目和项目项的不同技术。

## <a name="in-this-section"></a>在本节中
- [项目上下文](../../extensibility/internals/project-context.md)

 说明项目提供了环境中发生的情况的大部分上下文信息。

- [项目优先级](../../extensibility/internals/project-priority.md)

 说明项目项通常是一个项目的成员，以帮助避免有关用于打开项目的项目的歧义。

- [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)

 提供有关可用于在项目中打开文件的两种类型的编辑器以及项目在确定打开项目项时要使用的编辑器所扮演的角色的信息。

- [注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)

 解释创建[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目时发生的情况。

- [将项目添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 解释向"**添加新项目"** 对话框中添加项的过程。

- [将目录添加到"新项目"对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 提供了注册包含 VSPackage 提供的自定义模板的新目录的示例。

- [将目录添加到"添加新项目"对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 提供了为 **"添加新项目"** 对话框注册一组新目录的示例。

- [用于扩展项目系统的 IDE 定义命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 列出用于扩展项目系统的不同类型的命令项。

- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 列出用于扩展[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]的对象[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]的 CATID 和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目系统。

## <a name="related-sections"></a>相关章节
- [如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供用于打开与项目的特定编辑器绑定的项的分步说明。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供打开标准编辑器的分步说明。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型概念主题的链接。 项目子类型扩展现有[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目。

- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题的链接，这些主题提供有关如何设计新项目类型的信息。
