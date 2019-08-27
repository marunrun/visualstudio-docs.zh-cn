---
title: IDebugSessionProvider 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugSessionProvider interface
ms.assetid: 1b898423-7af9-44f5-8dda-987005309c99
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fe73901d92cb42675ff9ec981bd9b90dcca5d546
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979043"
---
# <a name="idebugsessionprovider-interface"></a>IDebugSessionProvider 接口
由调试器 IDE 来启用主机和语言提供的主界面启动调试。 它将建立一个正在运行的应用程序的调试会话。 此接口由计算机调试管理器实现。  
  
 除了继承的方法之外`IUnknown`，则`IDebugSessionProvider`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugSessionProvider::StartDebugSession](../../winscript/reference/idebugsessionprovider-startdebugsession.md)|启动具有指定的应用程序的调试会话。|