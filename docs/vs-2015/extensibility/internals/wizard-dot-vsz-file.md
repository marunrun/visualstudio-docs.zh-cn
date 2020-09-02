---
title: 向导 (。.Vsz) 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ab1adde4c7018f136f47769e16a8ce2fedf72c93
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687662"
---
# <a name="wizard-vsz-file"></a>向导 (.Vsz) 文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

集成开发环境 (IDE) 使用 .vsz 文件来启动向导。 这些 .vsz 文件包含 IDE 用于确定要调用哪个向导以及要传递到向导的信息的信息。  
  
 .Vsz 文件是 .ini 格式文本文件中没有节的版本。 IDE 已知的信息存储在文件的开头。 这提供了 IDE 所调用的向导与要传递到 IDE 的 .vsz 文件中的参数之间的链接。 文件的其余部分提供特定于向导的参数，这些参数由 IDE 收集并传递给特定向导。  
  
 下面的示例显示 .vsz 文件的内容。  
  
```  
VSWizard 8.0  
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}  
Param="WIZARDNAME = Wizard One"  
Param="WIZARDUI = FALSE"  
```  
  
 下面是 .vsz 文件中的部分。  
  
|组成部分|说明|  
|----------|-----------------|  
|VSWizard|文件中的第一个参数是模板文件格式的版本号。 此版本号必须是6.0、7.0、7.1 或8.0。 其他数字无法启动并导致无效格式错误。|  
|向导|此字段包含向导的 OLE ProgID，或者是 IDE cocreated 的向导 CLSID 的 GUID 字符串表示形式。|  
|Param|这些部分是可选的。 你可以根据需要添加多个。|  
  
 使用参数，.vsz 文件可以将其他自定义参数传递给该向导。 每个值作为变量数组中的字符串元素传递到向导。 有关详细信息，请参阅 [自定义参数](../../extensibility/internals/custom-parameters.md)。 有关如何在自定义向导开发中使用 .vsz 文件的信息，请参阅 [。.Vsz 文件 (项目控件) ](https://msdn.microsoft.com/library/b8678fee-6795-46d1-9338-48b22d5e9207)  
  
 若要将默认区域设置 ID 添加到 .vsz 文件，请指定 `FALLBACK_LCID` = xxxx，其中 xxxx 是区域设置 id，例如，1033表示英语。 `FALLBACK_LCID`定义参数时，如果未找到当前 ID，向导将使用提供的回退区域设置 ID。  
  
## <a name="see-also"></a>另请参阅  
 [自定义参数](../../extensibility/internals/custom-parameters.md)   
 [向导](../../extensibility/internals/wizards.md)   
 [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
