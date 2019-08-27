---
title: IMachineDebugManager::EnumApplications |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManager.EnumApplications
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManager::EnumApplications
ms.assetid: 5d833db4-fd9b-4e61-bebb-130faede5a77
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8a75af7e151ad233e1bd592203fb33d2cd7f5cbe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977586"
---
# <a name="imachinedebugmanagerenumapplications"></a>IMachineDebugManager::EnumApplications
返回当前正在运行的应用程序的列表的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumApplications(  
   IEnumRemoteDebugApplications**  ppeda  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppeda`  
 [out]包含正在运行的应用程序的当前列表的枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回当前正在运行的应用程序的列表的枚举器。 调试器 IDE 使用此方法来显示和附加以便进行调试的应用程序。  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManager 接口](../../winscript/reference/imachinedebugmanager-interface.md)