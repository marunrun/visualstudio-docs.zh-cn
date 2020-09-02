---
title: 使用字体和颜色 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, controlling in IDE
- IDE, controlling text color and fonts
- Fonts and Colors property page
- font and color control [Visual Studio SDK]
- text, IDE
ms.assetid: d1a9b99f-fbdc-45ed-920a-e08c3d931ac9
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42ebc9414e3e5bb10f2468ed7f5f4fb4900e4ec6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68177226"
---
# <a name="using-fonts-and-colors"></a>使用字体和颜色
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

为 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 使用字体和颜色显示文本提供支持。  
  
## <a name="in-this-section"></a>本节内容  
 [字体和颜色概述](../extensibility/font-and-color-overview.md)  
 讨论 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (IDE) 的集成开发环境中的文本字体和颜色设置。 还介绍了类别和显示项的概念，并介绍了 Vspackage 和核心编辑器如何使用文本特性。  
  
 [获取文本着色的字体和颜色信息](../extensibility/getting-font-and-color-information-for-text-colorization.md)  
 提供有关在 Vspackage 中实现文本着色的指导原则，这些类别管理**文本编辑器**之外的**类别**。  
  
 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)  
 说明如何存储、检索和应用当前字体和颜色设置。  
  
 [实现自定义类别和显示项](../extensibility/implementing-custom-categories-and-display-items.md)  
 描述窗口创建和使用其自己的 **显示项** 和 **类别** 以支持文本显示的基本步骤。  
  
 此方法需要 VSPackage 来实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> 接口和相关接口。  
  
 [如何：访问内置字体和配色方案](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)  
 讨论如何使用内置字体和颜色定义和注册类别，并启动系统提供的字体和颜色的使用。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>  
 提供一个的实例， `IVsFontAndColorDefaults` 或与 "选项" 对话框的 " <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> **字体和颜色**" 页的 "**显示其设置**" 列表中列出的特定**Options**项相对应的接口。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>  
 通过为窗口或 UI 组件定义默认字体和颜色，使 VSPackage 支持 "IDE **字体和颜色** " 页。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>  
 提供了一种机制，通过该机制，提供字体和颜色支持的 VSPackage 可以指定显示项组，即一个表示两个或多个类别的联合的超级类别。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>  
 允许 VSPackage 检索字体和颜色数据，或将其保存到注册表中。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>  
 通知 Vspackage，其中使用的字体和颜色信息与字体和颜色设置中的更改有关。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities>  
 提供一些工具，用于处理 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **字体和颜色** 机制的方法使用的输入和输出数据。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>  
 控制字体和颜色设置的缓存。  
  
## <a name="related-sections"></a>相关章节  
 [开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)  
 讨论 Vspackage 如何使用语言服务自定义 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 编辑器。  
  
 [自定义编辑器中的语法着色](../extensibility/syntax-coloring-in-custom-editors.md)  
 Descries 编辑器如何 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 使用语言服务来实现语法着色。  
  
 [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)  
 说明如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的其余部分的 UI 元素。
