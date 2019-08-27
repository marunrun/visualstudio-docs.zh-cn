---
title: IProcessDebugManager::GetDefaultApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.GetDefaultApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::GetDefaultApplication
ms.assetid: 6c991faa-ea40-4d18-a1b8-6e7d0de6dd43
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6fec84a60863b426f2f65c26e2375262b109d635
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953967"
---
# <a name="iprocessdebugmanagergetdefaultapplication"></a>IProcessDebugManager::GetDefaultApplication
返回当前进程的默认应用程序对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDefaultApplication(  
   IDebugApplication**  ppda  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppda`  
 [out]此应用程序的的调试应用程序的对象。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法创建新的调试应用程序对象，并将其添加到运行的应用程序列表中，如有必要。  
  
 语言引擎应使用指定的应用程序`GetDefaultApplication`方法如果它们不提供应用程序的主机上运行。  
  
## <a name="see-also"></a>请参阅  
 [IProcessDebugManager 接口](../../winscript/reference/iprocessdebugmanager-interface.md)