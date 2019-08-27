---
title: 'Ijsdebugprocess:: Createbreakpoint 方法 |Microsoft Docs'
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
ms.openlocfilehash: b398b93c2e7b5ad43abd35d385407b39c0c980f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557967"
---
# <a name="ijsdebugprocesscreatebreakpoint-method"></a>IJsDebugProcess::CreateBreakPoint 方法
将指定的文档位置处设置断点。  
  
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
 [in]指针指向 IDebugDocumentText。  
  
 `characterOffset`  
 [in]从文件开头的字符偏移量。  
  
 `characterCount`  
 [in]应在其中插入断点文档文本的长度。  
  
 `isEnabled`  
 [in]指定是否启用断点。  
  
 `ppDebugBreakPoint`  
 [out]表示已创建的断点的对象。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugProcess 接口](../../winscript/reference/ijsdebugprocess-interface.md)