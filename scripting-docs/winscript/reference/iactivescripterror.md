---
title: IActiveScriptError | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptError interface
ms.assetid: c8e0288d-38ff-4145-a7e3-f8cdfb72eefe
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1ca783e2100fe74ed05499f9611a9b8f3399817f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62954988"
---
# <a name="iactivescripterror"></a>IActiveScriptError
实现此接口的对象传递给[IActiveScriptSite::OnScriptError](../../winscript/reference/iactivescriptsite-onscripterror.md)脚本引擎遇到未经处理的错误时的方法。 主机然后方法对此对象调用以获取有关发生的错误的信息。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptError::GetExceptionInfo](../../winscript/reference/iactivescripterror-getexceptioninfo.md)|检索有关错误的信息。|  
|[IActiveScriptError::GetSourcePosition](../../winscript/reference/iactivescripterror-getsourceposition.md)|检索在源代码中发生错误的位置。|  
|[IActiveScriptError::GetSourceLineText](../../winscript/reference/iactivescripterror-getsourcelinetext.md)|检索错误的发生位置的源文件中的行。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)