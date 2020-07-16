---
title: IDebugProgram2：： Execute |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 676a3a7d184c1f34cafcfc2b2a4dd7a1c3f81a95
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387325"
---
# <a name="idebugprogram2execute"></a>IDebugProgram2::Execute
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

继续从停止状态运行该程序。 任何以前的执行状态（如步骤）都将被清除，程序将重新开始执行。  
  
> [!NOTE]
> 不推荐使用此方法。 改为使用[Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Execute(  
   void  
);  
```  
  
```csharp  
int Execute();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 当用户在其他程序的线程中从停止状态开始执行时，将对此程序调用此方法。 当用户从 IDE 的 "**调试**" 菜单中选择 "**启动**" 命令时，也会调用此方法。 此方法的实现可能与调用程序中当前线程上的[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)方法非常简单。  
  
> [!WARNING]
> 处理此调用时，不要将停止事件或即时（同步）事件发送到[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md);否则，调试器可能会停止响应。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [引发](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)
