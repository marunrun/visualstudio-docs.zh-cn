---
title: 活动脚本调试器常量、 枚举和结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Active Script Debugger structures
- Active Script Debugger enumerations
- Active Script Debugger constants
ms.assetid: b80b9207-fb19-4ee2-85fb-41f8c26e7706
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b287001371b80612a2b09a9672e59aff51309cc9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997338"
---
# <a name="active-script-debugger-constants-enumerations-and-structures"></a>活动脚本调试器常量、枚举和结构
下面的常量、枚举和结构由 Active Debugging 接口使用。  
  
## <a name="constants-enumerations-and-structures"></a>常量、枚举和结构  
  
|常量|描述|  
|---------------|-----------------|  
|[APPBREAKFLAGS 常量](../../winscript/reference/appbreakflags-enumeration.md)|指示当前的应用程序和线程调试状态。|  
|[DEBUG_TEXT 常量](../../winscript/reference/debug-text-constants.md)|期间使用的选项标志[IDebugExpressionContext::ParseLanguageText](../../winscript/reference/idebugexpressioncontext-parselanguagetext.md)。|  
|[TEXT_DOC_ATTR 常量](../../winscript/reference/text-doc-attr-constants.md)|描述文档的特性。|  
  
|枚举|描述|  
|------------------|-----------------|  
|[APPBREAKFLAGS 常量](../../winscript/reference/appbreakflags-enumeration.md)|指示当前的应用程序和线程调试状态。|  
|[APPLICATION_NODE_EVENT_FILTER 枚举](../../winscript/reference/application-node-event-filter-enumeration.md)|指示要使用筛选器排除的节点。|  
|[BREAKPOINT_STATE 枚举](../../winscript/reference/breakpoint-state-enumeration.md)|指示断点的状态。|  
|[BREAKREASON 枚举](../../winscript/reference/breakreason-enumeration.md)|指示造成中断的原因。|  
|[BREAKRESUMEACTION 枚举](../../winscript/reference/breakresumeaction-enumeration.md)|描述如何从断点继续。|  
|[DOCUMENTNAMETYPE 枚举](../../winscript/reference/documentnametype-enumeration.md)|描述为文档获取哪种类型。|  
|[ERRORRESUMEACTION 枚举](../../winscript/reference/errorresumeaction-enumeration.md)|描述如何从运行时错误继续。|  
|[JS_PROPERTY_ATTRIBUTES 枚举](../../winscript/reference/js-property-attributes-enumeration.md)|指示属性的特性。|  
|[JS_PROPERTY_MEMBERS 枚举](../../winscript/reference/js-property-members-enumeration.md)|在对象成员的请求中用于指定信息类型返回的标志。|  
|[JsDebugReadMemoryFlags 枚举](../../winscript/reference/jsdebugreadmemoryflags-enumeration.md)|读取内存时用于指定行为的标志。|  
|[SCRIPT_DEBUGGER_OPTIONS 枚举](../../winscript/reference/script-debugger-options-enumeration.md)|指示应用于附加调试器的选项或功能集。|  
|[SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND 枚举](../../winscript/reference/script-error-debug-exception-thrown-kind-enumeration.md)|指示已引发异常的类型。|  
|[SOURCE_TEXT_ATTR 常量](../../winscript/reference/source-text-attr-enumeration.md)|描述单个源文本字符的特性。|  
  
|结构|描述|  
|----------------|-----------------|  
|[DebugStackFrameDescriptor 结构](../../winscript/reference/debugstackframedescriptor-structure.md)|枚举堆栈帧并在同一线程上将多个枚举器的输出合并。|  
|[JS_NATIVE_FRAME 结构](../../winscript/reference/js-native-frame-structure.md)|表示堆栈帧。|  
|[JsDebugPropertyInfo 结构](../../winscript/reference/jsdebugpropertyinfo-structure.md)|指示与某一属性有关的信息。|  
|[TEXT_DOCUMENT_ARRAY 结构](../../winscript/reference/text-document-array-structure.md)|提供一组文档。|