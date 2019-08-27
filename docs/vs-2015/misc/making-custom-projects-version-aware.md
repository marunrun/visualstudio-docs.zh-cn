---
title: 使自定义项目版本可区别 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 5233d3ff-6e89-4401-b449-51b4686becca
caps.latest.revision: 33
manager: jillfra
ms.openlocfilehash: 0b29728cffc962b5d09a5adc45f8cac2093b020a
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825685"
---
# <a name="making-custom-projects-version-aware"></a>使自定义项目版本可区别
在自定义项目系统中，你可以允许在多个版本的 Visual Studio 中加载该类型的项目。 也可以阻止在早期版本的 Visual Studio 中加载该类型的项目。 还可以使该项目将其自身标识为较新版本，以防该项目需要修复、转换或弃用。  
  
## <a name="allowing-projects-to-load-in-multiple-versions"></a>允许在多个版本中加载项目  
 你可以修改在带有 SP1 的 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 或更高版本中创建的大多数项目，使其可在多个版本中使用。  
  
 加载项目之前，Visual Studio 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly%2A> 方法以确定是否可以随该项目进行升级。 如果可以对该项目进行升级，`UpgradeProject_CheckOnly` 方法将设置一个标志，该标志将引起稍后调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法以升级该项目。 由于不能对不兼容项目进行升级，因此 `UpgradeProject_CheckOnly` 必须首先检查项目兼容性，如上一部分中所述。  
  
 你作为项目系统的作者（从 `UpgradeProject_CheckOnly` 接口）实现 `IVsProjectUpgradeViaFactory4` ，以向该项目系统的用户提供升级检查。 当用户打开项目时，将调用此方法以确定是否必须在加载项目前修复该项目。 在 `VSPUVF_REPAIRFLAGS`中枚举了可能的升级需求，包括以下可能性：  
  
1. `SPUVF_PROJECT_NOREPAIR`：不需要修复。  
  
2. `VSPUVF_PROJECT_SAFEREPAIR`：使该项目与早期版本兼容，消除与以前版本的产品遇到可能具有的问题。  
  
3. `VSPUVF_PROJECT_UNSAFEREPAIR`：向后兼容，但你可能遇到的问题与以前版本的产品时可能遇到与使该项目。 例如，如果项目依赖于不同的 SDK 版本，则该项目不兼容。  
  
4. `VSPUVF_PROJECT_ONEWAYUPGRADE`：使该项目与早期版本不兼容。  
  
5. `VSPUVF_PROJECT_INCOMPATIBLE`：表示当前版本不支持此项目。  
  
6. `VSPUVF_PROJECT_DEPRECATED`：指示此项目不再受支持。  
  
