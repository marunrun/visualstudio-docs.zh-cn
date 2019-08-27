---
title: IActiveScript::GetScriptThreadID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptThreadID
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptThreadID
ms.assetid: 2595d76e-30b5-429f-88b4-1d026645dd9b
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d329e08e6a17d9edcdf26e14b468c3c56f036c00
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935687"
---
# <a name="iactivescriptgetscriptthreadid"></a>IActiveScript::GetScriptThreadID
检索与给定的 Win32 线程关联的线程的脚本引擎定义标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptThreadID(  
    DWORD dwWin32ThreadID,       // Win32 thread identifier.  
    SCRIPTTHREADID *pstidThread  // Receives scripting thread. identifier  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwWin32ThreadID` ,  
 [in]当前进程中正在运行的 Win32 线程的线程标识符。 使用[IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)函数可检索当前正在执行的线程的线程标识符。  
  
 `pstidThread` ,  
 [out]一个变量来接收与给定的 Win32 线程关联的脚本线程标识符的地址。 此标识符的解释为从左到脚本引擎，但它可以只是一份 Windows 线程标识符。 请注意，如果 Win32 线程终止，此标识符将成为未分配，随后可能分配给另一个线程。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化），因此失败。|  
  
## <a name="remarks"></a>备注  
 检索到的标识符可以如对脚本线程执行控制方法的后续调用中使用[iactivescript:: Interruptscriptthread](../../winscript/reference/iactivescript-interruptscriptthread.md)方法。  
  
 此方法可以从非基础线程调用不会导致到主机对象或一个非基本标注[iactivescript:: Interruptscriptthread](../../winscript/reference/iactivescript-interruptscriptthread.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)