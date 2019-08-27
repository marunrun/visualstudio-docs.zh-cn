---
title: VSPackage State | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- state, VSPackages
- VSPackages, managing application state
- state persistence
ms.assetid: 6056a9ea-e7a8-481c-9fc8-340229fa12d9
caps.latest.revision: 25
manager: jillfra
ms.openlocfilehash: f3140b527673f87b1d7c552e99584232494aed7f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979990"
---
# <a name="vspackage-state"></a>VSPackage 状态
许多因素的确定组持久的值或状态，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]应用程序。  
  
- 项目具有项目和配置属性。  
  
- 解决方案具有的属性。  
  
- 用户设置确定的大小和位置的文档窗口中，工具窗口、 停靠状态和键盘快捷方式。  
  
- 应用程序可以具有用户设置的选项。  
  
- 应用程序创建的对象可以具有其自己的属性。  
  
  以下是几种的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]可以管理应用程序状态：  
  
- 通过项目和解决方案属性页。  
  
- 通过**导入和导出设置向导**，这使用户能够将设置从一台计算机移动到另一个。  
  
- 通过**选项**对话框，其中包含与应用程序相关的选项。  
  
- 通过**属性**窗口，其中显示对象的属性。  
  
- 通过自动化。 应用程序可以访问已公开为自动化的 VSPackage 和对象属性。  
  
  基础应用程序状态是启用要进行保存和还原的应用程序状态的各种持久性机制。  
  
## <a name="in-this-section"></a>本节内容  
 [状态持久性支持](../misc/support-for-state-persistence.md)  
 列出保存、恢复和重置 VSPackage 状态的常见策略。  
  
 [选项和选项页](../extensibility/internals/options-and-options-pages.md)  
 介绍常规和自定义选项页，并介绍了如何实现它们。  
  
 [创建选项页](../extensibility/creating-an-options-page.md)  
 说明如何创建两个选项页面、 一个简单的页面和自定义页。  
  
 [支持设置类别](../misc/support-for-settings-categories.md)  
 讨论用户设置和它们的创建和保存。  
  
 [创建设置类别](../extensibility/creating-a-settings-category.md)  
 说明如何创建[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]设置类别，并使用它来保存到的值和从设置文件还原的值。  
  
 [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)  
 说明如何显示和更改的值中的对象**属性**窗口。  
  
 [在属性窗口中公开属性](../extensibility/exposing-properties-to-the-properties-window.md)  
 介绍如何将对象的公共属性公开**属性**窗口。  
  
 [支持项目和配置属性](../extensibility/internals/support-for-project-and-configuration-properties.md)  
 说明如何显示和更改项目和配置属性。  
  
 [获取项目属性](../extensibility/getting-project-properties.md)  
 指导您完成创建托管的 VSPackage 的工具窗口中显示项目属性的步骤。  
  
 [使用设置存储](../extensibility/using-the-settings-store.md)  
 说明设置存储持久性机制以及如何使用它。  
  
## <a name="related-sections"></a>相关章节  
 [VSPackage](../extensibility/internals/vspackages.md)  
 提供了一个，这些主题介绍如何创建和使用 Vspackage 的常规指导。