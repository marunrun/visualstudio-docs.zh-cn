---
title: 获取字体和颜色信息对文本着色 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696861"
---
# <a name="getting-font-and-color-information-for-text-colorization"></a>获取字体和颜色信息对文本着色
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

呈现或以的文本显示在用户界面 (UI) 元素中的过程取决于项目、 其技术和开发人员首选项的类型。 **字体和颜色**属性页存储的设置。  
  
 显示以的文本的大多数实现需要`T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults`和关联接口，用于显示、 检索和存储文本显示设置。  
  
> [!NOTE]
> 自定义核心编辑器时 (它也支持**文本 EditorCategory**)，强烈建议你使用的着色技术语言服务中。 有关详细信息，请参阅[字体和颜色概述](../extensibility/font-and-color-overview.md)。  
  
## <a name="getting-default-font-and-color-information"></a>获取默认字体和颜色信息  
 所有**字体和颜色**应在指定的任何窗口中显示的文本设置**显示项**之一**类别**。 有关详细信息，请参阅[字体和 Colors，Environment，Options Dialog Box](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)。  
  
 若要为着色，VSPackage 必须获取当前**字体和颜色**设置。 VSPackage 可以按以下方式，具体取决于其需要完成此操作：  
  
- 使用的字体和颜色的永久保存机制来检索存储或当前状态。 有关详细信息，请参阅[访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)。  
  
- 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>接口的一种服务进行要获取的实例的字体和颜色数据<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>，如果 VSPackage 还不是字体和颜色提供程序。  
  
- 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> 接口。  
  
  若要确保通过轮询获得的结果是最新的它可能需要使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>接口以确定更新是否需要在调用的检索方法之前<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口。  
  
  后获取字体和颜色信息分析文本要显示来标识需要着色的元素，然后使用相应的字体和颜色在窗口中显示文本。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 [使用字体和文本](https://msdn.microsoft.com/library/d43640f3-da94-4df2-a29d-a9d021a1c069)   
 [处理颜色](https://msdn.microsoft.com/library/d34ff96f-241d-494f-abdd-13811ada8cd3)   
 [GDI （图形设备接口）](https://msdn.microsoft.com/7e1d4540-bb2e-4257-8eee-eee376acba83)
