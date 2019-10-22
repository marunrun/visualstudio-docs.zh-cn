---
title: IJsDebugProcess：： CreateBreakPoint 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugProcess.CreateBreakPoint
apilocation:
- jscript9diag.dll
ms.assetid: a2cb4233-2846-4d11-aa13-21de43abda9f
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2b0a4d595a11dc54829c467a0aace9601042fa08
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575096"
---
# <a name="ijsdebugprocesscreatebreakpoint-method"></a>IJsDebugProcess::CreateBreakPoint 方法
在指定文档位置设置断点。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateBreakPoint(  
   UINT64 documentId,  
   DWORD characterOffset,  
   DWORD characterCount,  
   BOOL isEnabled,  
   IJsDebugBreakPoint **ppDebugBreakPoint  
);  
```  
  
#### <a name="parameters"></a>参数  
 `documentId`  
 中指向 IDebugDocumentText 的指针。  
  
 `characterOffset`  
 中从文件开头开始的字符偏移量。  
  
 `characterCount`  
 中应在其中插入断点的文档文本的长度。  
  
 `isEnabled`  
 中指定是否启用断点。  
  
 `ppDebugBreakPoint`  
 弄表示已创建的断点的对象。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugProcess 接口](../../winscript/reference/ijsdebugprocess-interface.md)