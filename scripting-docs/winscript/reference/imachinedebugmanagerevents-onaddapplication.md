---
title: IMachineDebugManagerEvents::onAddApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManagerEvents.onAddApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManagerEvents::onAddApplication
ms.assetid: 00a54b91-36d5-430d-b654-5e2abe5300cd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f063e36296d6a5a77208bac2fe533274a6f9c07f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62965784"
---
# <a name="imachinedebugmanagereventsonaddapplication"></a>IMachineDebugManagerEvents::onAddApplication
处理事件时应用程序添加到正在运行的应用程序列表。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onAddApplication(  
   IRemoteDebugApplication*  pda,  
   DWORD                     dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pda`  
 [in]已添加到正在运行的应用程序的应用程序列表。  
  
 `dwAppCookie`  
 [in]应用程序已添加到应用程序列表时提供的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法指示应用程序已添加到正在运行的应用程序列表。  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManagerEvents 接口](../../winscript/reference/imachinedebugmanagerevents-interface.md)   
 [IMachineDebugManagerEvents::onRemoveApplication](../../winscript/reference/imachinedebugmanagerevents-onremoveapplication.md)