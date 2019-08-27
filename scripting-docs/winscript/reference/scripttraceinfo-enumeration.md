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
ms.openlocfilehash: 2ed2c6566db8209280be7f102a55c7de8cf85c44
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840143"
---
# <a name="scripttraceinfo-enumeration"></a>SCRIPTTRACEINFO 枚举
表示正在跟踪的脚本事件。 在中使用[iactivescriptsitetraceinfo:: Sendscripttraceinfo 方法](../../winscript/reference/iactivescriptsitetraceinfo-sendscripttraceinfo-method.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagSCRIPTTRACEINFO {      SCRIPTTRACEINFO_SCRIPTSTART = 0,      SCRIPTTRACEINFO_SCRIPTEND   = 1,      SCRIPTTRACEINFO_COMCALLSTART    = 2,      SCRIPTTRACEINFO_COMCALLEND  = 3,      SCRIPTTRACEINFO_CREATEOBJSTART  = 4,      SCRIPTTRACEINFO_CREATEOBJEND    = 5,      SCRIPTTRACEINFO_GETOBJSTART = 6,      SCRIPTTRACEINFO_GETOBJEND   = 7,  } SCRIPTTRACEINFO ;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|||  
|-|-|  
|SCRIPTTRACEINFO_SCRIPTSTART|脚本的开头。|  
|SCRIPTTRACEINFO_SCRIPTEND|脚本的末尾。|  
|SCRIPTTRACEINFO_COMCALLSTART|启动 COM 调用。|  
|SCRIPTTRACEINFO_COMCALLEND|COM 调用的末尾。|  
|SCRIPTTRACEINFO_CREATEOBJSTART|对象创建开始。|  
|SCRIPTTRACEINFO_CREATEOBJEND|创建对象的末尾。|  
|SCRIPTTRACEINFO_GETOBJSTART|启动 GetObject 调用。|  
|SCRIPTTRACEINFO_GETOBJEND|GetObject 调用末尾。|