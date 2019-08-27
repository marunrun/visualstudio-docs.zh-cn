---
title: IActiveScriptSite | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptSite interface
ms.assetid: 4d604a11-5365-46cf-ab71-39b3dbbe9f22
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 67e16e2825f03c9ae452e639d6a086bee584ac95
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992556"
---
# <a name="iactivescriptsite"></a>IActiveScriptSite
实现的主机来创建 Windows 脚本引擎的站点。 通常情况下，此站点将会向脚本 （例如，ActiveX 控件） 的所有对象的容器与相关联。 通常情况下，此容器将对应于正在查看的页的文档。 例如，Microsoft Internet Explorer 中，将创建此类容器显示每个 HTML 页。 每个 ActiveX 控件 （或其他自动化对象） 上的网页和脚本引擎本身，将可枚举此容器中。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|||  
|-|-|  
|方法|描述|  
|[IActiveScriptSite::GetLCID](../../winscript/reference/iactivescriptsite-getlcid.md)|检索主机使用用于显示用户界面元素的区域设置标识符。|  
|[IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)|获取有关已添加到引擎通过调用某个项的信息[iactivescript:: Addnameditem](../../winscript/reference/iactivescript-addnameditem.md)方法。|  
|[IActiveScriptSite::GetDocVersionString](../../winscript/reference/iactivescriptsite-getdocversionstring.md)|检索唯一标识当前的文档版本从主机的角度来看是主机定义的字符串。|  
|[IActiveScriptSite::OnScriptTerminate](../../winscript/reference/iactivescriptsite-onscriptterminate.md)|当脚本已完成执行时调用。|  
|[IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)|通知主机脚本引擎已更改状态。|  
|[IActiveScriptSite::OnScriptError](../../winscript/reference/iactivescriptsite-onscripterror.md)|通知主机引擎运行脚本时发生了执行错误。|  
|[IActiveScriptSite::OnEnterScript](../../winscript/reference/iactivescriptsite-onenterscript.md)|通知主机脚本引擎已开始执行的脚本代码。|  
|[IActiveScriptSite::OnLeaveScript](../../winscript/reference/iactivescriptsite-onleavescript.md)|通知主机脚本引擎已返回执行脚本代码。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)