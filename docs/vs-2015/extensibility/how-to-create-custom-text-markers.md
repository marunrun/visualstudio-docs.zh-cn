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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435972"
---
# <a name="how-to-create-custom-text-markers"></a>如何：创建自定义文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你想要创建自定义文本标记，以强调或组织代码，必须执行以下步骤：  
  
- 注册新文本标记，以便其他工具可以访问它  
  
- 提供的默认实现和文本标记的配置  
  
- 创建一个服务用于其他进程可用于使文本标记的使用  
  
  有关如何将文本标记应用到某个区域的代码的详细信息，请参阅[如何：使用文本标记](../extensibility/how-to-use-text-markers.md)。  
  
### <a name="to-register-a-custom-marker"></a>若要注册自定义标记  
  
1. 创建一个注册表项，如下所示：  
  
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<Version>* \Text Editor\External Markers\\ *\<MarkerGUID>*  
  
    <em>\<MarkerGUID ></em>是`GUID`用于标识要添加的标记  
  
    *\<版本 >* 新版[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，例如 8.0  
  
    *\<PackageGUID >* 是实现自动化对象的 vspackage 的 GUID。  
  
   > [!NOTE]
   > 根路径的 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<版本 >* 初始化 Visual Studio shell 时，有关详细信息，请参阅时，可以使用备用根覆盖[命令行开关](../extensibility/command-line-switches-visual-studio-sdk.md)。  
  
2. 创建四个值下 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<版本 >* \Text Editor\External 标记\\ *\<MarkerGUID>*  
  
   - (默认)  
  
   - 服务  
  
   - DisplayName  
  
   - package  
  
   - `Default` 是 REG_SZ 类型的可选项。 设置时，该条目的值是包含一些有用的标识信息，例如"自定义文本标记"的字符串。  
  
   - `Service` 类型为 REG_SZ 的条目包含通过 proffering 提供自定义文本标记的服务的 GUID 字符串<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>。 格式为 {XXXXXX XXXX XXXX XXXX XXXXXXXXX}。  
  
   - `DisplayName` 类型为 REG_SZ 的条目包含自定义文本标记的名称的资源 ID。 格式为 #YYYY。  
  
   - `Package` 条目的类型 REG_SZ 包含`GUID`VSPackage 提供服务的服务下列出。 格式为 {XXXXXX XXXX XXXX XXXX XXXXXXXXX}。  
  
### <a name="to-create-a-custom-text-marker"></a>若要创建自定义文本标记  
  
1. 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType> 接口。  
  
     此接口的实现定义的行为和外观的自定义标记类型。  
  
     时，将调用此接口  
  
    1. 用户首次启动 IDE。  
  
    2. 用户选择**重置默认值**按钮下**字体和颜色**中的属性页**环境**文件夹，位于左窗格中的**选项**从对话框获取**工具**IDE 的菜单。  
  
2. 实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider.GetTextMarkerType%2A>方法，指定其`IVsPackageDefinedTextMarkerType`实现应用于根据返回的标记类型的方法调用中指定的 GUID。  
  
     环境调用此方法第一次你自定义标记的类型创建，并指定标识的自定义标记类型的 GUID。  
  
### <a name="to-proffer-your-marker-type-as-a-service"></a>若要为服务提供标记类型  
  
1. 调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager.QueryService%2A>方法<xref:Microsoft.VisualStudio.Shell.Interop.SProfferService>。  
  
     一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>返回。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.ProfferService%2A>方法，指定 GUID 标识你自定义标记类型的服务并提供指向您的实现的<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>接口。 你<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>实现应返回一个指针，向您实施的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>接口。  
  
     一个标识，所以你的服务将返回唯一的 cookie。 更高版本可以使用此 cookie 撤消你自定义标记类型的服务通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A>方法的<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>接口指定此 cookie 值。  
  
## <a name="see-also"></a>请参阅  
 [旧版 API 中使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)   
 [如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)   
 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)
