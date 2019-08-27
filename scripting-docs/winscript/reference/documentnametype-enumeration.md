---
title: DOCUMENTNAMETYPE 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DOCUMENTNAMETYPE
apilocation:
- scrobj.dll
helpviewer_keywords:
- DOCUMENTNAMETYPE enumeration
ms.assetid: d36d550e-efb4-493d-8971-4de267005654
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5ee258602c47951f4731dc1378542cc83d57d72b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955207"
---
# <a name="documentnametype-enumeration"></a>DOCUMENTNAMETYPE 枚举
描述为文档获取哪种类型。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagDOCUMENTNAMETYPE {  
   DOCUMENTNAMETYPE_APPNODE,  
   DOCUMENTNAMETYPE_TITLE,  
   DOCUMENTNAMETYPE_FILE_TAIL,  
   DOCUMENTNAMETYPE_URL,  
DOCUMENTNAMETYPE_UNIQUE_TITLE,} DOCUMENTNAMETYPE;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|DOCUMENTNAMETYPE_APPNODE|显示在应用程序树中获取的名称。|  
|DOCUMENTNAMETYPE_TITLE|在查看器标题栏上显示获取的名称。|  
|DOCUMENTNAMETYPE_FILE_TAIL|获取不含路径的文件名称。|  
|DOCUMENTNAMETYPE_URL|获取文档的 URL。|  
|DOCUMENTNAMETYPE_UNIQUE_TITLE|获取附加的标识的枚举的标题。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)