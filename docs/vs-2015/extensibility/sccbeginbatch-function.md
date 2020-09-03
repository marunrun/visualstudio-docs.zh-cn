---
title: SccBeginBatch 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 264d9057bf4f17281d6d8a16ed3a6794004e0e21
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189558"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数启动源代码管理操作的批处理序列。 将调用 [SccEndBatch](../extensibility/sccendbatch-function.md) 以结束批处理。 这些批处理不能嵌套。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccBeginBatch(void);  
```  
  
#### <a name="parameters"></a>参数  
 无。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|成功的批处理操作。|  
|SCC_E_UNKNOWNERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 源代码管理批处理用于在多个项目或多个上下文中执行相同的操作。 批处理可用于消除批处理操作期间用户体验中的冗余每个项目对话框。 `SccBeginBatch`函数和[SccEndBatch](../extensibility/sccendbatch-function.md)用作函数对，用于指示操作的开始和结束。 它们不能嵌套。 `SccBeginBatch` 设置一个标志，指示正在进行批处理操作。  
  
 批处理操作生效时，源代码管理插件最多应向用户显示一个对话框，并在所有后续操作上应用该对话框的响应。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccEndBatch](../extensibility/sccendbatch-function.md)
