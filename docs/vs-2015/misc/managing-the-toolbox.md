---
title: 管理 "工具箱" |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Toolbox [Visual Studio SDK], automatic tab selection
- Toolbox [Visual Studio SDK], managing
ms.assetid: 3b052047-f6db-46dd-b3bf-da1c348ee410
caps.latest.revision: 33
manager: jillfra
ms.openlocfilehash: 5eeb5d06b0e689391f450fec8744fa58a41f4508
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65681546"
---
# <a name="managing-the-toolbox"></a>Managing the Toolbox
[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 允许 VSPackage（如编辑器或设计器）管理“工具箱” **** 的成员资格和外观。  
  
 此外，还可以使用自动化管理“工具箱” **** 本身。 有关通过自动化管理工具箱的详细信息，请参阅 [How to: Control the Toolbox](https://msdn.microsoft.com/library/c9d8a18a-d2bc-43d4-a803-601bfc6a6599)。  
  
## <a name="automatic-toolbox-tab-selection"></a>自动工具箱选项卡选择  
 可以基于当前处于活动状态的编辑器或设计器，自动激活特定的“工具箱” **** 选项卡或类别。 例如，如果已激活窗体设计器，那么你可能希望选中“所有 Windows 窗体” **** 选项卡。  
  
 此支持仅限于编辑器和设计器，并要求：  
  
1. 实现工厂对象以提供编辑器或设计器实例。 有关实现设计器或编辑器工厂对象的详细信息，请参阅 [Editor Factories](../extensibility/editor-factories.md)。  
  
2. 如果存在编辑器或设计器，则将自动激活工具箱选项卡的注册。  
  
## <a name="controlling-the-toolbox"></a>控制工具箱  
 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 提供以下接口，使 VSPackage 能够更好地控制对“工具箱” **** 的管理方式，对自动支持进行了补充。  
  
|接口|说明|  
|---------------|-----------------|  
|<xref:System.Drawing.Design.IToolboxService>|允许应用程序管理、添加和删除 <xref:System.Drawing.Design.ToolboxItem> **工具箱**中的对象。 此外，还允许配置外观和“工具箱” **** 类别。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>|允许应用程序管理、添加和删除基于活动的“工具箱” **** 控件，以及配置“工具箱” **** 类别和外观。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>|通过为持久性和本地化提供全面的支持，可在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 中找到扩展功能。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox4>||  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox5>||  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox6>||  
  
 使用这些接口时，需要注意以下几个要点：  
  
- <xref:System.Drawing.Design.IToolboxService> 仅适用于基于托管的包框架的 VSPackage。  
  
- 控件不能使用直接添加到 **工具箱** 中 <xref:System.Drawing.Design.IToolboxService> 。  
  
- VSPackage 必须使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 来添加控件或托管派生自 <xref:System.Windows.Forms.AxHost> 的包装器控件中的控件。  
  
   Visual Studio 提供了 `Aximp.exe` 工具，以自动包装派生自 <xref:System.Windows.Forms.AxHost> 的控件中的 ActiveX 控件。 有关详细信息，请参阅 [Aximp.exe (Windows 窗体 ActiveX 控件导入程序) ](https://msdn.microsoft.com/library/482c0d83-7144-4497-b626-87d2351b78d0)。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> 是基于 COM 的接口，可通过互操作程序集获得。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 派生自 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox>，并实现其所有方法。  
  
   对象仅获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 的实例。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> 不是派生自 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>，且不会实现其方法。  
  
   如果对象需要两个接口中的功能，则该对象必须从环境中获取这两个接口的实例。  
  
- 在使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> 时，有关选项卡的规范（非本地化）名称的信息由 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3.GetIDOfTab%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3.SetIDOfTab%2A> 方法进行处理。  
  
- 当使用 <xref:System.Drawing.Design.IToolboxService> 时，由实现者管理本地化信息，如类别的名称。  
  
  使用设置机制以允许用户保存“工具箱” **** 设置，用户可以通过 IDE 的“工具” **** 菜单上的“导入/导出设置” **** 命令访问这些设置。 有关如何使用设置的详细信息，请参阅 [Extending User Settings and Options](../extensibility/extending-user-settings-and-options.md)。  
  
## <a name="see-also"></a>另请参阅  
 [扩展工具箱](../misc/extending-the-toolbox.md)