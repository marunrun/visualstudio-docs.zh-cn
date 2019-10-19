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
ms.openlocfilehash: 401eb759523ed1a33d24c3a298db0b3de2b7d5a7
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575880"
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
  
## <a name="members"></a>Members  
  
|成员|描述|  
|------------|-----------------|  
|DOCUMENTNAMETYPE_APPNODE|获取应用程序树中显示的名称。|  
|DOCUMENTNAMETYPE_TITLE|获取显示在查看器标题栏上的名称。|  
|DOCUMENTNAMETYPE_FILE_TAIL|获取不带路径的文件名。|  
|DOCUMENTNAMETYPE_URL|获取文档的 URL。|  
|DOCUMENTNAMETYPE_UNIQUE_TITLE|获取用枚举追加的标题，用于标识。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)