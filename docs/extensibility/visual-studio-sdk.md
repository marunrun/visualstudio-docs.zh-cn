---
title: 视觉工作室 SDK |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56f772d7d27f11318cdeb0bf365373d5f7c1294b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698079"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
Visual Studio SDK 可帮助您扩展视觉工作室功能或将新功能集成到可视化工作室中。 您可以将扩展分发给其他用户以及可视化工作室应用商店。 以下是一些扩展 Visual Studio 的方式：

- 将命令、按钮、菜单和其他 UI 元素添加到 IDE

- 为新功能添加工具窗口

- 扩展给定语言的 IntelliSense，或为新编程语言提供 IntelliSense

- 使用灯泡提供提示和建议，帮助开发人员编写更好的代码

- 启用对新语言的支持

- 添加自定义项目类型

- 通过可视化工作室市场覆盖数百万开发人员

  如果您以前从未编写过 Visual Studio 扩展，您应该找到有关这些功能的更多信息，并在[开始开发 Visual Studio 扩展](../extensibility/starting-to-develop-visual-studio-extensions.md)。

## <a name="install-the-visual-studio-sdk"></a>安装 Visual Studio SDK
 可视化工作室 SDK 是可视化工作室设置中的可选功能。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="whats-new-in-the-visual-studio-2017-sdk"></a>视觉工作室 2017 SDK 中的新增功能
 Visual Studio SDK 具有一些新功能，如 VSIX v3 格式以及重大更改，这可能需要您更新扩展。 有关详细信息，请参阅[Visual Studio 2017 SDK 中的新增功能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)。

## <a name="visual-studio-user-experience-guidelines"></a>可视化工作室用户体验指南
 在[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中获取为扩展设计 UI 的提示。

 您还可以了解如何通过["地址 DPI 问题](../extensibility/addressing-dpi-issues2.md)"一文在高 DPI 设备上使扩展看起来很棒。

 利用[图像服务和目录](../extensibility/image-service-and-catalog.md)，对高 DPI 和问题进行出色的图像管理和支持。

## <a name="find-and-install-existing-visual-studio-extensions"></a>查找并安装现有的可视化工作室扩展
 您可以在 **"工具**"菜单上的"**扩展和更新**"对话框中找到可视化工作室扩展。 有关详细信息，请参阅[查找和使用可视化工作室扩展](../ide/finding-and-using-visual-studio-extensions.md)。 您还可以在[可视化工作室市场](https://marketplace.visualstudio.com/)中找到扩展

## <a name="visual-studio-sdk-reference"></a>可视化工作室 SDK 参考
 您可以在[可视化工作室 SDK 参考](../extensibility/visual-studio-sdk-reference.md)中找到可视化工作室 SDK API 参考。

## <a name="visual-studio-sdk-samples"></a>可视化工作室 SDK 示例
 您可以在[Visual Studio 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)的 GitHub 上找到 VS SDK 扩展的开源示例。 此 GitHub 存储库包含示例，这些示例说明了 Visual Studio 中的各种可扩展功能。

## <a name="other-visual-studio-sdk-resources"></a>其他可视化工作室 SDK 资源
 如果您对 VSSDK 有疑问，或者想要分享开发扩展的经验，您可以使用[可视化工作室扩展性论坛](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)或[ExtendVS Gitter 聊天室](https://gitter.im/Microsoft/extendvs)。

 您可以在[VSX Arcana 博客](https://blogs.msdn.microsoft.com/vsx/)和 Microsoft MVP 撰写的许多博客中找到更多信息：

- [最喜欢的视觉工作室扩展](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)

- [视觉工作室可扩展性](http://www.visualstudioextensibility.com/overview/vs/)

- [扩展视觉工作室](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>请参阅

- [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)
- [如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [常见问题解答：将加载项转换为 VSPackage 扩展](/visualstudio/extensibility/faq-converting-add-ins-to-vspackage-extensions?view=vs-2015)
- [在托管代码中管理多个线程](../extensibility/managing-multiple-threads-in-managed-code.md)
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [将命令添加到工具栏](../extensibility/adding-commands-to-toolbars.md)
- [扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)
- [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)
- [扩展项目](../extensibility/extending-projects.md)
- [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)
- [创建自定义项目和项目模板](../extensibility/creating-custom-project-and-item-templates.md)
- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)
- [扩展视觉工作室的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [管理 VSPackage](../extensibility/managing-vspackages.md)
- [可视化工作室隔离外壳](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
- [船舶视觉工作室扩展](../extensibility/shipping-visual-studio-extensions.md)
- [深入探究 Visual Studio SDK](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [支持 Visual Studio SDK](../extensibility/support-for-the-visual-studio-sdk.md)
- [可视化工作室 SDK 参考](../extensibility/visual-studio-sdk-reference.md)
