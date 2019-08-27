---
title: IActiveScript | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScript interface
ms.assetid: d8acee11-7f0d-4999-b97a-66774af16f71
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5b7e3a0172a798eab9a743f446dff3d339a785b2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436085"
---
# <a name="iactivescript"></a>IActiveScript
提供初始化脚本引擎所需的方法。 脚本引擎必须实现`IActiveScript`接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScript::SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md)|通知的脚本引擎[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)由主机提供的站点。|  
|[IActiveScript::GetScriptSite](../../winscript/reference/iactivescript-getscriptsite.md)|检索与 Windows 脚本引擎关联的站点对象。|  
|[IActiveScript::SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md)|将脚本引擎放入指定的状态。|  
|[IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md)|检索脚本引擎的当前的状态。|  
|[IActiveScript::Close](../../winscript/reference/iactivescript-close.md)|使脚本引擎放弃所有当前加载的脚本，会丢失其状态，并释放任何对其他对象，因此进入关闭的状态的接口指针。|  
|[IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)|向脚本引擎的命名空间的根级别项名称。|  
|[IActiveScript::AddTypeLib](../../winscript/reference/iactivescript-addtypelib.md)|将类型库添加到脚本的命名空间。|  
|[IActiveScript::GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)|检索`IDispatch`正在运行的脚本的接口。|  
|[IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)|检索当前正在执行的线程的脚本引擎定义标识符。|  
|[IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)|检索与给定的 Microsoft Win32 线程关联的线程的脚本引擎定义标识符。|  
|[IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)|检索脚本线程的当前的状态。|  
|[IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)|中断正在运行的脚本线程执行。|  
|[IActiveScript::Clone](../../winscript/reference/iactivescript-clone.md)|克隆当前脚本引擎 （减去任何当前执行状态），返回当前线程中没有站点加载脚本引擎。|  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)