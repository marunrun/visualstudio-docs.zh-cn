---
title: 扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c7154395be43f6a0b07e9f2557d94fa594ef5ba4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150793"
---
# <a name="shipping-visual-studio-extensions"></a>传送 Visual Studio 扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**说明**：Visual Studio 库即将被 Visual Studio Marketplace。 请参阅本主题的详细信息的最新版本。

完成开发您的扩展插件后，可以在其他计算机上安装、 共享与朋友和同事，或将其发布在 Visual Studio 库上。 在本部分中，我们介绍需要执行的操作将发布和维护您的扩展插件的所有操作： 使用.vsix 文件，发布、 本地化，和更新。

## <a name="working-with-vsix-extensions"></a>使用 VSIX 扩展
 创建一个空白的 VSIX 项目，然后将不同的项模板添加到它，可以创建 VSIX 扩展。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

 VSIX 格式可用于包项目模板、 项模板、 Vspackage、 Managed Extensibility Framework (MEF) 组件**工具箱**控件、 组件和自定义类型 （这包括自定义起始页）。 VSIX 格式使用基于文件的部署。 有关 VSIX 包的详细信息，请参阅[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)。

 VSIX 格式不支持代码段的安装。 它还不支持某些其他方案，如写入到全局程序集缓存 (GAC) 或系统注册表。 如果需要将写入到 gac 中或在安装中的注册表，则必须使用 Windows 安装程序。 有关详细信息，请参阅[准备扩展的 Windows Installer 部署](../extensibility/preparing-extensions-for-windows-installer-deployment.md)。

## <a name="publishing-your-extension-to-the-visual-studio-gallery"></a>将你的扩展发布到 Visual Studio 库
 您可以只需通过的用户邮寄贴.vsix 文件或在服务器上将放在分发给其他人扩展。 但若要获取你的代码中的很多人的手中的最佳方式是将其放入[Visual Studio Marketplace](https://marketplace.visualstudio.com/)。 可以使用 Visual Studio 用户可通过 visual Studio 库扩展**扩展和更新**。 有关详细信息，请参阅[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。

 有关演示如何将扩展上传到 Visual Studio 库的完整示例，请参阅[演练：发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

## <a name="private-galleries"></a>Private Galleries
 在开发控件、 模板和工具，您可以将它们发布到您的 intranet 上的专用库与组织共享它们。 有关详细信息，请参阅[专用库](../extensibility/private-galleries.md)。

## <a name="localizing-your-extension"></a>本地化您的扩展插件
 如果您打算发布你的扩展在不同的区域设置中，则应考虑对其进行本地化。 有关所涉及的内容的说明，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="updating-and-versioning-your-extension"></a>更新和版本控制您的扩展插件
 发布你的扩展后，会需要进行更新的时间。 若要了解如何更新已发布在 Visual Studio 库的扩展，请参阅[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)。

 您可以设置您的扩展支持的 Visual Studio 的多个版本。 有关详细信息，请参阅[支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)|介绍如何使用 VSIX 项目模板来安装自定义项目模板。|
|[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)|介绍了 VSIX 包的组件。|
|[VSIX 项目模板](../extensibility/vsix-project-template.md)|提供有关如何打包和发布扩展的分步说明。|
|[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)|介绍如何使用 extension.vsixlangpack 文件为安装过程中提供本地化的文本。|
|[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)|介绍如何更新您的系统上的某个扩展以及如何将更新部署到现有的 Visual Studio 扩展。|
|[如何：将依赖项添加到 VSIX 包](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|介绍如何将引用添加到 VSIX 部署包。|
|[准备 Windows Installer 部署的扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|介绍如何部署与 Windows 安装程序扩展插件。|
|[对 VSIX 包进行签名](../extensibility/signing-vsix-packages.md)|介绍如何进行签名 VSIX 包。|
|[专用库](../extensibility/private-galleries.md)|说明如何创建扩展的专用库。|
|[支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|介绍如何配置你的扩展插件支持多个版本的 Visual Studio。|
