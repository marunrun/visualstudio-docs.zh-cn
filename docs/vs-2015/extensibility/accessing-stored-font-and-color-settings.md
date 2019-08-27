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
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821830"
---
# <a name="accessing-stored-font-and-color-settings"></a>访问存储的字体和颜色设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成的开发环境 (IDE) 存储修改后的设置字体和颜色在注册表中。 可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>界面来访问这些设置。  
  
## <a name="to-initiate-state-persistence-of-fonts-and-colors"></a>若要启动的字体和颜色的状态持久性  
 字体和颜色信息存储在以下注册表位置中按类别: [HKCU\SOFTWARE\Microsoft \Visual Studio\\ *\<Visual Studio 版本 >* \FontAndColors\\ *\<CategoryGUID >* ]，其中 *\<CategoryGUID >* 类别的 GUID。  
  
 因此，若要启动暂留，VSPackage 必须：  
  
- 获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口通过调用`QueryService`针对全局服务提供程序。  
  
     `QueryService` 必须使用的服务 ID 自变量调用`SID_SVsFontAndColorStorage`的接口 ID 自变量和`IID_IVsFontAndColorStorage`。  
  
- 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A>方法打开某个类别，以保存通过使用类别的 GUID 和模式标志作为参数。  
  
  通过指定的模式`fFlags`参数，构造中的值从<xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>枚举。 此模式下控制：  

  - 可以通过访问的设置<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口。  

  - 所有设置或仅这些用户修改的并且可通过检索<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口。  

  - 将更改传播到用户设置的方式。  

  - 所使用的颜色值的格式。  

## <a name="to-use-state-persistence-of-fonts-and-colors"></a>若要使用的字体和颜色的状态持久性  
 保留的字体和颜色涉及：  
  
- 与存储在注册表中设置同步的 IDE 设置。  
  
- 传播注册表修改信息。  
  
- 设置和检索存储在注册表中的设置。  
  
  与 IDE 设置同步的存储设置是很大程度上透明的。 基础 IDE 自动将写入的更新的设置**显示项**到类别的注册表项。  
  
  如果多个 Vspackage 共享特定类别，VSPackage 应要求将生成事件时的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口用于修改存储的注册表设置。  
  
  默认情况下未启用事件生成。 若要启用事件生成，类别必须打开使用<xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>。 这会导致 IDE 以调用适当<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>VSPackage 实现的方法。  
  
> [!NOTE]
> 通过修改**字体和颜色**属性页生成事件的独立<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>。 可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>接口，以确定是否在调用的方法需要更新的缓存的字体和颜色设置<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>类。  
  
### <a name="storing-and-retrieving-information"></a>存储和检索信息  
 若要获取或配置的用户可以修改在打开的类别为命名的显示项的信息，Vspackage 将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetItem%2A>方法。  
  
 有关字体的信息特性的使用获取特定类别<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetFont%2A>方法。  
  
> [!NOTE]
> `fFlags`自变量传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A>方法时已打开该类别定义的行为<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A>方法。 默认情况下，这些方法仅返回信息 aboutdisplay itemsthat 已更改。 但是，如果使用打开类别<xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>标志，同时更新，并且可以通过访问不变的显示项<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A>。  
  
 默认情况下，仅更改**显示项**信息保存在注册表中。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口不能用于检索所有设置的字体和颜色。  
  
> [!NOTE]
> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A>并<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A>方法返回 REGDB_E_KEYMISSING，(0x80040152L) 使用它们来检索信息时，有关未更改**显示项**。  
  
 所有的设置**显示项**中特定**类别**可以通过使用的方法来获取`T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults`接口。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>   
 [实现自定义类别和显示项](../extensibility/implementing-custom-categories-and-display-items.md)
