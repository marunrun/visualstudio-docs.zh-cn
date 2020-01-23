---
title: Visual Studio SDK |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
caps.latest.revision: 57
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 27dce16d9fe02063eae935af96c26184285e583d
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850368"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio SDK 可帮助你扩展 Visual Studio 的功能，或将新功能集成到 Visual Studio 中。 可以将扩展分发给其他用户以及 Visual Studio 库。 以下是一些扩展 Visual Studio 的方式：  
  
- 向 IDE 添加命令、按钮、菜单和其他 UI 元素  
  
- 添加工具窗口以实现新功能  
  
- 扩展给定语言的 IntelliSense，或为新的编程语言提供 IntelliSense  
  
- 使用轻型电灯泡提供帮助开发人员编写更好代码的提示和建议  
  
- 启用新语言支持  
  
- 添加自定义项目类型  
  
- 通过 Visual Studio Marketplace 与数百万个开发人员联系  
  
  如果你之前从未编写过 Visual Studio 扩展，则应在[开始开发 Visual Studio 扩展](../extensibility/starting-to-develop-visual-studio-extensions.md)时找到有关这些功能的详细信息。  
  
## <a name="installing-the-visual-studio-sdk"></a>安装 Visual Studio SDK  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="whats-new-in-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK 的新增功能  
 Visual Studio SDK 具有一些新功能，包括轻型电灯泡和新的项目项，它们允许你使用 VSIX 包创建菜单命令、工具窗口和编辑器扩展。 有关详细信息，请参阅[Visual Studio 2015 SDK 的新增功能](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md)。  
  
## <a name="visual-studio-user-experience-guidelines"></a>Visual Studio 用户体验指南  
 获取有关在[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中设计扩展 UI 的极佳技巧。  
  
 你还可以了解如何通过我们的[解决 DPI 问题](../extensibility/addressing-dpi-issues2.md)主题，使你的扩展在高 DPI 设备上看起来很好。  
  
 利用[映像服务和目录](../extensibility/image-service-and-catalog.md)获得极佳的图像管理，并提供高 DPI 和主题的支持。  
  
## <a name="finding-and-installing-existing-visual-studio-extensions"></a>查找和安装现有的 Visual Studio 扩展  
 可以在 "**工具**" 菜单上的 "**扩展和更新**" 对话框中找到 Visual Studio 扩展。 有关详细信息，请参阅[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。 你还可以在[Visual Studio Marketplace](https://marketplace.visualstudio.com/)中找到扩展  
  
## <a name="visual-studio-sdk-reference"></a>Visual Studio SDK 引用  
 可在[Visual STUDIO Sdk 参考](../extensibility/visual-studio-sdk-reference.md)中找到 VISUAL STUDIO sdk API 参考。  
  
## <a name="visual-studio-sdk-samples"></a>Visual Studio SDK 示例  
 可在 GitHub 上的[Visual Studio 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)中找到 VS SDK 扩展的开源示例。 此 GitHub 存储库包含说明 Visual Studio 中各种可扩展功能的示例。  
  
## <a name="other-visual-studio-sdk-resources"></a>其他 Visual Studio SDK 资源  
 如果对 VSSDK 有疑问或想要分享开发扩展的经验，可以使用[Visual Studio 扩展性论坛](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)或[ExtendVS 组聊天](https://gitter.im/Microsoft/extendvs)。  
  
 可以在[VSX Arcana 博客](https://blogs.msdn.microsoft.com/vsx/)和 Microsoft mvp 编写的多个博客中找到详细信息：  
  
- [最喜爱的 Visual Studio 扩展](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)  
  
- [Visual Studio 扩展性](http://www.visualstudioextensibility.com/overview/vs/)  
  
- [扩展 Visual Studio](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)  
  
## <a name="see-also"></a>请参阅  
 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)   
 [如何：将扩展性项目迁移到 Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md)   
 [常见问题解答：将外接程序转换为 VSPackage 扩展](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md)   
 [在托管代码中管理多个线程](../extensibility/managing-multiple-threads-in-managed-code.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)   
 [将命令添加到工具栏](../extensibility/adding-commands-to-toolbars.md)   
 [扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)   
 [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)   
 [扩展项目](../extensibility/extending-projects.md)   
 [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)   
 [创建自定义项目和项模板](../extensibility/creating-custom-project-and-item-templates.md)   
 [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)   
 [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)   
 [使用和提供服务](../extensibility/using-and-providing-services.md)   
 [扩展连接的服务](../extensibility/extending-connected-services.md)   
 [管理 vspackage](../extensibility/managing-vspackages.md)   
 [Visual Studio 独立 Shell](../extensibility/visual-studio-isolated-shell.md)   
 [发布 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)   
 在[Visual STUDIO SDK](../extensibility/internals/inside-the-visual-studio-sdk.md)   
 [支持 Visual STUDIO SDK](../extensibility/support-for-the-visual-studio-sdk.md)   
 [存档](../extensibility/archive.md)   
 [Visual Studio SDK 引用](../extensibility/visual-studio-sdk-reference.md)
