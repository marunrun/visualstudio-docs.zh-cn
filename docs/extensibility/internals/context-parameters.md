---
title: 上下文参数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ea38b79be362f78fcc34161a480597fb0ecce40
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72727551"
---
# <a name="context-parameters"></a>上下文参数
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境（IDE）中，可以将向导添加到 "**新建项目**"、"**添加新项**" 或 "**添加子项目**" 对话框中。 添加的向导位于 "**文件**" 菜单上，或右键单击 "**解决方案资源管理器**中的项目。 IDE 将上下文参数传递到向导实现。 上下文参数定义在 IDE 调用向导时项目的状态。

 IDE 将启动向导，方法是将 IDE 调用中的 <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> 标志设置为项目的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> 方法。 如果设置此参数，项目必须使用注册的向导名称或 GUID 以及 IDE 传递给它的其他上下文参数来执行 `IVsExtensibility::RunWizardFile` 方法。

## <a name="context-parameters-for-new-project"></a>新项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册向导类型（<xref:EnvDTE.Constants.vsWizardNewProject>）或指示向导类型的 GUID。 在 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 实现中，向导的 GUID 为 {0F90E1D0-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目名称的字符串。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `InstallationDirectory` | 安装 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的目录路径。 |
| `FExclusive` | 布尔型标志，指示项目应关闭打开的解决方案。 |
| `SolutionName` | 解决方案文件的名称，不含目录部分或 *.sln*扩展名。 *.Suo*文件名也是使用 `SolutionName` 创建的。 如果此参数不是空字符串，则向导将使用 <xref:EnvDTE._Solution.Create%2A>，然后将项目添加 <xref:EnvDTE._Solution.AddFromTemplate%2A>。 如果此名称为空字符串，请使用 <xref:EnvDTE._Solution.AddFromTemplate%2A>，而不调用 <xref:EnvDTE._Solution.Create%2A>。 |
| `Silent` | 布尔值，指示向导是否应以无提示方式运行，就好像单击了**finish** （`TRUE`）。 |

## <a name="context-parameters-for-add-new-item"></a>添加新项的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册向导类型（<xref:EnvDTE.Constants.vsWizardAddItem>）或指示向导类型的 GUID。 在 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 实现中，向导的 GUID 为 {0F90E1D1-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目名称的字符串。 |
| `ProjectItems` | 包含工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称可以是默认文件名，也可以是用户在 "**添加项**" 对话框中键入的文件名。 此名称基于在*vsdir*文件中设置的标志。 名称可以为 null 值。 |
| `InstallationDirectory` | 安装 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的目录路径。 |
| `Silent` | 布尔值，指示向导是否应以无提示方式运行，就好像单击了**finish** （`TRUE`）。 |

## <a name="context-parameters-for-add-sub-project"></a>添加子项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册向导类型（<xref:EnvDTE.Constants.vsWizardAddSubProject>）或指示向导类型的 GUID。 在 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 实现中，向导的 GUID 为 {0F90E1D2-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目名称的字符串。 |
| `ProjectItems` | 指向向导操作 `ProjectItems` 集合的指针。 此指针将根据项目层次结构选择传递到向导。 用户通常会选择要在其中放置项的文件夹，然后调用项目的 "**添加项**" 对话框。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称可以是默认文件名，也可以是用户在 "**添加项**" 对话框中键入的文件名。 此名称基于在*vsdir*文件中设置的标志。 名称可以为 null 值。 |
| `InstallationDirectory` | @No__t_0 安装的目录路径。 |
| `Silent` | 布尔值，指示向导是否应以无提示方式运行，就好像单击了**finish** （`TRUE`）。 |

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导（.vsz）文件](../../extensibility/internals/wizard-dot-vsz-file.md)
- [用于启动向导的上下文参数](https://msdn.microsoft.com/Library/051a10f4-9e45-4604-b344-123044f33a24)