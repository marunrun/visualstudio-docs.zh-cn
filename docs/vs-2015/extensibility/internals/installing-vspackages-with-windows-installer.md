---
title: 使用 Windows Installer 安装 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], with Windows Installer
- VSPackages, deploying
ms.assetid: 41d2c72c-0a97-4fcd-b3aa-33a8d3aa962a
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 35942f6babf18967e11f268ef0412acb4cc8edf7
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687470"
---
# <a name="installing-vspackages-with-windows-installer"></a>使用 Windows Installer 安装 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将集成到你的 VSPackage[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]需要不止将文件复制到用户的计算机。 你的 VSPackage 的安装程序必须安装 VSPackage 和其依赖的文件，并注册并将它们到集成[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 你的 VSPackage 可以利用集成功能，例如上显示一个图标[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]初始屏幕和关于对话框。  
  
 Microsoft Windows Installer 文件是将你的 Vspackage 的推荐的方法。 易于使用 Windows Installer 程序包可以在支持的任何 Windows 操作系统上运行[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 有关详细信息，请参阅[Windows 安装程序](https://msdn.microsoft.com/121be21b-b916-43e2-8f10-8b080516d2a0)。  
  
## <a name="in-this-section"></a>本节内容  
 [Windows Installer 基本知识](../../extensibility/internals/windows-installer-basics.md)  
 概述 Windows 安装程序。  
  
 [VSPackage 安装方案](../../extensibility/internals/vspackage-setup-scenarios.md)  
 讨论可支持你的 Vspackage 的通过并行安装不同的方式和[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 [创作 Windows Installer 程序包](../../extensibility/internals/authoring-a-windows-installer-package.md)  
 提供的安装程序遵循正确安装并集成到 Vspackage 的典型步骤概述[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)  
 介绍如何安装程序可以检测[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]和其组件和取消设置如果未满足 VSPackage 要求。  
  
 [组件管理](../../extensibility/internals/component-management.md)  
 讨论如何开发的安装程序将保持以前的产品版本的完整性。  
  
 [为 VSPackage 选择安装目录](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)  
 总结了用于查找 Vspackage 的选项。  
  
 [VSPackage 注册](../../extensibility/internals/vspackage-registration.md)  
 讨论如何在安装时注册 Vspackage 并自动注册的原因是个好主意。  
  
 [部署项目类型](../../extensibility/internals/deploying-project-types.md)  
 讨论如何为托管代码的项目类型使用新的项目类型聚合器。  
  
 [如何：生成安装程序的注册表信息](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)  
 介绍如何使用 RegPkg.exe 生成托管的 VSPackage 注册清单。  
  
 [安装后必须运行的命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md)  
 说明如何运行安装后命令集成到 Vspackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 [使用 Windows Installer 卸载 VSPackage](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)  
 介绍您的安装程序时用户卸载你的 VSPackage 必须执行的步骤。  
  
## <a name="related-sections"></a>相关章节  
 [安装 VSPackage](../../misc/installing-vspackages.md)  
 讨论如何生成和安装 Vspackage 以及如何支持运行多个版本的用户的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]在同一时间。
