---
title: 上下文参数 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6673ad8f26c94165635b5f1bc652b91dcbbfd24f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709309"
---
# <a name="context-parameters"></a>上下文参数
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 中，您可以将向导添加到 **"新项目**"、**添加新项目**或**添加子项目**对话框。 添加的向导可在 **"文件"** 菜单上或通过右键单击**解决方案资源管理器**中的项目。 IDE 将上下文参数传递给向导的实现。 当 IDE 调用向导时，上下文参数定义项目的状态。

 IDE 通过在 IDE 对项目<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION><xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>方法的调用中设置标志来启动向导。 设置时，项目必须使用已注册的`IVsExtensibility::RunWizardFile`向导名称或 GUID 以及 IDE 传递给它的其他上下文参数来执行该方法。

## <a name="context-parameters-for-new-project"></a>新项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册向导类型<xref:EnvDTE.Constants.vsWizardNewProject>（ ） 或指示向导类型的 GUID。 在实现中[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]，向导的 GUID 是 {0F90E1D0-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目名称的字符串。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `InstallationDirectory` | 正在安装的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]目录路径。 |
| `FExclusive` | 表示项目应关闭打开的解决方案的布尔标志。 |
| `SolutionName` | 没有目录部分或 *.sln*扩展名的解决方案文件的名称。 *.suo*文件名也通过使用 创建`SolutionName`。 当此参数不是空字符串时，向导在使用<xref:EnvDTE._Solution.Create%2A><xref:EnvDTE._Solution.AddFromTemplate%2A>添加项目之前使用。 如果此名称为空字符串，请使用<xref:EnvDTE._Solution.AddFromTemplate%2A>而不调用<xref:EnvDTE._Solution.Create%2A>。 |
| `Silent` | 布尔，指示向导是否应以静默方式运行，就像单击 **"完成"** 一样`TRUE`（ 。 |

## <a name="context-parameters-for-add-new-item"></a>添加新项的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册向导类型<xref:EnvDTE.Constants.vsWizardAddItem>（ ） 或指示向导类型的 GUID。 在实现中[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]，向导的 GUID 是 {0F90E1D1-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目名称的字符串。 |
| `ProjectItems` | 包含工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称是默认文件名或用户从 **"添加项目"** 对话框中键入的文件名。 名称基于*在 .vsdir*文件中设置的标志。 名称可以是空值。 |
| `InstallationDirectory` | 正在安装的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]目录路径。 |
| `Silent` | 布尔，指示向导是否应以静默方式运行，就像单击 **"完成"** 一样`TRUE`（ 。 |

## <a name="context-parameters-for-add-sub-project"></a>添加子项目的上下文参数

| 参数 | 描述 |
|-------------------------| - |
| `WizardType` | 已注册向导类型<xref:EnvDTE.Constants.vsWizardAddSubProject>（ ） 或指示向导类型的 GUID。 在实现中[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]，向导的 GUID 是 {0F90E1D2-4999-11D1-B6D1-00A0C90F2744}。 |
| `ProjectName` | 作为唯一[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目名称的字符串。 |
| `ProjectItems` | 指向`ProjectItems`向导操作的集合。 此指针根据项目层次结构选择传递给向导。 用户通常选择一个文件夹，将项目放在其中，然后调用项目的 **"添加项目"** 对话框。 |
| `LocalDirectory` | 工作项目文件的本地位置。 |
| `ItemName` | 要添加的项的名称。 此名称是默认文件名或用户从 **"添加项目"** 对话框中键入的文件名。 名称基于*在 .vsdir*文件中设置的标志。 名称可以是空值。 |
| `InstallationDirectory` | 安装的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]目录路径。 |
| `Silent` | 布尔，指示向导是否应以静默方式运行，就像单击 **"完成"** 一样`TRUE`（ 。 |

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 （.vsz） 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
- [用于启动向导的上下文参数](https://msdn.microsoft.com/Library/051a10f4-9e45-4604-b344-123044f33a24)
