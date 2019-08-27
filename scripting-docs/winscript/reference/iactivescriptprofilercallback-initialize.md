---
title: IActiveScriptProfilerCallback::Initialize | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.Initialize
apilocation:
- scrobj.dll
ms.assetid: a257111e-a50b-4962-9dd6-c893d40f6985
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 66ef6dc37e1f2f8117e440089ee36958d616dda0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993353"
---
# <a name="iactivescriptprofilercallbackinitialize"></a>IActiveScriptProfilerCallback::Initialize
每当调用以初始化探查器对象对脚本引擎开始分析。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Initialize(  
    [in] DWORD dwContext);  
```  
  
#### <a name="parameters"></a>参数  
 `dwContext`  
 [in]一个 4 字节值，传递给[IActiveScriptProfilerControl::StartProfiling](../../winscript/reference/iactivescriptprofilercontrol-startprofiling.md)。  
  
## <a name="return-value"></a>返回值  
 返回一个 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 如果该方法不能初始化探查器对象，它应返回失败 HRESULT 通知脚本引擎。 在这种情况下，脚本引擎应直接调用[IActiveScriptProfilerCallback::Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)、 将 HRESULT 传递的参数中，然后释放探查器对象。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)