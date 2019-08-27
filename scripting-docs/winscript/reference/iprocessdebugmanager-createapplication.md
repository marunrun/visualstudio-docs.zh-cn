---
title: IProcessDebugManager::CreateApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.CreateApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::CreateApplication
ms.assetid: d6b646f2-8af0-445c-ae7e-a9772042b3a1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 10d7f2246b327393a810170f5b133f2885186c3a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944809"
---
# <a name="iprocessdebugmanagercreateapplication"></a>IProcessDebugManager::CreateApplication
创建一个新的调试应用程序对象，此应用程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateApplication(  
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
 此方法创建的对象没有名称且未添加到正在运行的应用程序列表。 使用`IProcessDebugManager::AddApplication`若要添加到应用程序列表的调试应用程序。  
  
## <a name="see-also"></a>请参阅  
 [IProcessDebugManager 接口](../../winscript/reference/iprocessdebugmanager-interface.md)   
 [IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)