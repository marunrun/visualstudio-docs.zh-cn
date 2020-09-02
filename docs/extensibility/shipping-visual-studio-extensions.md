---
title: 发布 Visual Studio 扩展 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700109"
---
# <a name="shipping-visual-studio-extensions"></a>传送 Visual Studio 扩展
完成扩展开发后，可以将其安装在其他计算机上，与朋友和同事共享，或将其发布到 Visual Studio Marketplace。 在本部分中，我们将介绍需要执行哪些操作才能发布和维护扩展：使用 .vsix 文件、发布、本地化和更新。

## <a name="working-with-vsix-extensions"></a>使用 VSIX 扩展
 您可以通过创建一个空白 VSIX 项目，然后向其添加不同的项模板来创建 VSIX 扩展。 有关详细信息，请参阅 [VSIX 项目模板](../extensibility/vsix-project-template.md)。

 您可以使用 VSIX 格式来打包项目模板、项模板、Vspackage、Managed Extensibility Framework (MEF) 组件、 **工具箱** 控件、程序集和自定义类型 (这包括 Visual Studio 2017) 的自定义起始页。 VSIX 格式使用基于文件的部署。 有关 VSIX 包的详细信息，请参阅 [Vsix 包的解析](../extensibility/anatomy-of-a-vsix-package.md)。

 VSIX 格式不支持安装代码片段。 它也不支持某些其他方案，例如向全局程序集缓存写入 (GAC) 或系统注册表。 如果需要写入 GAC 或安装中的注册表，则必须使用 Windows Installer。 有关详细信息，请参阅 [准备 Windows Installer 部署扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)。

## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>将扩展发布到 Visual Studio Marketplace
 只需通过向用户发送 .vsix 文件或将其放在服务器上，即可将扩展分发给其他人。 但很多人都要将您的代码放在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)上。 Visual Studio Marketplace 扩展可通过 **扩展和更新**提供给 Visual Studio 用户。 有关详细信息，请参阅 [查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。

 有关演示如何将扩展上载到 Visual Studio Marketplace 的完整示例，请参阅 [演练：发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

## <a name="private-galleries"></a>Private Galleries
 开发控件、模板和工具时，可以通过将其发布到 intranet 上的专用库，与组织共享。 有关详细信息，请参阅 [私有库](../extensibility/private-galleries.md)。

## <a name="localizing-your-extension"></a>本地化扩展
 如果打算在不同的区域设置中发布扩展，应考虑对其进行本地化。 有关所涉及内容的说明，请参阅 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="updating-and-versioning-your-extension"></a>更新扩展并对其进行版本控制
 在发布扩展后，需要对其进行更新。 若要了解如何更新已在 Visual Studio Marketplace 上发布的扩展，请参阅 [如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)。

 你可以设置扩展以支持多个版本的 Visual Studio。 有关详细信息，请参阅 [支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)|介绍如何使用 VSIX 项目模板安装自定义项目模板。|
|[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)|描述 VSIX 包的组件。|
|[VSIX 项目模板](../extensibility/vsix-project-template.md)|提供有关如何打包和发布扩展的分步说明。|
|[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)|说明如何使用 vsixlangpack 文件提供安装过程的本地化文本。|
|[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)|介绍如何更新系统上的扩展，以及如何将更新部署到现有的 Visual Studio 扩展。|
|[如何：将依赖项添加到 VSIX 包](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|介绍如何添加对 VSIX 部署包的引用。|
|[准备 Windows Installer 部署的扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|说明如何通过 Windows Installer 部署扩展。|
|[对 VSIX 包进行签名](../extensibility/signing-vsix-packages.md)|说明如何对 VSIX 包进行签名。|
|[Private Galleries](../extensibility/private-galleries.md)|说明如何为扩展创建专用库。|
|[支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|演示如何使你的扩展支持多个版本的 Visual Studio。|
|[查找 Visual Studio](locating-visual-studio.md)|描述如何查找用于自定义扩展部署的 Visual Studio 实例。|
