---
title: APPLICATION_NODE_EVENT_FILTER Enumeration | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- APPLICATION_NODE_EVENT_FILTER Constants
ms.assetid: dccb2cf7-0598-46f8-b3eb-16b752815e96
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3c1727c8d1526199d179fe137c9bf899959bc2ba
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422205"
---
# <a name="applicationnodeeventfilter-enumeration"></a>APPLICATION_NODE_EVENT_FILTER 枚举
指定要排除筛选代码文档时的节点类型。 在中使用[IDebugApplicationNode100::GetExcludedDocuments](../../winscript/reference/idebugapplicationnode100-getexcludeddocuments.md)和[IDebugApplicationNode100::SetFilterForEventSink](../../winscript/reference/idebugapplicationnode100-setfilterforeventsink.md)  
  
> [!IMPORTANT]
> 这些常量由 PDM 10.0 版及更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum tagAPPLICATION_NODE_EVENT_FILTER {    FILTER_EXCLUDE_NOTHING = 0,    FILTER_EXCLUDE_ANONYMOUS_CODE = 0x1,    FILTER_EXCLUDE_EVAL_CODE = 0x2} APPLICATION_NODE_EVENT_FILTER;  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|FILTER_EXCLUDE_NOTHING|0x00000000|发送的所有事件。|  
|FILTER_EXCLUDE_ANONYMOUS_CODE|0x00000001|不包括匿名代码节点。 JScript 运行时使用这些节点`new Function([args,] <code>)'`。|  
|FILTER_EXCLUDE_EVAL_CODE|0x00000002|不包括 eval 代码节点。 这些节点用于 JScript 运行时评估版的支持。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)