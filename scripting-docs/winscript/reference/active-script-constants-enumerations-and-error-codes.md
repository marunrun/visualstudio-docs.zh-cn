---
title: 活动脚本常量、 枚举和错误代码 |Microsoft Docs
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
ms.openlocfilehash: 090b494e904fbef1c0d3d8b380f7a184a6042788
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953993"
---
# <a name="active-script-constants-enumerations-and-error-codes"></a>活动脚本常量、枚举和错误代码
本部分介绍枚举和错误代码在 Windows 脚本引擎中使用。  
  
## <a name="constants"></a>常量  
  
|返回的常量|描述|  
|--------------|-----------------|  
|[SCRIPTTHREADID 常量](../../winscript/reference/scriptthreadid-constants.md)|指定线程的类型。|  
  
## <a name="properties"></a>属性  
  
|属性|描述|  
|--------------|-----------------|  
|[SCRIPTPROP_HOSTKEEPALIVE 属性](../../winscript/reference/scriptprop-hostkeepalive-property.md)|用于指定应保留脚本引擎完全正常运行，如果有未完成的引用。|  
  
## <a name="enumerations"></a>枚举  
  
|枚举|描述|  
|-----------------|-----------------|  
|[SCRIPTGCTYPE 枚举](../../winscript/reference/scriptgctype-enumeration.md)|若要执行的垃圾回收的类型。|  
|[SCRIPTLANGUAGEVERSION 枚举](../../winscript/reference/scriptlanguageversion-enumeration.md)|指定可能的脚本版本。|  
|[SCRIPTSTATE 枚举](../../winscript/reference/scriptstate-enumeration.md)|指定脚本引擎的状态。|  
|||  
|[SCRIPTTHREADSTATE 枚举](../../winscript/reference/scriptthreadstate-enumeration.md)|脚本引擎中指定的线程的状态。|  
|[SCRIPTTRACEINFO 枚举](../../winscript/reference/scripttraceinfo-enumeration.md)|表示正在跟踪的脚本事件。 在中使用[iactivescriptsitetraceinfo:: Sendscripttraceinfo 方法](../../winscript/reference/iactivescriptsitetraceinfo-sendscripttraceinfo-method.md)。|  
|[SCRIPTUICHANDLING 枚举](../../winscript/reference/scriptuichandling-enumeration.md)|表示应处理 UI 控件的方式。|  
|[SCRIPTUICITEM 枚举](../../winscript/reference/scriptuicitem-enumeration.md)|表示 UI 项的类型。 在中使用[iactivescriptsiteuicontrol:: Getuibehavior 方法](../../winscript/reference/iactivescriptsiteuicontrol-getuibehavior-method.md)。|  
  
## <a name="error-codes"></a>错误代码  
  
|错误代码|描述|  
|----------------|-----------------|  
|[SCRIPT_E_PROPAGATE 错误代码](../../winscript/reference/script-e-propagate-error-code.md)|脚本错误被传播到调用方，这可能是在不同线程中。|  
|[SCRIPT_E_RECORDED 错误代码](../../winscript/reference/script-e-recorded-error-code.md)|脚本引擎和主机之间传递了错误。|  
|[SCRIPT_E_REPORTED 错误代码](../../winscript/reference/script-e-reported-error-code.md)|脚本引擎已报告到的主机未处理的异常。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)