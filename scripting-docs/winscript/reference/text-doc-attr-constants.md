---
title: TEXT_DOC_ATTR 常量 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TEXT_DOC_ATTR
apilocation:
- scrobj.dll
helpviewer_keywords:
- TEXT_DOC_ATTR constants
ms.assetid: fd9c53a4-8f73-4c6a-abe5-6b831ecd5b1e
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d22b178d85d304f19e52727ef2c67d77f16da1b3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840078"
---
# <a name="textdocattr-constants"></a>TEXT_DOC_ATTR 常量
描述文档的特性。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef DWORD TEXT_DOC_ATTR;  
```  
  
## <a name="constants"></a>常量  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|TEXT_DOC_ATTR_READONLY|0x00000001|文档是只读的。|  
|TEXT_DOC_ATTR_TYPE_PRIMARY|0x00000002|文档是此文档树的主文件。|  
|TEXT_DOC_ATTR_TYPE_WORKER|0x00000004|文档是在辅助角色。|  
|TEXT_DOC_ATTR_TYPE_SCRIPT|0x00000008|文档是一个脚本文件。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)