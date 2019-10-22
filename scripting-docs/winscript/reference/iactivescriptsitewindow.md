---
title: IActiveScriptSiteWindow |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptSiteWindow interface
ms.assetid: 96d5c493-2c0b-47e2-848b-4a8dacdcd65c
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1ee680a3d00c6736549b03ce8fee5593a7a8c5af
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575895"
---
# <a name="iactivescriptsitewindow"></a>IActiveScriptSiteWindow
此接口由支持与[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)相同的对象上的用户界面的主机实现。 不支持用户界面的主机（如服务器）不会实现 `IActiveScriptSiteWindow` 接口。 脚本引擎通过从 `IActiveScriptSite` 调用 `QueryInterface` 来访问此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptSiteWindow::GetWindow](../../winscript/reference/iactivescriptsitewindow-getwindow.md)|检索可充当脚本引擎必须显示的弹出窗口的所有者的窗口句柄。|  
|[IActiveScriptSiteWindow::EnableModeless](../../winscript/reference/iactivescriptsitewindow-enablemodeless.md)|使宿主启用或禁用其主窗口以及任何无模式对话框。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)