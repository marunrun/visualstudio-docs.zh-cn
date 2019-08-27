---
title: GenerateDeploymentManifest 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateDeploymentManifest
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateDeploymentManifest task
- GenerateDeploymentManifest task [MSBuild]
ms.assetid: 0734ebda-734d-49c4-9642-8d9d919d45fd
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6f0c13e5ea8778ca91c30383287aaad6e965bb65
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149602"
---
# <a name="generatedeploymentmanifest-task"></a>GenerateDeploymentManifest 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

生成 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署清单。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署清单描述如何通过为部署定义唯一标识、标识部署特征（如安装或联机模式）、指定应用程序更新设置和更新位置，以及指示相应的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序清单，来进行应用程序的部署。  
  
## <a name="parameters"></a>参数  
 下表描述了 `GenerateDeploymentManifest` 任务的参数。  
  
|参数|描述|  
|---------------|-----------------|  
|`AssemblyName`|可选 `String` 参数。<br /><br /> 指定生成的清单的程序集标识的 `Name` 字段。 如果未指定此参数，则从 `EntryPoint` 或 `InputManifest` 参数中推断名称。 如果无法推断名称，则任务将引发错误。|  
|`AssemblyVersion`|可选 `String` 参数。<br /><br /> 指定生成的清单的程序集标识的 `Version` 字段。 如果未指定此参数，则任务使用值“1.0.0.0”。|  
|`CreateDesktopShortcut`|可选 `Boolean` 参数。<br /><br /> 如果为 True，则将在安装 ClickOnce 应用程序过程中在桌面创建图标。|  
|`DeploymentUrl`|可选 `String` 参数。<br /><br /> 指定应用程序的更新位置。 如果未指定此参数，则不会为应用程序定义更新位置。 但是，如果 `UpdateEnabled` 参数为 `true`，则必须指定更新位置。 指定的值应为完全限定的 URL 或 UNC 路径。|  
|`Description`|可选 `String` 参数。<br /><br /> 指定应用程序的可选说明。|  
|`DisallowUrlActivation`|可选 `Boolean` 参数。<br /><br /> 指定当通过 URL 打开应用程序时是否应该自动运行该应用程序。 如果此参数为 `true`，则应用程序只能从“开始”菜单中启动。 此参数的默认值为 `false`。 仅当 `Install` 参数值为 `true` 时才应用此输入。|  
|`EntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指示生成的清单程序集的入口点。 对于 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署清单，此输入指定了 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序清单。<br /><br /> 在 [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] 中，[GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)要求具有 `EntryPoint` 才能生成应用程序清单。 （程序集或本机清单无需 `EntryPoint`。）此要求已强制执行并生成错误："MSB3185:未指定入口点的清单。"<br /><br /> 如果未指定 `EntryPoint` 任务参数，则 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 不会发出此错误。 相反，会将 \<customHostSpecified> 标记作为 \<entryPoint> 标记的子级插入，例如：<br /><br /> `<entryPoint xmlns="urn:schemas-`<br /><br /> `microsoft-com:asm.v2">`<br /><br /> `<co.v1:customHostSpecified />`<br /><br /> `</entryPoint>`<br /><br /> 通过执行以下步骤，可将 DDL 依赖项添加到应用程序清单：<br /><br /> 1.通过调用 <xref:Microsoft.Build.Tasks.ResolveAssemblyReference> 解析程序集引用。<br />2.将上一个任务的输出和程序集本身传递给 <xref:Microsoft.Build.Tasks.ResolveManifestFiles>。<br />3.使用 `Dependencies` 参数将依赖项传递给 <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>。|  
|`ErrorReportUrl`|可选 [String](<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) 参数。<br /><br /> 指定安装 ClickOnce 过程中显示在对话框中的网页 URL。|  
|`InputManifest`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指示输入 XML 文档，使其充当清单生成器的基础。 这使得结构化数据（如自定义清单定义）可反映在输出清单中。 XML 文档中的根元素必须是 asmv1 命名空间中的程序集节点。|  
|`Install`|可选 `Boolean` 参数。<br /><br /> 指定应用程序是已安装应用程序还是仅联机应用程序。 如果此参数为 `true`，则应用程序将安装在用户的“开始”菜单中，并可通过“添加或删除程序”对话框将其删除。 如果此参数为 `false`，则应用程序适用于在网页上联机使用。 此参数的默认值为 `true`。|  
|`MapFileExtensions`|可选 `Boolean` 参数。<br /><br /> 指定是否使用 .deploy 文件扩展名映射。 如果此参数为 `true`，则每个程序文件都使用 .deploy 文件扩展名发布。 此选项限制文件扩展名的数量（必须取消阻止这些文件扩展名，才能启用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序部署），有助于提升 Web 服务器安全性。 此参数的默认值为 `false`。|  
|`MaxTargetPath`|可选 `String` 参数。<br /><br /> 指定 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序部署中允许的最大文件路径长度。 如果指定此参数，则将针对此限制检查应用程序中每个文件路径的长度。 超出该限制的任何项都会导致一条生成警告。 如果此输入未指定或为零，则不会执行任何检查。|  
|`MinimumRequiredVersion`|可选 `String` 参数。<br /><br /> 指定用户是否可以跳过更新。 如果用户的版本低于所需的最低版本，则用户将无法选择跳过更新。 仅当 `Install` 参数的值为 `true` 时才应用此输入。|  
|`OutputManifest`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定所生成的输出清单文件的名称。 如果未指定此参数，则将从生成的清单的标识中推断输出文件的名称。|  
|`Platform`|可选 `String` 参数。<br /><br /> 指定应用程序的目标平台。 此参数可以具有下列值：<br /><br /> -   `AnyCPU`<br />-   `x86`<br />-   `x64`<br />-   `Itanium`<br /><br /> 默认值为 `AnyCPU`。|  
|`Product`|可选 `String` 参数。<br /><br /> 指定应用程序的名称。 如果未指定此参数，则将从生成的清单的标识中推断该名称。 该名称将用作“开始”菜单上的快捷名称，且将作为“添加或删除程序”对话框中显示的名称的一部分。|  
|`Publisher`|可选 `String` 参数。<br /><br /> 指定应用程序的发布者。 如果未指定此参数，则将从注册的用户或生成的清单的标识中推断该名称。 该名称将用作“开始”菜单上的文件夹名称，且将作为“添加或删除程序”对话框中显示的名称的一部分。|  
|`SuiteNamel`|可选 `String` 参数。<br /><br /> 指定在完成 ClickOnce 部署后，“开始”菜单上应用程序所在文件夹的名称。|  
|`SupportUrl`|可选 `String` 参数。<br /><br /> 指定在“添加或删除程序”对话框中为应用程序显示的链接。 指定的值应为完全限定的 URL 或 UNC 路径。|  
|`TargetCulture`|可选 `String` 参数。<br /><br /> 标识应用程序的区域性，并指定生成的清单的程序集标识的 `Language` 字段。 如果未指定此参数，则会假定该应用程序的区域性是固定的。|  
|`TrustUrlParameters`|可选 `Boolean` 参数。<br /><br /> 指定是否应使 URL 查询字符串参数对应用程序可用。 此参数的默认值为 `false`，表示参数不可用于应用程序。|  
|`UpdateEnabled`|可选 `Boolean` 参数。<br /><br /> 指示应用程序是否启用更新。 此参数的默认值为 `false`。 仅当 `Install` 参数的值为 `true` 时才应用此参数。|  
|`UpdateInterval`|可选 `Int32` 参数。<br /><br /> 指定应用程序的更新间隔。 此参数的默认值为零。 仅当 `Install` 和 `UpdateEnabled` 参数的值都为 `true` 时才应用此参数。|  
|`UpdateMode`|可选 `String` 参数。<br /><br /> 指定是在应用程序启动之前在前台检查更新，还是在应用程序运行时在后台检查更新。 此参数可以具有下列值：<br /><br /> -   `Foreground`<br />-   `Background`<br /><br /> 此参数的默认值为 `Background`。 仅当 `Install` 和 `UpdateEnabled` 参数的值都为 `true` 时才应用此参数。|  
|`UpdateUnit`|可选 `String` 参数。<br /><br /> 指定 `UpdateInterval` 参数的单位。 此参数可以具有下列值：<br /><br /> -   `Hours`<br />-   `Days`<br />-   `Weeks`<br /><br /> 仅当 `Install` 和 `UpdateEnabled` 参数的值都为 `true` 时才应用此参数。|  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.GenerateManifestBase> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关任务类的参数列表，请参阅[任务基类](../msbuild/task-base-class.md)。  
  
## <a name="see-also"></a>请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)   
 [SignFile 任务](../msbuild/signfile-task.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
