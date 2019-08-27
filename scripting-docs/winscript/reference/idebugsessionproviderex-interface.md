---
title: IDebugSessionProviderEx 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 26c5da2d-8c93-4d2b-94d2-97aaa377dcfe
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c9bf341adeaeb17c8986b1b30b12f58113aef562
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978991"
---
# <a name="idebugsessionproviderex-interface"></a>IDebugSessionProviderEx 接口
提供由调试器 IDE 以启用主机和语言启动调试的主要接口。 它将建立一个正在运行的应用程序的调试会话。 此接口由计算机调试管理器实现。  
  
 除了继承的方法之外`IUnknown`，则`IDebugSessionProviderEx`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugSessionProviderEx:CanJITDebug](../../winscript/reference/idebugsessionproviderex-canjitdebug.md)|确定是否能使用指定的应用程序进行实时调试。|  
|[IDebugSessionProviderEx:StartDebugSession](../../winscript/reference/idebugsessionproviderex-startdebugsession.md)|启动具有指定的应用程序的调试会话。|