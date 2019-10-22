---
title: 活动脚本常量、枚举和错误代码 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: aab24471-5817-45c0-be07-ffe4648923ed
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e03bef99c2297d517aa5234db49820a2b9600ce7
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572720"
---
# <a name="active-script-constants-enumerations-and-error-codes"></a>活动脚本常量、枚举和错误代码
本部分介绍 Windows 脚本引擎中使用的枚举和错误代码。  
  
## <a name="constants"></a>常量  
  
|返回的常量|描述|  
|--------------|-----------------|  
|[SCRIPTTHREADID 常量](../../winscript/reference/scriptthreadid-constants.md)|指定线程的类型。|  
  
## <a name="properties"></a>属性  
  
|Property|描述|  
|--------------|-----------------|  
|[SCRIPTPROP_HOSTKEEPALIVE 属性](../../winscript/reference/scriptprop-hostkeepalive-property.md)|用于指定是否应在有未完成的引用时使脚本引擎保持完全正常运行。|  
  
## <a name="enumerations"></a>枚举  
  
|枚举|描述|  
|-----------------|-----------------|  
|[SCRIPTGCTYPE 枚举](../../winscript/reference/scriptgctype-enumeration.md)|要执行的垃圾回收的类型。|  
|[SCRIPTLANGUAGEVERSION 枚举](../../winscript/reference/scriptlanguageversion-enumeration.md)|指定可能的脚本版本。|  
|[SCRIPTSTATE 枚举](../../winscript/reference/scriptstate-enumeration.md)|指定脚本引擎的状态。|  
|||  
|[SCRIPTTHREADSTATE 枚举](../../winscript/reference/scriptthreadstate-enumeration.md)|指定脚本引擎中的线程的状态。|  
|[SCRIPTTRACEINFO 枚举](../../winscript/reference/scripttraceinfo-enumeration.md)|表示正在跟踪的脚本事件。 在[IActiveScriptSiteTraceInfo：： SendScriptTraceInfo 方法](../../winscript/reference/iactivescriptsitetraceinfo-sendscripttraceinfo-method.md)中使用。|  
|[SCRIPTUICHANDLING 枚举](../../winscript/reference/scriptuichandling-enumeration.md)|表示应对 UI 控件进行处理的方式。|  
|[SCRIPTUICITEM 枚举](../../winscript/reference/scriptuicitem-enumeration.md)|表示 UI 项的类型。 在[IActiveScriptSiteUIControl：： GetUIBehavior 方法](../../winscript/reference/iactivescriptsiteuicontrol-getuibehavior-method.md)中使用。|  
  
## <a name="error-codes"></a>错误代码  
  
|错误代码|描述|  
|----------------|-----------------|  
|[SCRIPT_E_PROPAGATE 错误代码](../../winscript/reference/script-e-propagate-error-code.md)|脚本错误将传播到调用方，该调用方可能在不同的线程中。|  
|[SCRIPT_E_RECORDED 错误代码](../../winscript/reference/script-e-recorded-error-code.md)|脚本引擎和主机之间已传递错误。|  
|[SCRIPT_E_REPORTED 错误代码](../../winscript/reference/script-e-reported-error-code.md)|脚本引擎已向主机报告了未经处理的异常。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)