---
title: 支持设置类别 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- settings, supporting with Visual Studio SDK
- Visual Studio SDK, supporting settings
ms.assetid: 3bac375d-8bd5-41be-a8de-32eb33c5cfac
caps.latest.revision: 20
manager: jillfra
ms.openlocfilehash: 15a3896f8a2010a063393d3a11c1ed3453a008d5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65689101"
---
# <a name="support-for-settings-categories"></a>支持设置类别
设置类别包含一组可自定义集成开发环境 (IDE) 的选项。 例如，设置可以控制 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 窗口的布局和菜单的内容。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 在“工具”  菜单上，单击“导入和导出设置”  以启动“导入和导出设置向导” 。 向导提供三个选项：导出、导入或重置设置。 例如，选择导出会打开向导的“选择要导出的设置”  页面。  
  
 此页面的导航窗格中的树控件会列出类别。 类别是一组显示为“自定义设置点”（即显示为复选框）的相关设置。 使用这些复选框可选择要保留在 .vsettings 文件中的类别。 向导允许命名 .vsettings 文件并指定其路径。  
  
> [!NOTE]
> 设置会作为类别进行保存或还原，各个设置名称不会显示在向导中。  
  
 托管包框架 (MPF) 支持使用最少的额外代码创建设置类别。  
  
- 可创建 VSPackage，以便通过创建 <xref:Microsoft.VisualStudio.Shell.Package> 类的子类来为类别提供容器。  
  
- 可通过从 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类派生来创建类别本身。  
  
- 可使用 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 将这两者联系起来。  
  
## <a name="support-for-settings-categories"></a>支持设置类别  
 <xref:Microsoft.VisualStudio.Shell.Package> 类为创建类别提供支持。 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类可实现类别。 <xref:Microsoft.VisualStudio.Shell.DialogPage> 的默认实现以类别的形式向用户提供其公共属性。 有关详细信息，请参阅 [Creating a Settings Category](../extensibility/creating-a-settings-category.md)。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类实现 <xref:Microsoft.VisualStudio.Shell.IProfileManager>，后者为选项页面和用户设置提供持久性。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromXml%2A> 和 <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToXml%2A> 方法将设置保留在 .vssettings 文件中（[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分别以 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsWriter> 的形式提供该文件）。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.ResetSettings%2A> 方法将设置重置为其默认值。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类提供 <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromXml%2A> 方法的实现，该方法从 xml 源读取名称/值对，并使用反射发现 <xref:Microsoft.VisualStudio.Shell.DialogPage> 派生类中的公共属性。 会向名称与名称/值对匹配的属性提供对应值。  
  
 <xref:Microsoft.VisualStudio.Shell.DialogPage.SaveSettingsToXml%2A> 的默认实现使用反射发现 <xref:Microsoft.VisualStudio.Shell.DialogPage> 派生类中的公共属性，并以名称/值对的形式向 XML 源写入属性名称和值。  
  
### <a name="settings-category-registry-path"></a>设置类别注册表路径  
 类别设置的注册表路径通过将 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、UserSettings 一词、设置类别和自定义设置点的名称进行组合来确定。 类别设置和自定义设置点的名称进行联接并使用下划线进行分隔，以形成出现在注册表中的非本地化规范名称。 例如，如果类别设置是“My Category”，自定义设置点名称是“My Settings”，并且 ApplicationRegistryRoot 是 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp，则设置类别具有注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\UserSettings\My Category_My Settings。  
  
> [!NOTE]
> 规范名称不会出现在用户界面 (UI) 中。 它用于将可读名称与设置类别进行关联，非常类似于编程标识符 (ProgID)。  
  
### <a name="settings-category-attribute"></a>设置类别属性  
 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>确定到中的自定义设置点类别的映射**导入和导出设置向导**通过将类别与提供它的 VSPackage 相关联。 考虑以下代码片断：  
  
 [!code-csharp[VSSDKSupportForSettingsCategories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksupportforsettingscategories/cs/vssdksupportforsettingscategoriespackage.cs#1)]
 [!code-vb[VSSDKSupportForSettingsCategories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportforsettingscategories/vb/vssdksupportforsettingscategoriespackage.vb#1)]  
  
 资源 ID 106 映射到“My Category”，107 映射到“My Settings”，108 映射到“Various Options”。 这声明 `MyPackage` 提供类别 My Category_My Settings。 该类别由 `OptionsPageGeneral` 类提供，该类必须实现 <xref:Microsoft.VisualStudio.Shell.IProfileManager>。 该类别中的设置是 `OptionsPageGeneral` 类的公共属性。  
  
 在“导入和导出设置向导” 中，设置点的名称是 My Settings。 选择设置点时，说明“Various Options” 会出现。 设置点名称和说明取自本地化字符串资源。  
  
## <a name="see-also"></a>请参阅  
 [创建选项页](../extensibility/creating-an-options-page.md)   
 [VSSDK 示例](../misc/vssdk-samples.md)   
 [VSPackage 状态](../misc/vspackage-state.md)   
 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)