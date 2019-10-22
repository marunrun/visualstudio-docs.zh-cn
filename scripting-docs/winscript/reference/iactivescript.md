---
title: IActiveScript |Microsoft Docs
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
ms.openlocfilehash: 7a33db2bcbcb356a508fec2e6bc5449a899a1299
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577239"
---
# <a name="iactivescript"></a>IActiveScript
提供初始化脚本引擎所需的方法。 脚本引擎必须实现 `IActiveScript` 接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScript::SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md)|通知主机提供的[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)网站的脚本引擎。|  
|[IActiveScript::GetScriptSite](../../winscript/reference/iactivescript-getscriptsite.md)|检索与 Windows 脚本引擎关联的网站对象。|  
|[IActiveScript::SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md)|将脚本引擎置于指定状态。|  
|[IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md)|检索脚本引擎的当前状态。|  
|[IActiveScript::Close](../../winscript/reference/iactivescript-close.md)|使脚本引擎放弃当前加载的任何脚本，失去其状态，然后释放它所拥有的任何指向其他对象的接口指针，从而进入已关闭状态。|  
|[IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)|将根级别项的名称添加到脚本引擎的命名空间中。|  
|[IActiveScript::AddTypeLib](../../winscript/reference/iactivescript-addtypelib.md)|将类型库添加到脚本的命名空间中。|  
|[IActiveScript::GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)|检索正在运行的脚本的 `IDispatch` 接口。|  
|[IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)|检索当前正在执行的线程的脚本引擎定义的标识符。|  
|[IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)|检索与给定的 Microsoft Win32 线程关联的线程的脚本引擎定义的标识符。|  
|[IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)|检索脚本线程的当前状态。|  
|[IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)|中断正在运行的脚本线程的执行。|  
|[IActiveScript::Clone](../../winscript/reference/iactivescript-clone.md)|克隆当前脚本引擎（减去任何当前执行状态），并返回在当前线程中没有站点的加载的脚本引擎。|  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)