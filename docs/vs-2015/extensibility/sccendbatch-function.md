---
title: SccEndBatch 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccEndBatch
helpviewer_keywords:
- SccEndBatch function
ms.assetid: 100e7833-fe0a-45c0-9fca-3e61fd1165b7
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 986056b1f5202c2fb94d27a8792ed3b0fe308944
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200140"
---
# <a name="sccendbatch-function"></a>SccEndBatch 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数最后一批的源代码管理操作。 这些批不能嵌套。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccEndBatch(void);  
```  
  
#### <a name="parameters"></a>参数  
 无。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|一批操作已成功结束。|  
|SCC_E_UNKNOWNERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 使用源控制批处理跨多个项目或多个上下文中执行相同的源代码管理操作。 若要在批处理操作期间消除冗余的对话框中，从用户体验，可以使用批处理。 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)和`SccEndBatch`函数用作一个对，以指示的开头和结尾的操作。 它们不能嵌套。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
