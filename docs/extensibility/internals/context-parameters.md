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
ms.openlocfilehash: 1ddbd8084da150e47fdbe350770ea5e6bdb7e28d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335598"
---
# <a name="context-parameters"></a>上下文参数
在中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE) 中，您可以添加到向导**新建项目**，**添加新项**，或**添加子项目**对话框。 添加了的向导位于**文件**菜单或通过右键单击项目中的**解决方案资源管理器**。 IDE 将上下文参数传递给该向导的实现。 IDE 调用向导时，上下文参数定义项目的状态。

 在 IDE 启动向导，通过设置<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>对 IDE 的调用中的标志<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>项目的方法。 设置时，项目必须导致`IVsExtensibility::RunWizardFile`方法要执行的使用已注册的向导名称或 GUID 和其他 IDE 将传递给它的上下文参数。

## <a name="context-parameters-for-new-project"></a>用于新的项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册的向导类型 (<xref:EnvDTE.Constants.vsWizardNewProject>) 或 GUID，该值指示类型的向导。 在[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]实现，该向导的 GUID 是 {0F90E1D0-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 是唯一的字符串[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目名称。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `InstallationDirectory` | 目录路径的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]是安装。 |
| `FExclusive` | 布尔标志，指示该项目应关闭打开的解决方案。 |
| `SolutionName` | 而无需目录部分的解决方案文件的名称或 *.sln*扩展。 *.Suo*还通过使用创建文件名称`SolutionName`。 当此参数不为空字符串时，该向导将使用<xref:EnvDTE._Solution.Create%2A>然后再添加具有项目<xref:EnvDTE._Solution.AddFromTemplate%2A>。 如果此名称为空字符串，请使用<xref:EnvDTE._Solution.AddFromTemplate%2A>而无需调用<xref:EnvDTE._Solution.Create%2A>。 |
| `Silent` | 一个布尔值，该值指示是否应以无提示方式运行向导如同**完成**已单击过 (`TRUE`)。 |

## <a name="context-parameters-for-add-new-item"></a>用于添加新项的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册的向导类型 (<xref:EnvDTE.Constants.vsWizardAddItem>) 或 GUID，该值指示类型的向导。 在[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]实现，该向导的 GUID 是 {0F90E1D1-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 是唯一的字符串[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目名称。 |
| `ProjectItems` | 包含工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称是默认文件名称或从用户键入的文件名**添加的项**对话框。 名称基于中设置的标志 *.vsdir*文件。 名称可以是 null 值。 |
| `InstallationDirectory` | 目录路径的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]是安装。 |
| `Silent` | 一个布尔值，该值指示是否应以无提示方式运行向导如同**完成**已单击过 (`TRUE`)。 |

## <a name="context-parameters-for-add-sub-project"></a>添加子项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册的向导类型 (<xref:EnvDTE.Constants.vsWizardAddSubProject>) 或 GUID，该值指示类型的向导。 在[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]实现，该向导的 GUID 是 {0F90E1D2-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 是唯一的字符串[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目名称。 |
| `ProjectItems` | 指向`ProjectItems`向导进行操作的集合。 此指针传递给向导基于对项目层次结构所选内容。 用户通常会选择在其中放入该项目的文件夹，然后调用项目的**添加项**对话框。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称是默认文件名称或从用户键入的文件名**添加的项**对话框。 名称基于中设置的标志 *.vsdir*文件。 名称可以是 null 值。 |
| `InstallationDirectory` | 目录路径的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]安装。 |
| `Silent` | 一个布尔值，该值指示是否应以无提示方式运行向导如同**完成**已单击过 (`TRUE`)。 |

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
- [用于启动向导的上下文参数](https://msdn.microsoft.com/Library/051a10f4-9e45-4604-b344-123044f33a24)