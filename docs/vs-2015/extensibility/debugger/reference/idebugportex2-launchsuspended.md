---
title: IDebugPortEx2：： LaunchSuspended |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortEx2::LaunchSuspended
helpviewer_keywords:
- IDebugPortEx2::LaunchSuspended
ms.assetid: 34b2cf99-2e52-4757-8969-1d12ac517ec0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3c5e57c003257650f5ca60d4a7c3d9becea3e776
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188460"
---
# <a name="idebugportex2launchsuspended"></a>IDebugPortEx2::LaunchSuspended
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

启动可执行文件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT LaunchSuspended(   
   LPCOLESTR        pszExe,  
   LPCOLESTR        pszArgs,  
   LPCOLESTR        pszDir,  
   BSTR             bstrEnv,  
   DWORD            hStdInput,  
   DWORD            hStdOutput,  
   DWORD            hStdError,  
   IDebugProcess2** ppPortProcess  
);  
```  
  
```csharp  
int LaunchSuspended(   
   string             pszExe,  
   string             pszArgs,  
   string             pszDir,  
   string             bstrEnv,  
   uint               hStdInput,  
   uint               hStdOutput,  
   uint               hStdError,  
   out IDebugProcess2 ppPortProcess  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszExe`  
 中要启动的可执行文件的名称。 此路径可以是完整路径，也可以是在参数中指定的工作目录 `pszDir` 。  
  
 `pszArgs`  
 中要传递给可执行文件的参数。 如果没有参数，则可以为 null 值。  
  
 `pszDir`  
 中可执行文件使用的工作目录的名称。 如果不需要任何工作目录，则可以为 null 值。  
  
 `bstrEnv`  
 中以 null 结尾的字符串的环境块，后跟一个其他 NULL 终止符。  
  
 `hStdInput`  
 中替代输入流的句柄。 如果不需要重定向，则可以为0。  
  
 `hStdOutput`  
 中备用输出流的句柄。 如果不需要重定向，则可以为0。  
  
 `hStdError`  
 中备用错误输出流的句柄。 如果不需要重定向，则可以为0。  
  
 `ppPortProcess`  
 弄返回一个 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 对象，该对象表示已启动的进程。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法应启动进程，使其挂起并且不运行任何代码。 调用 [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md) 方法以恢复进程。  
  
 还可以从调试引擎启动程序。 有关详细信息，请参阅 [启动程序](../../../extensibility/debugger/launching-a-program.md)。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)   
 [启动程序](../../../extensibility/debugger/launching-a-program.md)
