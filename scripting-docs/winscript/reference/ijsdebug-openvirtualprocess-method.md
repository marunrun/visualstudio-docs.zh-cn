---
title: IJsDebug：： OpenVirtualProcess 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJSDebug.OpenVirtualProcess
apilocation:
- jscript9diag.dll
ms.assetid: 5612bf1b-a4e3-4eaf-ac5e-c2e1f147c395
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3de39beb28a68ec3b8e0d76b17a7e914a464ecfe
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577750"
---
# <a name="ijsdebugopenvirtualprocess-method"></a>IJsDebug::OpenVirtualProcess 方法
用于创建新的虚拟进程对象的工厂方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OpenVirtualProcess(  
   DWORD processId,  
   UINT64 runtimeJsBaseAddress,  
   IJsDebugDataTarget *pDataTarget,  
   IJsDebugProcess **ppProcess  
);  
```  
  
#### <a name="parameters"></a>参数  
 `processId`  
 中要将调试器附加到的进程 Id。  
  
 `runtimeJsBaseAddress`  
 中JavaScript 运行时加载到目标进程中的基址。  
  
 `pDataTarget`  
 中调试器提供的用于查询进程状态的接口。  
  
 `ppProcess`  
 弄新建调试进程对象  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 如果 Jscript9diag 和 Jscript9.dll 不匹配，则返回 E_JsDEBUG_MISMATCHED_RUNTIME。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebug 接口](../../winscript/reference/ijsdebug-interface.md)