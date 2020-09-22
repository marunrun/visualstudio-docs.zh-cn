---
title: 如何：创建自定义文本标记 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - custom text markers
ms.assetid: 6e32ed81-c604-4a32-9012-8db3bec7c846
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ac681879e0f7ad0902358be23d74d57ccee406f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840351"
---
# <a name="how-to-create-custom-text-markers"></a>如何：创建自定义文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要创建自定义文本标记以强调或组织代码，必须执行以下步骤：  
  
- 注册新的文本标记，以便其他工具可以访问它  
  
- 提供文本标记的默认实现和配置  
  
- 创建可由其他进程用来利用文本标记的服务  
  
  有关如何对代码区域应用文本标记的详细信息，请参阅 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)。  
  
### <a name="to-register-a-custom-marker"></a>注册自定义标记  
  
1. 按如下所示创建注册表项：  
  
    HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio \\ *\<Version>* \Text Editor\External 标记\\*\<MarkerGUID>*  
  
    <em>\<MarkerGUID></em>`GUID`用于标识要添加的标记的。  
  
    *\<Version>* 是的版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，例如8。0  
  
    *\<PackageGUID>* 实现自动化对象的 VSPackage 的 GUID。  
  
   > [!NOTE]
   > \\ *\<Version>* 初始化 Visual Studio shell 时，可以使用备用根覆盖 HKEY_LOCAL_MACHINE \software\microsoft\visualstudio 的根路径。有关详细信息，请参阅[命令行开关](../extensibility/command-line-switches-visual-studio-sdk.md)。  
  
2. 在 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio \\ *\<Version>* \Text Editor\External 标记下创建四个值\\*\<MarkerGUID>*  
  
   - （默认值）  
  
   - 服务  
  
   - DisplayName  
  
   - 包  
  
   - `Default` REG_SZ 类型的可选条目。 设置后，该条目的值是一个字符串，其中包含一些有用的标识信息，例如 "自定义文本标记"。  
  
   - `Service` REG_SZ 类型的条目，其中包含通过 proffering 提供自定义文本标记的服务的 GUID 字符串 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider> 。 格式为 {XXXXXX XXXX xxxx XXXX XXXXXXXXX}。  
  
   - `DisplayName` REG_SZ 类型的条目，其中包含自定义文本标记的名称的资源 ID。 格式为 #YYYY。  
  
   - `Package` REG_SZ 类型的输入 `GUID` ，它包含提供服务中列出的服务的 VSPackage 的。 格式为 {XXXXXX XXXX xxxx XXXX XXXXXXXXX}。  
  
### <a name="to-create-a-custom-text-marker"></a>创建自定义文本标记  
  
1. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType> 接口。  
  
     此接口的实现定义自定义标记类型的行为和外观。  
  
     此接口在  
  
    1. 用户首次启动 IDE。  
  
    2. 用户选择 "**环境**" 文件夹中 "**字体和颜色**" 属性页下的 "**重置默认值**" 按钮，该按钮位于从 IDE 的 "**工具**" 菜单中获取的 "**选项**" 对话框的左窗格中。  
  
2. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider.GetTextMarkerType%2A> 方法，指定 `IVsPackageDefinedTextMarkerType` 应根据方法调用中指定的标记类型 GUID 返回的实现。  
  
     在首次创建自定义标记类型时，环境将调用此方法，并指定标识自定义标记类型的 GUID。  
  
### <a name="to-proffer-your-marker-type-as-a-service"></a>将标记类型提供为服务  
  
1. 调用的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager.QueryService%2A> 方法 <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> 。  
  
     返回指向的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.ProfferService%2A> 方法，并指定标识自定义标记类型服务的 GUID，并提供指向接口的实现的指针 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 。 你的 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 实现应返回指向接口的实现的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider> 。  
  
     标识服务返回的唯一 cookie。 稍后可以通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> 指定此 cookie 值的接口的方法，使用此 cookie 来撤消自定义标记类型服务。  
  
## <a name="see-also"></a>另请参阅  
 [将文本标记与旧版 API 一起使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)   
 [如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)   
 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)
