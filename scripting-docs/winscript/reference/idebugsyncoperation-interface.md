---
title: IDebugSyncOperation 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugSyncOperation interface
ms.assetid: 8d714492-1836-462c-980a-c99e91a2c81b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7184be62a8ad2b65e81d1ad82f01f0ce3f4668c5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004890"
---
# <a name="idebugsyncoperation-interface"></a>IDebugSyncOperation 接口
允许脚本引擎需要时嵌套在特定受阻线程中执行的操作 （如表达式计算）。 接口还提供了一种机制的取消无响应的操作。  
  
 除了继承的方法之外`IUnknown`，则`IDebugSyncOperation`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugSyncOperation::GetTargetThread](../../winscript/reference/idebugsyncoperation-gettargetthread.md)|返回此同步操作的目标应用程序线程。|  
|[IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)|以同步方式执行该操作并返回。|  
|[IDebugSyncOperation::InProgressAbort](../../winscript/reference/idebugsyncoperation-inprogressabort.md)|取消正在进行另一个线程上的操作。|