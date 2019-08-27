---
title: 自定义参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1a595861be835ec1aaa7079b3e3fe1962d5055e9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154996"
---
# <a name="custom-parameters"></a>自定义参数
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

启动向导后，自定义参数控制操作的向导。 相关的.vsz 文件提供了集成的开发环境 (IDE) 通过打包并启动该向导时作为一个字符串数组传递到向导的用户定义参数的数组。 向导然后分析的字符串数组，并使用这些信息来控制实际操作的向导。 以这种方式，具体取决于.vsz 文件的内容的功能可以自定义向导。  
  
 启动向导，上下文参数，但是，定义项目的状态。 有关详细信息，请参阅[上下文参数](../../extensibility/internals/context-parameters.md)。  
  
 下面是一个具有自定义参数的.vsz 文件的示例：  
  
```  
VSWIZARD 8.0  
Wizard=VsWizard.VsWizard_Engine  
Param="WIZARD_NAME = Sample Wizard"  
Param="WIZARD_UI = FALSE"  
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"  
Param="PREPROCESS_FUNCTION = CanAddATLSupport"  
Param="PROJECT_TYPE = CSPROJ"  
```  
  
 .Vsz 文件的作者添加了参数的值。 如果用户选择**新的项目**或**添加新项**文件菜单或通过右键单击项目中的**解决方案资源管理器**，IDE 将这些值收集到的数组字符串。 IDE 然后调用项目的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>方法替换<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>标记集和项目调用<xref:EnvDTE.IVsExtensibility.RunWizardFile%2A>负责运行该向导并返回结果的方法。  
  
 该向导负责分析的字符串数组并相应地作用于字符串。 在这种方式，通过实现自定义参数可以创建一个向导执行各种功能。 换而言之，一个向导无法具有三个不同的.vsz 文件。 每个文件将传递不同的自定义的参数来控制在各种情况下向导行为集。  
  
 有关详细信息，请参阅[向导 (。在 Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>   
 [上下文参数](../../extensibility/internals/context-parameters.md)   
 [向导](../../extensibility/internals/wizards.md)   
 [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
