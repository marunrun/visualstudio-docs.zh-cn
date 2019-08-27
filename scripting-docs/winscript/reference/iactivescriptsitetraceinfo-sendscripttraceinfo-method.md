---
title: 'Iactivescriptsitetraceinfo:: Sendscripttraceinfo 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0419e4c5-eb7c-45a3-b6dc-1a5e157d95f9
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c2b444afa22e38694166f7d7522dbe6d0d3774d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992282"
---
# <a name="iactivescriptsitetraceinfosendscripttraceinfo-method"></a>IActiveScriptSiteTraceInfo::SendScriptTraceInfo 方法
将发送跟踪信息，包括事件类型、 上下文和脚本语句。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SendScriptTraceInfo(     [in] SCRIPTTRACEINFO stiEventType,     [in] GUID guidContextID,     [in] DWORD dwScriptContextCookie,     [in] LONG lScriptStatementStart,     [in] LONG lScriptStatementEnd,     [in] DWORD64 dwReserved );   
```  
  
#### <a name="parameters"></a>参数  
 `stiEventType`  
 事件类型。  
  
 `guidContextId`  
 上下文的 GUID。  
  
 `dwScriptContextCookie`  
 上下文的 cookie。  
  
 `lScriptStatementStart`  
 脚本语句的起始位置。  
  
 `lScriptStatementEnd`  
 脚本语句的末尾的位置。  
  
 `dwReserved`  
 保留。