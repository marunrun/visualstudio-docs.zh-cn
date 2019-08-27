---
title: 添加项目和项目项模板 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b68c9f4bbaed73603c46fc0beab77a308b8933d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203855"
---
# <a name="adding-project-and-project-item-templates"></a>添加项目和项目项模板
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建你自己的项目类型时，你必须通过使用标准添加新项目和项目项提供支持[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成开发环境 (IDE) 对话框。 以下主题讨论不同的技术来添加项目和项目项。  
  
## <a name="in-this-section"></a>本节内容  
 [项目上下文](../../extensibility/internals/project-context.md)  
 介绍了该项目提供了大部分什么怎样在环境中的上下文信息。  
  
 [项目优先级](../../extensibility/internals/project-priority.md)  
 介绍了项目项通常是一个项目的成员，以帮助避免的多义性有关哪些项目用于打开该项目。  
  
 [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)  
 提供有关两种类型的编辑器，可用于打开一个项目和角色中的文件中确定哪个编辑器打开项目项时要使用播放该项目的信息。  
  
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)  
 介绍了所发生的情况时[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]创建项目。  
  
 [将项添加到“添加新项”对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)  
 解释了将项添加到的过程**添加新项**对话框。  
  
 [将目录添加到“新建项目”对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)  
 提供注册包含由 VSPackage 提供的自定义模板的新目录的示例。  
  
 [将目录添加到“添加新项”对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)  
 提供了一组新的目录中注册示例**添加新项**对话框。  
  
 [用于扩展项目系统的 IDE 定义的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)  
 列出了不同类型的命令项用于扩展项目系统。  
  
 [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)  
 列出用于扩展的对象的 Catid [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]， [!INCLUDE[csprcs](../../includes/csprcs-md.md)]，和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目系统。  
  
## <a name="related-sections"></a>相关章节  
 [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)  
 提供用于打开本质上绑定到特定的编辑器项目的项的分步说明。  
  
 [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)  
 提供用于打开标准编辑器的分步说明。  
  
 [项目子类型](../../extensibility/internals/project-subtypes.md)  
 提供指向项目子类型概念主题的链接。 项目子类型扩展现有[!INCLUDE[csprcs](../../includes/csprcs-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目。  
  
 [项目类型](../../extensibility/internals/project-types.md)  
 提供指向其他主题提供有关如何设计新的项目类型的信息。
