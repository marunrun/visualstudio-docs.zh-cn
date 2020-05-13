---
title: 使用 Windows 安装程序安装 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], with Windows Installer
- VSPackages, deploying
ms.assetid: 41d2c72c-0a97-4fcd-b3aa-33a8d3aa962a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2eb90dbffa9f04cd17afa70d2bdfc59205bc99cb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707465"
---
# <a name="installing-vspackages-with-windows-installer"></a>使用 Windows Installer 安装 VSPackage
将 VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成到其中不仅需要将文件复制到用户的计算机。 VSPackage 的安装程序必须安装 VSPackage 及其相关文件，并注册它们并将其集成到 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 您的 VSPackage 可以利用集成功能，例如在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]初始屏幕上显示图标和"关于"对话框。

 Microsoft Windows 安装程序文件是分发 VS 包的推荐方式。 易于使用的 Windows 安装程序包可以在 支持[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的任何 Windows 操作系统上运行。 有关详细信息，请参阅[Windows 安装程序](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)。

## <a name="in-this-section"></a>本节内容
- [Windows Installer 基本知识](../../extensibility/internals/windows-installer-basics.md)

 提供 Windows 安装程序的概述。

- [VSPackage 安装方案](../../extensibility/internals/vspackage-setup-scenarios.md)

 讨论支持并行安装 VS 包和[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的不同方法。

- [创作 Windows Installer 程序包](../../extensibility/internals/authoring-a-windows-installer-package.md)

 概述了安装程序为正确安装 VS 包并将其集成到 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]所遵循的典型步骤。

- [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)

 描述安装程序如何检测[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]其组件，并在不符合 VSPackage 要求时取消设置。

- [组件管理](../../extensibility/internals/component-management.md)

 讨论如何开发一个安装程序，将保持以前产品版本的完整性。

- [为 VSPackage 选择安装目录](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)

 总结了查找 VSPackages 的选项。

- [VSPackage 注册](../../extensibility/internals/vspackage-registration.md)

 讨论如何在安装时注册 VSPackages，以及为什么自注册是一个坏主意。

- [部署项目类型](../../extensibility/internals/deploying-project-types.md)

 讨论如何将新的项目类型聚合器用于托管代码项目类型。

- [如何：生成安装程序的注册表信息](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)

 说明如何使用 RegPkg.exe 为托管 VSPackage 生成注册清单。

- [安装后必须运行的命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md)

 说明如何运行安装后命令以将 VS 包集成到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中。

- [使用 Windows Installer 卸载 VSPackage](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)

 描述用户卸载您的 VSPackage 时安装程序必须执行的步骤。
