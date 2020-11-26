---
title: 添加项目和项目项模板 |Microsoft Docs
description: 了解如何将项目和项目项模板添加到 Visual Studio 集成开发环境中的对话框 (IDE) 。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 1e97b04294f0545c378210d39f343f3b009b6d15
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190169"
---
# <a name="add-project-and-project-item-templates"></a>添加项目和项目项模板
创建自己的项目类型时，必须通过使用标准 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境 (IDE) "对话框提供对添加新项目和项目项的支持。 以下主题介绍添加项目和项目项的不同方法。

## <a name="in-this-section"></a>在本节中
- [项目上下文](../../extensibility/internals/project-context.md)

 说明项目为环境中的发生提供了大部分上下文信息。

- [项目优先级](../../extensibility/internals/project-priority.md)

 说明项目项通常是一个项目的成员，有助于避免用于打开该项的项目的歧义。

- [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)

 提供有关两种类型的编辑器的信息，可用于打开项目中的文件和项目在确定项目项打开时使用的编辑器的角色。

- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)

 说明创建项目时发生的情况 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 说明将项添加到 " **添加新项** " 对话框的过程。

- [将目录添加到 "新建项目" 对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 提供注册新目录的示例，该目录包含 VSPackage 提供的自定义模板。

- [将目录添加到 "添加新项" 对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 提供一个为 " **添加新项** " 对话框注册一组新目录的示例。

- [IDE 定义的用于扩展项目系统的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 列出用于扩展项目系统的不同类型的命令项。

- [通常用于扩展项目的对象的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 列出用于扩展 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和项目系统的对象的 catid [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。

## <a name="related-sections"></a>相关章节
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供有关打开与项目的特定编辑器绑定的项的分步说明。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供打开标准编辑器的分步说明。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型概念性主题的链接。 项目子类型扩展现有 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目。

- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题的链接，这些主题提供有关如何设计新的项目类型的信息。
