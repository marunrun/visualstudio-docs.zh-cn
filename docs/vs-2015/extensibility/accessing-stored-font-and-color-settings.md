---
title: 访问存储的字体和颜色设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, accessing stored settings
- font and color control [Visual Studio SDK], persistence
- colors, accessing stored settings
ms.assetid: beba7174-e787-45c2-b6ff-a60f67ad4998
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fbb2f118d903eae2124e705f14c7aa7b51bf9c4d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "67821830"
---
# <a name="accessing-stored-font-and-color-settings"></a>访问存储的字体和颜色设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成开发环境 (IDE) 为注册表中的字体和颜色存储修改后的设置。 您可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 接口来访问这些设置。  
  
## <a name="to-initiate-state-persistence-of-fonts-and-colors"></a>启动字体和颜色的状态持久性  
 字体和颜色信息按类别存储在以下注册表位置中： [HKCU\SOFTWARE\Microsoft \Visual Studio \\ *\<Visual Studio version>* \FontAndColors \\ *\<CategoryGUID>* ]，其中 *\<CategoryGUID>* 是类别 GUID。  
  
 因此，若要启动持久性，VSPackage 必须：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>通过调用 `QueryService` 全局服务提供程序来获取接口。  
  
     `QueryService` 必须使用的服务 ID 参数 `SID_SVsFontAndColorStorage` 和的接口 id 参数来调用 `IID_IVsFontAndColorStorage` 。  
  
- 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A> 方法可通过将类别的 GUID 和模式标志用作参数来打开要保存的类别。  
  
  由参数指定的模式由 `fFlags` 枚举中的值构造而成 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> 。 此模式控制：  

  - 可以通过接口访问的设置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  

  - 要么是所有的设置，要么只是用户修改的、可通过接口检索的设置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  

  - 传播对用户设置所做更改的方式。  

  - 使用的颜色值的格式。  

## <a name="to-use-state-persistence-of-fonts-and-colors"></a>使用字体和颜色的状态持久性  
 保存字体和颜色涉及：  
  
- 将 IDE 设置与注册表中存储的设置进行同步。  
  
- 传播注册表修改信息。  
  
- 设置和检索注册表中存储的设置。  
  
  将存储设置与 IDE 设置同步很大程度上是透明的。 基础 IDE 自动将 **显示项** 的更新设置写入类别的注册表项。  
  
  如果多个 Vspackage 共享特定类别，则 VSPackage 应要求在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 使用接口的方法修改存储的注册表设置时生成事件。  
  
  默认情况下，不启用事件生成。 若要启用事件生成，必须使用打开一个类别 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> 。 这会使 IDE 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> VSPackage 实现的适当方法。  
  
> [!NOTE]
> 通过 " **字体和颜色** " 属性页的修改将生成独立于的事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> 调用类的方法之前，可以使用接口来确定是否需要更新缓存的字体和颜色设置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  
  
### <a name="storing-and-retrieving-information"></a>存储和检索信息  
 若要获取或配置用户可以为打开的类别中的已命名显示项修改的信息，Vspackage 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetItem%2A> 方法。  
  
 有关特定类别的字体属性的信息，请使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> 和方法获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetFont%2A> 。  
  
> [!NOTE]
> `fFlags` <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A> 当该类别打开时，传递给方法的参数定义 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> 和方法的行为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> 。 默认情况下，这些方法只返回 aboutdisplay itemsthat 已更改的信息。 但是，如果使用标志打开类别 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> ，则和都可以访问更新和未更改的显示项 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> 。  
  
 默认情况下，注册表中仅保留更改的 **显示项** 信息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口不能用于检索字体和颜色的所有设置。  
  
> [!NOTE]
> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> 当使用和方法检索有关未更改的**显示项**的信息时，将返回 REGDB_E_KEYMISSING， (0x80040152L) 。  
  
 可以通过使用接口的方法来获取特定**类别**中的所有**显示项**的设置 `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults` 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>   
 [实现自定义类别和显示项](../extensibility/implementing-custom-categories-and-display-items.md)
