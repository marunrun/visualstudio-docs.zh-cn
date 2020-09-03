---
title: Windows Installer 安装 Vspackage |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687470"
---
# <a name="installing-vspackages-with-windows-installer"></a>使用 Windows Installer 安装 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将 VSPackage 集成到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 只需将文件复制到用户的计算机。 VSPackage 的安装程序必须安装 VSPackage 及其依赖文件，并将其注册并集成到中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 你的 VSPackage 可以利用集成功能，如在 "初始屏幕" 和 "关于" 对话框中显示图标 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 Microsoft Windows Installer 文件是分发 Vspackage 的建议方法。 易于使用的 Windows Installer 包可在支持的任何 Windows 操作系统上运行 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 有关详细信息，请参阅 [Windows Installer](https://msdn.microsoft.com/121be21b-b916-43e2-8f10-8b080516d2a0)。  
  
## <a name="in-this-section"></a>本节内容  
 [Windows Installer 基本知识](../../extensibility/internals/windows-installer-basics.md)  
 提供 Windows Installer 的概述。  
  
 [VSPackage 安装方案](../../extensibility/internals/vspackage-setup-scenarios.md)  
 讨论了不同的方法，可同时支持 Vspackage 和的并行安装 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [创作 Windows Installer 程序包](../../extensibility/internals/authoring-a-windows-installer-package.md)  
 概述安装程序正确安装并将 Vspackage 集成到的典型步骤 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)  
 介绍安装程序如何检测 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 及其组件，并在不满足 VSPackage 要求时取消安装。  
  
 [组件管理](../../extensibility/internals/component-management.md)  
 讨论如何开发将维护以前产品版本的完整性的安装程序。  
  
 [为 VSPackage 选择安装目录](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)  
 概述用于查找 Vspackage 的选项。  
  
 [VSPackage 注册](../../extensibility/internals/vspackage-registration.md)  
 讨论了如何在安装时注册 Vspackage，以及为什么自我注册是一项糟糕的事情。  
  
 [部署项目类型](../../extensibility/internals/deploying-project-types.md)  
 讨论如何使用托管代码项目类型的新项目类型聚合器。  
  
 [如何：生成安装程序的注册表信息](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)  
 介绍如何使用 RegPkg.exe 为托管 VSPackage 生成注册清单。  
  
 [安装后必须运行的命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md)  
 说明如何运行安装后命令，以便将 Vspackage 集成到中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [使用 Windows Installer 卸载 VSPackage](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)  
 介绍用户在卸载 VSPackage 时必须执行的步骤。  
  
## <a name="related-sections"></a>相关章节  
 [安装 VSPackage](../../misc/installing-vspackages.md)  
 讨论如何生成和安装 Vspackage 以及如何支持同时运行多个版本的的用户 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。
