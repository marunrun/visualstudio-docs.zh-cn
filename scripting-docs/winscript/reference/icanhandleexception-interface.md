---
title: ICanHandleException Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICanHandleException interface
ms.assetid: 32df7f81-557d-40cf-a844-06a6eaa292f3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 363a52cfeb409d293ba3589b9d869bbc4fdf5918
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991357"
---
# <a name="icanhandleexception-interface"></a>ICanHandleException 接口
允许调用方的脚本引擎的调用方以指定哪些异常句柄。  
  
## <a name="methods"></a>方法  
 除了继承的方法之外`IUnknown`，则`ICanHandleException`接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[ICanHandleException::CanHandleException](../../winscript/reference/icanhandleexception-canhandleexception.md)|确定是否脚本引擎的调用方可以处理指定的异常。|