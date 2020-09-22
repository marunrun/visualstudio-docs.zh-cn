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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840465"
---
# <a name="implementing-custom-categories-and-display-items"></a>实现自定义类别和显示项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage 可以 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 通过自定义类别和显示项，向集成开发环境 (IDE) 提供文本的字体和颜色。  
  
 自定义类别和显示项位于 " **字体和颜色** " 属性页上。 若要打开 " **字体和颜色** " 属性页，请在 " **工具** " 菜单上单击 " **选项**"。 展开 " **环境** "，然后单击 " **字体和颜色**"。  
  
 使用此机制时，Vspackage 必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> 接口及其关联接口。  
  
 原则上，此机制可用于修改所有现有 **显示项** 以及包含它们的 **类别** 。 但不应使用它来修改 **文本 EditorCategory** 或其 **显示项**。 有关详细信息，请参阅 " [字体和颜色概述](../extensibility/font-and-color-overview.md)"。  
  
 若要实现自定义 **类别** 或 **显示项**，VSPackage 必须：  
  
- 在注册表中创建或标识类别。  
  
   IDE 的 " **字体和颜色** " 属性页的实现将使用此信息来正确查询支持给定类别的服务。  
  
- 在注册表中创建或标识组 (可选) 。  
  
   定义组（表示两个或多个类别的联合）可能会很有用。 如果定义了组，则 IDE 会自动合并子类别，并在组内分配显示项。  
  
- 实现 IDE 支持。  
  
- 处理字体和颜色更改。  
  
  有关信息，请参阅 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)。  
  
## <a name="to-create-or-identify-categories"></a>创建或标识类别  
  
- 在 [HKLM\SOFTWARE\Microsoft \Visual Studio \\ *\<Visual Studio version>* \FontAndColors \\ `<Category>` ] 下构造一种特殊类型的类别注册表项  
  
   *\<Category>* 是类别的非本地化名称。  
  
- 用两个值填充注册表：  
  
  |名称|类型|数据|说明|  
  |----------|----------|----------|-----------------|  
  |类别|REG_SZ|GUID|为标识类别而创建的 GUID。|  
  |包|REG_SZ|GUID|支持该类别的 VSPackage 服务的 GUID。|  
  
  注册表中指定的服务必须为相应的类别提供的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> 。  
  
## <a name="to-create-or-identify-groups"></a>创建或标识组  
  
- 在 [HKLM\SOFTWARE\Microsoft \Visual Studio \\ *\<Visual Studio version>* \FontAndColors \\ *\<group>* ] 下构造一种特殊类型的类别注册表项  
  
   *\<group>* 组的非本地化名称。  
  
- 用两个值填充注册表：  
  
  |名称|类型|数据|说明|  
  |----------|----------|----------|-----------------|  
  |类别|REG_SZ|GUID|为标识组而创建的 GUID。|  
  |包|REG_SZ|GUID|支持该类别的服务的 GUID。|  
  
  注册表中指定的服务必须 `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` 为相应组提供的实现。  
  
## <a name="to-implement-ide-support"></a>实现 IDE 支持  
  
- 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider.GetObject%2A> ，该方法为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` 提供的每个 **类别** 或组 GUID，将接口或接口返回到 IDE。  
  
- 对于它支持的每个 **类别** ，VSPackage 实现了接口的单独实例 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> 。  
  
- 通过实现的方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> 必须向 IDE 提供以下内容：  
  
  - 类别中 **显示项** 的列表 **。**  
  
  - **显示项**的可本地化名称。  
  
  - 显示每个 **类别**成员的信息。  
  
  > [!NOTE]
  > 每个 **类别** 都必须至少包含一个 **显示项**。  
  
- IDE 使用 `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` 接口来定义多个类别的联合。  
  
   它的实现为 IDE 提供了：  
  
  - 包含给定组的 **类别** 的列表。  
  
  - 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> 支持组中每个 **类别** 的实例的访问。  
  
  - 可本地化的组名。  
  
- 更新 IDE：  
  
   IDE 缓存有关 **字体和颜色** 设置的信息。 因此，在对 IDE **字体和颜色** 配置进行修改后，最好确保缓存是最新的。  
  
  更新缓存是通过接口完成的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> ，可以全局执行，也可以仅在所选项目上执行。  
  
## <a name="to-handle-font-and-color-changes"></a>处理字体和颜色更改  
 若要正确支持 VSPackage 显示的文本的着色，支持 VSPackage 的着色服务必须响应用户通过 " **字体和颜色** " 属性页所做的更改。 VSPackage 通过以下方式执行此操作：  
  
- 通过实现接口处理 IDE 生成的事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> 。  
  
     在用户修改 " **字体和颜色** " 页后，IDE 将调用相应的方法。 例如， <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents.OnFontChanged%2A> 如果选择了新字体，它将调用方法。  
  
     - 或 -  
  
- 轮询 IDE 中的更改。  
  
     可以通过系统实现的接口完成此操作 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。 尽管主要是为了支持暂留，但 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> 方法可用于获取 **显示项**的字体和颜色信息。 有关详细信息，请参阅 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)。  
  
    > [!NOTE]
    > 若要确保通过轮询获得的结果是正确的，请在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> 调用接口的检索方法之前，使用接口来确定是否需要缓存刷新和更新，这可能会很有用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 [获取文本着色的字体和颜色信息](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)   
 [如何：访问内置字体和配色方案](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)   
 [字体和颜色概述](../extensibility/font-and-color-overview.md)
