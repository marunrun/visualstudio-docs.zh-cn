---
title: 自定义参数 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cd52a49daa7d57a21d8cb0896f7108efa09e32b2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708937"
---
# <a name="custom-parameters"></a>自定义参数
自定义参数控制向导启动后向导的操作。 相关的 *.vsz*文件提供由集成开发环境 （IDE） 打包的用户定义参数数组，并在向导启动时作为字符串数组传递给向导。 然后，向导分析字符串数组，并使用信息来控制向导的实际操作。 这样，向导可以根据 *.vsz*文件的内容自定义功能。

 上下文参数，另一方面，定义项目的状态，当向导启动。 有关详细信息，请参阅[上下文参数](../../extensibility/internals/context-parameters.md)。

 下面是具有自定义参数的 *.vsz*文件的示例：

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 *.vsz*文件的作者添加参数的值。 当用户在 **"文件**"菜单上选择 **"新项目**"或 **"添加新项目**"时，或通过右键单击**解决方案资源管理器**中的项目，IDE 将这些值收集到字符串数组中。 然后，IDE 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A><xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>标志集调用项目的方法，项目调用负责运行向导并返回结果<xref:EnvDTE.IVsExtensibility.RunWizardFile%2A>的方法。

 向导负责分析字符串数组并适当地对字符串进行操作。 通过这种方式，通过实现自定义参数，您可以创建一个执行各种功能的向导。 换句话说，一个向导可以有三个不同的 *.vsz*文件。 每个文件传递不同的自定义参数集，以控制向导在各种情况下的行为。

 有关详细信息，请参阅向导[（.vsz） 文件](../../extensibility/internals/wizard-dot-vsz-file.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 （.vsz） 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
