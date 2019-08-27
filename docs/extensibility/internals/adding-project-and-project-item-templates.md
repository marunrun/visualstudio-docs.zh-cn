---
title: 添加项目和项目项模板 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 38ab7a0a14c5a4e832aec330852546b64a41fd0c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315851"
---
# <a name="add-project-and-project-item-templates"></a>添加项目和项目项模板
创建你自己的项目类型时，你必须通过使用标准添加新项目和项目项提供支持[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 对话框。 以下主题讨论不同的技术来添加项目和项目项。

## <a name="in-this-section"></a>本节内容
- [项目上下文](../../extensibility/internals/project-context.md)

 介绍了该项目提供了大部分什么怎样在环境中的上下文信息。

- [项目优先级](../../extensibility/internals/project-priority.md)

 介绍了项目项通常是一个项目的成员，以帮助避免的多义性有关哪些项目用于打开该项目。

- [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)

 提供有关两种类型的编辑器，可用于打开一个项目和角色中的文件中确定哪个编辑器打开项目项时要使用播放该项目的信息。

- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)

 介绍了所发生的情况时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]创建项目。

- [将项目添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 解释了将项添加到的过程**添加新项**对话框。

- [将目录添加到新项目对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 提供注册包含由 VSPackage 提供的自定义模板的新目录的示例。

- [将目录添加到添加新项对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 提供了一组新的目录中注册示例**添加新项**对话框。

- [IDE 定义用于扩展项目系统的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 列出了不同类型的命令项用于扩展项目系统。

- [对象通常用于扩展项目的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 列出用于扩展的对象的 Catid [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]， [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]，和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目系统。

## <a name="related-sections"></a>相关章节
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供用于打开本质上绑定到特定的编辑器项目的项的分步说明。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供用于打开标准编辑器的分步说明。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型概念主题的链接。 项目子类型扩展现有[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目。

- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题提供有关如何设计新的项目类型的信息。