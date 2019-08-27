---
title: IJsDebugDataTarget Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a9b784d6-958f-4d55-b3f6-c2d6b260a16b
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3cbb4b0b54fb9a3821d3033ef0e65fd0bafbc246
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62582493"
---
# <a name="ijsdebugdatatarget-interface"></a>IJsDebugDataTarget 接口
由调试器提供功能来访问和更改目标调试器进程的状态的实现。  
  
## <a name="syntax"></a>语法  
  
```cpp
IJsDebugDataTarget : public IUnknown;  
```  
  
## <a name="members"></a>成员  
  
### <a name="public-methods"></a>公共方法  
  
|名称|描述|  
|----------|-----------------|  
|[IJsDebugDataTarget::AllocateVirtualMemory 方法](../../winscript/reference/ijsdebugdatatarget-allocatevirtualmemory-method.md)|释放和/或提交目标过程虚拟地址空间内的内存区域。|  
|[IJsDebugDataTarget::CreateStackFrameEnumerator 方法](../../winscript/reference/ijsdebugdatatarget-createstackframeenumerator-method.md)|创建堆栈帧的枚举器。|  
|[IJsDebugDataTarget::FreeVirtualMemory 方法](../../winscript/reference/ijsdebugdatatarget-freevirtualmemory-method.md)|释放和/或解除目标过程虚拟地址空间内的内存区域。|  
|[IJsDebugDataTarget::GetThreadContext 方法](../../winscript/reference/ijsdebugdatatarget-getthreadcontext-method.md)|给定线程的检索上下文。|  
|[IJsDebugDataTarget::GetTlsValue 方法](../../winscript/reference/ijsdebugdatatarget-gettlsvalue-method.md)|有关正在调试的线程，检索指定的 TLS 索引的线程本地存储 (TLS) 槽中的值。|  
|[IJsDebugDataTarget::ReadBSTR 方法](../../winscript/reference/ijsdebugdatatarget-readbstr-method.md)|从调试目标中读取 BSTR。|  
|[IJsDebugDataTarget::ReadMemory 方法](../../winscript/reference/ijsdebugdatatarget-readmemory-method.md)|读取目标进程的内存。|  
|[IJsDebugDataTarget::ReadNullTerminatedString 方法](../../winscript/reference/ijsdebugdatatarget-readnullterminatedstring-method.md)|从目标读取指定的数量的字符。|  
|[IJsDebugDataTarget::WriteMemory 方法](../../winscript/reference/ijsdebugdatatarget-writememory-method.md)|读取目标进程的内存。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)