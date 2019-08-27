---
title: IDebugStackFrameSniffer 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugStackFrameSniffer interface
ms.assetid: 5669598e-a6bd-4694-9cb2-bd908be72bed
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5c9181b5013a9584a2a686ed0e499698be0b62b9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432259"
---
# <a name="idebugstackframesniffer-interface"></a>IDebugStackFrameSniffer 接口
提供了一种方法来枚举逻辑堆栈帧已知的组件。 脚本引擎通常情况下实现此接口。 此接口以查找所有堆栈帧进程调试管理器使用与给定线程相关联。  
  
> [!NOTE]
> 调试程序调用此接口中所需的线程。 脚本引擎必须确定当前线程，并返回相应的枚举器。  
  
## <a name="methods"></a>方法  
 除了继承的方法之外`IUnknown`，则`IDebugStackFrameSniffer`接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugStackFrameSniffer::EnumStackFrames](../../winscript/reference/idebugstackframesniffer-enumstackframes.md)|返回当前线程的堆栈帧的枚举器。|