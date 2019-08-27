---
title: IDebugProgramEx2::Attach | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4fe729f2fc196380a3db1a60d1c32f62bbd70998
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439158"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将会话附加到的程序。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Attach(   
   IDebugEventCallback2* pCallback,  
   DWORD                 dwReason,  
   IDebugSession2*       pSession  
);  
```  
  
```  
[C#]  
int Attach(   
   IDebugEventCallback2 pCallback,  
   uint                 dwReason,  
   IDebugSession2       pSession  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pCallback`  
 [in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象，表示附加的调试引擎将事件发送到回调函数。  
  
 `dwReason`  
 [in]中的值[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)介绍了在附加操作的原因的枚举。  
  
 `pSession`  
 [in]一个值，唯一标识将附加到程序的会话。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则返回错误代码。 此方法应返回`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`如果程序已附加。  
  
## <a name="remarks"></a>备注  
 包含的程序的端口可以使用中的值`pSession`以确定哪个会话正在尝试将附加到该程序。 例如，如果一个端口允许只有一个调试会话以一次附加到进程，该端口可以确定是否同一个会话已附加到进程中其他程序。  
  
> [!NOTE]
> 接口传入`pSession`仅视为 cookie 中，用于唯一标识会话调试管理器将附加到此程序; 的值上提供的接口的方法不起作用。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