> [!NOTE]
> 为避免混淆，设置升级标志时请勿将其合并。 例如，请勿创建 `VSPUVF_PROJECT_SAFEREPAIR | VSPUVF_PROJECT_DEPRECATED`等不明确的升级状态。  
  
 项目风格可能从 `UpgradeProjectFlavor_CheckOnly` 接口实现函数 `IVsProjectFlavorUpgradeViaFactory2` 。 若要使此函数生效，则前述 `IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly` 实现必须调用该函数。 已在 Visual Basic 或 C# 基本项目系统中实现此调用。 此函数使得在基本项目系统已确定的升级需求之外，项目风格也能确定项目的升级需求。 兼容性对话框将显示这两个要求中较严格者。  
  
 在 Visual Studio 执行升级检查时，它将提供一个记录器，而不是像在 Visual Studio 早期版本中一样 NULL 值。 该记录器使项目系统和风格能够提供额外信息，这些信息可以帮助你了解让较旧项目正确加载所需进行更改的本质。 我们建议使用记录器提供详细信息，而不使用对话框。 有关详细信息，请参阅本主题后面的 [The Upgrade Logger](../misc/making-custom-projects-version-aware.md#BKMK_UpgradeLogger) 。  
  
 对于托管实现，在 Microsoft.VisualStudio.Shell.Interop.11.0.dll 互操作程序集中提供了项目升级接口。  
  
 `UpgradeProject` 方法可以确定所做更改是否会妨碍在以前版本的 Visual Studio 中加载项目。 如果是这样，该方法会将项目标记为不兼容。 若要了解如何将项目标记为不兼容，请参阅本主题前面的 [Marking a Project as Incompatible](../misc/making-custom-projects-version-aware.md#BKMK_Incompat) 我们建议，在出现此对话框后通过直接调用方法 `IVsAppCompat.BreakAssetCompatibility` 将项目标记为不兼容，而不是首先调用 `IVsAppCompat.AskForUserConsentToBreakAssetCompat` 方法，因为对该话框不需要出现两次。  
  
 下面是一个有助于总结用兼容性户体验的示例。 如果项目是在早期版本中创建的，而当前版本确定需要升级，则 Visual Studio 将显示要求用户允许更改的对话框。 如果用户同意，则将修改并加载项目。 如果就此关闭并在在早期版本中重新打开该解决方案，则该单向升级的项目将不兼容且不加载。 如果项目仅需要修复（而非升级），则修复后的项目将仍可在这两个版本中打开。  
  
## <a name="BKMK_Incompat"></a> 将标记为不兼容的项目  
 你可以将项目标记为与早期版本的 Visual Studio 不兼容。  例如，假设你创建使用 .NET Framework 4.5 功能的项目。 由于不能在 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]生成此项目，因此可将其标记为不兼容，以防止该版本尝试加载它。  
  
 添加不兼容功能的组件负责将项目标记为不兼容。 该组件必须有权访问表示相关项目的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 接口。  
  
#### <a name="to-mark-a-project-as-incompatible"></a>将项目标记为不兼容  
  
1. 在该组件中，从全局服务 SVsSolution 获取 `IVsAppCompat` 接口。  
  
     有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> 。  
  
2. 在该组件中，调用 `IVsAppCompat.AskForUserConsentToBreakAssetCompat`，并向其传递一个表示相关项目的 `IVsHierarchy` 接口的数组。  
  
     此方法具有以下签名：  
  
    ```  
    HRESULT AskForUserConsentToBreakAssetCompat([in] SAFEARRAY(IVsHierarchy*) sarrProjectHierarchies)  
  
    ```  
  
     如果你实现此代码，则将出现项目兼容性对话框。 该对话框将会要求用户允许将所有指定项目标记为不兼容。 如果用户同意，则 `AskForUserConsentToBreakAssetCompat` 将返回 `S_OK`；否则 `AskForUserConsentToBreakAssetCompat` 将返回 `OLE_E_PROMPTSAVECANCELLED`。  
  
    > [!WARNING]
    > 在最常见的情况下， `IVsHierarchy` 数组将仅包含一个项。  
  
3. 如果 `AskForUserConsentToBreakAssetCompat` 返回 `S_OK`，则该组件将做出或接受破坏兼容性的更改。  
  
4. 在组件中，对每个想要标记为不兼容的项目调用 `IVsAppCompat.BreakAssetCompatibility` 方法。 该组件可以将参数 `lpszMinimumVersion` 的值设置为特定的最低版本，而不是让 Visual Studio 在注册表中查找当前版本字符串。 此方法以当时注册表中的内容为基础，将该组件将来无意设置较高值的风险降至最低。 如果设置了较高的值，则 Visual Studio 将无法打开该项目。  
  
     此方法具有以下签名：  
  
    ```  
    HRESULT BreakAssetCompatibility([in] IVsHierarchy * pProjHier), [in] LPCOLESTR lpszMinimumVersion);  
  
    ```  
  
     如果该组件将 `lpszMinimumVersion` 设置为 NULL，则 `BreakAssetCompatibility` 方法将调用 `IVsAppCompat.GetCurrentDesignTimeCompatVersion` 方法来获取表示当前 Visual Studio 版本的字符串。  
  
     此方法具有以下签名：  
  
    ```  
    HRESULT GetCurrentDesignTimeCompatVersion([out] BSTR * pbstrCurrentDesignTimeCompatVersion)  
    ```  
  
     BreakAssetCompatibility 方法随后调用 `IVsHierarchy.SetProperty` 方法，将根 `VSHPROPID_MinimumDesignTimeCompatVersion` 属性设置为你在上一步中获得的版本字符串的值。  
  
     有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A>。  
  
> [!IMPORTANT]
> 必须实现 `VSHPROPID_MinimumDesignTimeCompatVersion` 属性以将项目标记为兼容或不兼容。 例如，如果项目系统使用 MSBuild 项目文件，请向项目文件添加一个具有与相应 `<MinimumVisualStudioVersion>` 属性值的相等的值的生成属性 `VSHPROPID_MinimumDesignTimeCompatVersion` 。  
  
## <a name="detecting-whether-a-project-is-incompatible"></a>检测项目是否不兼容  
 必须阻止加载与当前版本的 Visual Studio 不兼容的项目。 而且，不能对不兼容的项目进行升级或修复。 因此，必须两次检查项目的兼容性：第一次在考虑进行升级或修复时，第二次在加载之前。  
  
 若要启用项目不兼容性的检测，则必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 方法。 如果项目不兼容，则 `UpgradeProject_CheckOnly` 必返回成功代码 `VS_S_INCOMPATIBLEPROJECT`，而 `CreateProject` 必返回错误代码 `VS_E_INCOMPATIBLEPROJECT`。 对于风格化项目，必须实现 `IVsProjectFlavorUpgradeViaFactory2.UpgradeProjectFlavor_CheckOnly` 而不是 `IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly`。  
  
 如果项目系统上构建了 Web、Office (VSTO)、Silverlight 或其他项目类型，则称该项目系统为风格化项目系统。 将继续支持已实现 `IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly` 的较旧项目系统和已实现 `IVsProjectFlavorUpgradeViaFactory.UpgradeProjectFlavor_CheckOnly` 的风格化项目系统。 较旧版本的 `IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly` 具有以下实现签名：  
  
```  
IVsProjectUpgradeViaFactory::UpgradeProject_CheckOnly(  
  
/* [in] */ BSTR bstrFileName,  
/* [in] */ IVsUpgradeLogger *pLogger,  
/* [out] */ BOOL *pUpgradeRequired,  
/* [out] */ GUID *pguidNewProjectFactory,  
/* [out] */ VSPUVF_FLAGS *pUpgradeProjectCapabilityFlags  
)  
```  
  
 如果此方法可将 `pUpgradeRequired` 设置为 TRUE 并返回 `S_OK`，则该结果将被视为“升级”，就像该方法向值 `VSPUVF_PROJECT_ONEWAYUPGRADE`设置了升级标志一样，本主题后面对此进行了描述。 使用此较旧方法支持下列返回值，但仅当 `pUpgradeRequired` 设置为 TRUE 时有效：  
  
1. `VS_S_PROJECT_SAFEREPAIRREQUIRED`。 此返回值等效于 `pUpgradeRequired` （本主题后面对其进行了描述），会将 `VSPUVF_PROJECT_SAFEREPAIR`值转换为 TRUE。  
  
2. `VS_S_PROJECT_UNSAFEREPAIRREQUIRED`。 此返回值等效于 `pUpgradeRequired` （本主题后面对此进行了描述），会将 `VSPUVF_PROJECT_UNSAFEREPAIR`值转换为 TRUE  
  
3. `VS_S_PROJECT_ONEWAYUPGRADEREQUIRED`。 此返回值等效于 `pUpgradeRequired` （本主题后面对其进行了描述），会将 `VSPUVF_PROJECT_ONEWAYUPGRADE`值转换为 TRUE。  
  
   `IVsProjectUpgradeViaFactory4` 和 `IVsProjectFlavorUpgradeViaFactory2` 中的新实现让你可以更精确地指定迁移类型。  
  
> [!NOTE]
> 可以缓存 `UpgradeProject_CheckOnly` 方法所进行兼容性检查的结果，以供对 `CreateProject`的后续调用使用。  
  
 例如，如果为带有 SP1 的 `UpgradeProject_CheckOnly` 项目系统编写的 `CreateProject` 和 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 方法检查项目文件并发现 `<MinimumVisualStudioVersion>` 版本属性为“11.0”，则带有 SP1 的 Visual Studio 2010 不会加载该项目。 此外，“解决方案导航器”  将指示该项目为“不兼容”，并且不会加载它。  
  
## <a name="BKMK_UpgradeLogger"></a> 升级记录器  
 对 `IVsProjectUpgradeViaFactory::UpgradeProject` 的调用包含 `IVsUpgradeLogger` 记录器，项目系统和风格将用其提供详细的升级跟踪记录以便故障排除。 如果记录到警告或错误，则 Visual Studio 将显示升级报告。  
  
 编写到升级记录器时，请考虑以下准则：  
  
- Visual Studio 将在所有项目完成升级后调用 Flush。 请勿在你的项目系统调用它。  
  
- LogMessage 函数具有以下 Errorlevel：  
  
  - 0 代表想要跟踪的任何信息。  

  - 1 代表警告。  

  - 2 代表错误  

  - 3 代表报告格式化程序。 项目升级后，记录一次“Converted”，请勿对此单词进行本地化。  
  
- 如果项目不需要任何修复或升级，则只有当项目系统在 UpgradeProject_CheckOnly 或 UpgradeProjectFlavor_CheckOnly 方法调用期间记录到警告或错误时，Visual Studio 才会生成日志文件。
