---
title: 获取文本着色的字体和颜色信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- text, coloring
- font and color control [Visual Studio SDK], coloring
ms.assetid: d1f985bd-743e-40b7-9458-d9af53647c91
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8724c31accb26e478c2726dfe791256994fc95ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696861"
---
# <a name="getting-font-and-color-information-for-text-colorization"></a>获取文本着色的字体和颜色信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在用户界面 (UI) 元素中呈现或显示着色文本的过程取决于项目的类型、技术和开发人员首选项。 " **字体和颜色** " 属性页存储设置。  
  
 大多数显示着色文本的实现都需要 `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults` 和关联的接口来显示、检索和存储文本显示设置。  
  
> [!NOTE]
> 自定义支持 **文本 EditorCategory**) 的核心编辑器 (时，强烈建议你在语言服务中使用着色技术。 有关详细信息，请参阅 " [字体和颜色概述](../extensibility/font-and-color-overview.md)"。  
  
## <a name="getting-default-font-and-color-information"></a>获取默认字体和颜色信息  
 所有显示文本的窗口的**字体和颜色**设置都应在一个**类别**的 "**显示项**" 中指定。 有关详细信息，请参阅 " [字体和颜色、环境、选项" 对话框](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)。  
  
 若要着色，VSPackage 必须获取当前的 **字体和颜色** 设置。 VSPackage 可通过以下方式完成此操作，具体取决于其需求：  
  
- 使用 "字体" 和 "颜色" 持久性机制来检索存储或当前状态。 有关详细信息，请参阅 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> 如果 VSPackage 也不是字体和颜色提供程序，请使用提供字体和颜色数据的服务接口来获取的实例。  
  
- 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> 接口。  
  
  若要确保通过轮询获得的结果是最新的，在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> 调用接口的检索方法之前，使用接口来确定是否需要更新可能会很有用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  
  
  获取字体和颜色信息后，请分析要显示的文本，以标识要求着色的元素，然后使用相应的字体和颜色在窗口中显示文本。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 [使用字体和文本](https://msdn.microsoft.com/library/d43640f3-da94-4df2-a29d-a9d021a1c069)   
 [使用颜色](https://msdn.microsoft.com/library/d34ff96f-241d-494f-abdd-13811ada8cd3)   
 [GDI (图形设备接口) ](https://msdn.microsoft.com/7e1d4540-bb2e-4257-8eee-eee376acba83)
