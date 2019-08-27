---
title: ISetNextStatement::CanSetNextStatement |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISetNextStatement.CanSetNextStatement
apilocation:
- scrobj.dll
ms.assetid: e2a54634-31ec-4d16-84e8-2b123845d876
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eb65faaf107c42b44201ea18c1150f8093b1654c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786610"
---
# <a name="isetnextstatementcansetnextstatement"></a>ISetNextStatement::CanSetNextStatement
此方法确定是否执行点，用于确定要执行的代码的下一个语句，可以将设置为指定的位置。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CanSetNextStatement(  
   IDebugStackFrame*  pStackFrame,  
   IDebugCodeContext*  pCodeContext  
)  
```  
  
#### <a name="parameters"></a>参数  
 `pStackFrame`  
 [in]指向堆栈帧对象的指针。  
  
 `pCodeContext`  
 [in]对代码上下文对象的指针。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|下一条语句可以将更新为指定的代码上下文。|  
|`S_FALSE`|下一条语句不能更新为指定的代码上下文。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [ISetNextStatement 接口](../../winscript/reference/isetnextstatement-interface.md)