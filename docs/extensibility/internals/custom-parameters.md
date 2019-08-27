---
title: 自定义参数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a879c7a842bdabff396fa2df31d0aa7326b19c50
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312216"
---
# <a name="custom-parameters"></a>自定义参数
启动向导后，自定义参数控制操作的向导。 相关 *.vsz*文件提供了一系列集成的开发环境 (IDE) 通过打包并启动该向导时作为一个字符串数组传递到向导的用户定义参数。 向导然后分析的字符串数组，并使用这些信息来控制实际操作的向导。 在这种方式，向导可以自定义功能，具体取决于的内容 *.vsz*文件。

 启动向导，上下文参数，但是，定义项目的状态。 有关详细信息，请参阅[上下文参数](../../extensibility/internals/context-parameters.md)。

 下面是举例 *.vsz*具有自定义参数文件：

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 一书的作者 *.vsz*文件添加参数的值。 如果用户选择**新的项目**或**添加新项**上**文件**菜单或通过右键单击项目中的**解决方案资源管理器**，IDE将这些值收集到一个字符串数组。 IDE 然后调用项目的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>方法替换<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>标记集和项目调用<xref:EnvDTE.IVsExtensibility.RunWizardFile%2A>负责运行该向导并返回结果的方法。

 该向导负责分析的字符串数组并相应地作用于字符串。 在这种方式，通过实现自定义参数可以创建一个向导执行各种功能。 换而言之，一个向导可以有三个不同 *.vsz*文件。 每个文件将传递不同的自定义的参数来控制在各种情况下向导行为集。

 有关详细信息，请参阅[向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)