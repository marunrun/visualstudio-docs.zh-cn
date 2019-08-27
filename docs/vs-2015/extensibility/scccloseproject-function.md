---
title: SccCloseProject 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccCloseProject
helpviewer_keywords:
- SccCloseProject function
ms.assetid: 259c2069-d349-4814-810f-1c3151b7fb84
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7d2364215f528f16d05ecf0c53b152f7334f4b4a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156133"
---
# <a name="scccloseproject-function"></a>SccCloseProject 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数用于关闭特定会话的结束标记的项目。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccCloseProject (  
   LPVOID pvContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 源控制插件上下文结构。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|已成功关闭该项目。|  
|SCC_E_PROJNOTOPEN|不没有当前打开任何项目。|  
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|  
|SCC_E_NONSPECIFICERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 [SccOpenProject](../extensibility/sccopenproject-function.md)始终调用此函数之前。 对此函数的调用后跟调用`SccOpenProject`函数或[SccUninitialize](../extensibility/sccuninitialize-function.md)，以便完全结束与源代码管理系统的连接。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)
