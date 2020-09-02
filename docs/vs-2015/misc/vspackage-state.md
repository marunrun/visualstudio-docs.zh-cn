---
title: VSPackage 状态 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62979990"
---
# <a name="vspackage-state"></a>VSPackage 状态
许多因素决定了应用程序的持久值集或状态 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
- 项目具有项目和配置属性。  
  
- 解决方案具有属性。  
  
- 用户设置确定文档窗口、工具窗口、停靠状态和键盘快捷方式的大小和位置。  
  
- 应用程序可以包含用户设置的选项。  
  
- 应用程序创建的对象可以具有其自己的属性。  
  
  下面是一些 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 可管理应用程序状态的方法：  
  
- 通过项目和解决方案属性页。  
  
- 通过 **导入和导出设置向导**，用户可以将设置从一台计算机移动到另一台计算机。  
  
- 通过 " **选项** " 对话框，其中包含与应用程序相关的选项。  
  
- " **属性** " 窗口，用于显示对象的属性。  
  
- 通过自动化。 应用程序可以访问已向自动化公开的 VSPackage 和对象属性。  
  
  基本应用程序状态是各种持久性机制，它们允许保存和还原应用程序状态。  
  
## <a name="in-this-section"></a>本节内容  
 [状态持久性支持](../misc/support-for-state-persistence.md)  
 列出保存、恢复和重置 VSPackage 状态的常见策略。  
  
 [选项和选项页](../extensibility/internals/options-and-options-pages.md)  
 介绍了 "常规" 和 "自定义" 选项页，并说明了如何实现它们。  
  
 [创建选项页](../extensibility/creating-an-options-page.md)  
 说明如何创建两个选项页：一个简单的页和一个自定义页。  
  
 [支持设置类别](../misc/support-for-settings-categories.md)  
 讨论用户设置以及如何创建和保存这些设置。  
  
 [创建设置类别](../extensibility/creating-a-settings-category.md)  
 说明如何创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 设置类别并使用它将值保存到设置和从设置文件还原值。  
  
 [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)  
 说明如何在 " **属性** " 窗口中显示和更改对象的值。  
  
 [在属性窗口中公开属性](../extensibility/exposing-properties-to-the-properties-window.md)  
 说明如何向 " **属性** " 窗口公开对象的公共属性。  
  
 [支持项目和配置属性](../extensibility/internals/support-for-project-and-configuration-properties.md)  
 介绍如何显示和更改项目和配置属性。  
  
 [获取项目属性](../extensibility/getting-project-properties.md)  
 指导您完成创建在工具窗口中显示项目属性的托管 VSPackage 的步骤。  
  
 [使用设置存储](../extensibility/using-the-settings-store.md)  
 介绍设置存储持久性机制以及如何使用它。  
  
## <a name="related-sections"></a>相关章节  
 [VSPackages](../extensibility/internals/vspackages.md)  
 提供介绍如何创建和使用 Vspackage 的主题的一般方向。