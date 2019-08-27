---
title: 实现自定义类别和显示项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- font and color control [Visual Studio SDK], categories
- custom categories
ms.assetid: 99311a93-d642-4344-bbf9-ff6e7fa5bf7f
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 474d5c66507b56bea609568b6acfe9f5eff75e9c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63414608"
---
# <a name="implementing-custom-categories-and-display-items"></a>实现自定义类别和显示项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage 可以提供控件的字体和颜色对其文本的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]通过自定义类别和显示项的集成的开发环境 (IDE)。  
  
 自定义类别和显示项位于**字体和颜色**属性页。 若要打开**字体和颜色**属性页上，在**工具**菜单中，单击**选项**。 展开**环境**，然后单击**字体和颜色**。  
  
 在使用此机制，Vspackage 必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>接口和其关联的接口。  
  
 原则上，可以使用此机制来修改所有现有**显示的项**并**类别**包含它们。 但是，它不应修改**文本 EditorCategory**或其**显示项**。 有关详细信息，请参阅[字体和颜色概述](../extensibility/font-and-color-overview.md)。  
  
 若要实现自定义**类别**或**显示项**，VSPackage 必须：  
  
- 创建或标识注册表中的类别。  
  
   IDE 的实现**字体和颜色**属性页使用此信息来正确地查询支持给定的类别的服务。  
  
- 创建或标识组 （可选） 在注册表中。  
  
   它可能很适合用于定义一个表示集合的两个或多个类别的组。 如果定义一个组，则 IDE 将自动合并子类别，并将分发在组中的显示项。  
  
- 实现 IDE 的支持。  
  
- 处理更改字体和颜色。  
  
  有关信息，请参阅[访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)。  
  
## <a name="to-create-or-identify-categories"></a>若要创建或标识类别  
  
- 构造一个特殊类型的类别下的注册表项 [HKLM\SOFTWARE\Microsoft \Visual Studio\\*\<Visual Studio 版本 >* \FontAndColors\\`<Category>`]  
  
   *\<类别 >* 类别的非本地化名称。  
  
- 填充注册表具有两个值：  
  
  |名称|类型|数据|描述|  
  |----------|----------|----------|-----------------|  
  |类别|REG_SZ|GUID|创建标识类别的 GUID。|  
  |package|REG_SZ|GUID|支持类别的 VSPackage 服务的 GUID。|  
  
  在注册表中指定的服务必须提供的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>相应类别。  
  
## <a name="to-create-or-identify-groups"></a>若要创建或标识组  
  
- 构造一个特殊类型的类别下的注册表项 [HKLM\SOFTWARE\Microsoft \Visual Studio\\*\<Visual Studio 版本 >* \FontAndColors\\  *\<组 >*]  
  
   *\<组 >* 是组的非本地化名称。  
  
- 填充注册表具有两个值：  
  
  |名称|类型|数据|描述|  
  |----------|----------|----------|-----------------|  
  |类别|REG_SZ|GUID|创建以确定组的 GUID。|  
  |package|REG_SZ|GUID|支持类别的服务的 GUID。|  
  
  在注册表中指定的服务必须提供的实现`T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup`为相应的组。  
  
## <a name="to-implement-ide-support"></a>若要实现 IDE 支持  
  
- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider.GetObject%2A>，这会返回任一<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>接口或`T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup`接口的每个 IDE**类别**或组提供的 GUID。  
  
- 对于每个**类别**它支持、 VSPackage 实现的一个单独实例<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>接口。  
  
- 方法实现通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>必须提供与 IDE:  
  
  - 列出的**显示的项**中**类别。**  
  
  - 可本地化的名称**显示的项**。  
  
  - 显示的每个成员的信息**类别**。  
  
  > [!NOTE]
  > 每个**类别**必须包含至少一个**显示项**。  
  
- IDE 使用`T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup`接口可定义多个类别的联合。  
  
   其实现提供了与 IDE:  
  
  - 一系列**类别**组成给定的组。  
  
  - 对实例的访问<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>支持每个**类别**组内。  
  
  - 可本地化的组名称。  
  
- 正在更新 IDE:  
  
   IDE 缓存有关的信息**字体和颜色**设置。 因此，在 IDE 的任何修改后**字体和颜色**配置，则最好确保缓存是最新。  
  
  更新缓存是通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>接口，并可执行全局或仅在所选的项。  
  
## <a name="to-handle-font-and-color-changes"></a>若要处理字体和颜色更改  
 若要正确支持 VSPackage 显示的文本的颜色，支持 VSPackage 的着色服务必须响应通过所做的用户启动的更改**字体和颜色**属性页。 VSPackage 可以做到这一点：  
  
- 通过实现处理 IDE 生成的事件<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>接口。  
  
     IDE 调用相应的方法遵循的用户修改**字体和颜色**页。 例如，它调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents.OnFontChanged%2A>如果选择新字体的方法。  
  
     或  
  
- 轮询更改 IDE。  
  
     这可以通过系统实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口。 主要用于支持暂留，尽管<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A>方法可用于获取字体和颜色信息**显示项**。 有关详细信息，请参阅[访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)。  
  
    > [!NOTE]
    > 若要确保正确轮询所获得的结果，可能会使用很有用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>接口，以确定是否刷新的缓存和 update 之前调用的检索方法所需<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>接口。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 [获取字体和颜色信息对文本着色](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)   
 [如何：访问内置的字体和配色方案](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)   
 [字体和颜色概述](../extensibility/font-and-color-overview.md)
