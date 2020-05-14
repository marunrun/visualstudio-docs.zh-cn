---
title: 运输视觉工作室扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 767bb24bb5cb47f1af1452aa04ebdc91c778e284
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700109"
---
# <a name="shipping-visual-studio-extensions"></a>传送 Visual Studio 扩展
开发完扩展后，可以在其他计算机上安装它，与朋友和同事共享它，或在可视化工作室应用商店上发布。 在本节中，我们将解释发布和维护扩展程序所需的所有操作：使用 .vsix 文件、发布、本地化和更新。

## <a name="working-with-vsix-extensions"></a>使用 VSIX 扩展
 您可以通过创建空白 VSIX 项目，然后向其中添加不同的项目模板来创建 VSIX 扩展。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

 您可以使用 VSIX 格式打包项目模板、项目模板、VSPackage、托管扩展框架 （MEF） 组件、**工具箱**控件、程序集和自定义类型（这包括 Visual Studio 2017 的自定义起始页）。 VSIX 格式使用基于文件的部署。 有关 VSIX 包的详细信息，请参阅[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)。

 VSIX 格式不支持代码段的安装。 它还不支持某些其他方案，如写入全局程序集缓存 （GAC） 或系统注册表。 如果需要在安装中写入 GAC 或注册表，则必须使用 Windows 安装程序。 有关详细信息，请参阅为[Windows 安装程序部署准备扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)。

## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>将扩展发布到可视化工作室市场
 只需将 .vsix 文件邮寄到其他人或放入服务器，即可将扩展分发给其他人。 但是，让你的代码在很多人手中的最好方法是把它放到[视觉工作室市场](https://marketplace.visualstudio.com/vs)。 视觉工作室市场扩展可以通过**扩展和更新**提供给视觉工作室用户。 有关详细信息，请参阅[查找和使用可视化工作室扩展](../ide/finding-and-using-visual-studio-extensions.md)。

 有关演示如何将扩展上载到可视化工作室市场的完整示例，请参阅[演练：发布可视化工作室扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

## <a name="private-galleries"></a>Private Galleries
 在开发控件、模板和工具时，可以通过将它们发布到 Intranet 上的专用库来与组织共享它们。 有关详细信息，请参阅[私人画廊](../extensibility/private-galleries.md)。

## <a name="localizing-your-extension"></a>本地化扩展
 如果您计划在不同区域设置中发布扩展，则应考虑本地化它。 有关相关内容的说明，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="updating-and-versioning-your-extension"></a>更新和版本控制扩展
 发布扩展后，总有一段时间需要更新它。 要了解如何更新已在可视化工作室应用商店上发布的扩展，请参阅[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)。

 您可以将扩展设置为支持多个版本的 Visual Studio。 有关详细信息，请参阅[支持可视化工作室的多个版本](../extensibility/supporting-multiple-versions-of-visual-studio.md)。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)|说明如何使用 VSIX 项目模板安装自定义项目模板。|
|[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)|描述 VSIX 包的组件。|
|[VSIX 项目模板](../extensibility/vsix-project-template.md)|提供有关如何打包和发布扩展的分步说明。|
|[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)|说明如何使用扩展.vsixlangpack 文件为安装过程提供本地化文本。|
|[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)|介绍如何更新系统上的扩展以及如何将更新部署到现有的 Visual Studio 扩展。|
|[如何：将依赖项添加到 VSIX 包](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|描述如何添加对 VSIX 部署包的引用。|
|[准备 Windows Installer 部署的扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|说明如何使用 Windows 安装程序部署扩展。|
|[对 VSIX 包进行签名](../extensibility/signing-vsix-packages.md)|说明如何对 VSIX 包进行签名。|
|[Private Galleries](../extensibility/private-galleries.md)|说明如何为扩展创建专用库。|
|[支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|演示如何让扩展支持多个版本的 Visual Studio。|
|[查找 Visual Studio](locating-visual-studio.md)|介绍如何查找用于自定义扩展部署的可视化工作室实例。|
