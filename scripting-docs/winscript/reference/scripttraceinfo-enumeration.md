---
title: SCRIPTTRACEINFO 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: cb8a4767-8c8e-4fa0-a735-038767a8c500
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cf4933cc5778dd4af21e1b12d64fc59d371ad097
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238213"
---
# <a name="scripttraceinfo-enumeration"></a>SCRIPTTRACEINFO 枚举
表示正在跟踪的脚本事件。 在 [IActiveScriptSiteTraceInfo：： SendScriptTraceInfo 方法](../../winscript/reference/iactivescriptsitetraceinfo-sendscripttraceinfo-method.md)中使用。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagSCRIPTTRACEINFO {      SCRIPTTRACEINFO_SCRIPTSTART = 0,      SCRIPTTRACEINFO_SCRIPTEND   = 1,      SCRIPTTRACEINFO_COMCALLSTART    = 2,      SCRIPTTRACEINFO_COMCALLEND  = 3,      SCRIPTTRACEINFO_CREATEOBJSTART  = 4,      SCRIPTTRACEINFO_CREATEOBJEND    = 5,      SCRIPTTRACEINFO_GETOBJSTART = 6,      SCRIPTTRACEINFO_GETOBJEND   = 7,  } SCRIPTTRACEINFO ;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|“值”|脚本事件|  
|-|-|  
|SCRIPTTRACEINFO_SCRIPTSTART|脚本的开头。|  
|SCRIPTTRACEINFO_SCRIPTEND|脚本的末尾。|  
|SCRIPTTRACEINFO_COMCALLSTART|COM 调用的开头。|  
|SCRIPTTRACEINFO_COMCALLEND|COM 调用的结束。|  
|SCRIPTTRACEINFO_CREATEOBJSTART|对象创建的开始。|  
|SCRIPTTRACEINFO_CREATEOBJEND|对象创建的结束。|  
|SCRIPTTRACEINFO_GETOBJSTART|GetObject 调用的开头。|  
|SCRIPTTRACEINFO_GETOBJEND|GetObject 调用的结束。|