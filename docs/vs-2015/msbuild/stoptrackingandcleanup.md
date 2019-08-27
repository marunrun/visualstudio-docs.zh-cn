---
title: StopTrackingAndCleanup | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- StopTrackingAndCleanup
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- StopTrackingAndCleanup
ms.assetid: 9f8c5994-2dfc-43c3-a5fb-89b2f8990429
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7b4a6cca4010284c9a75767710710d28c093c271
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203111"
---
# <a name="stoptrackingandcleanup"></a>StopTrackingAndCleanup
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

停止所有跟踪，并释放跟踪会话使用的任何内存。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT WINAPI StopTrackingAndCleanup(void);  
```  
  
## <a name="return-value"></a>返回值  
 返回一个 [HRESULT] （<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) 使用的 [SUCCEEDED] （<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) 如果跟踪已停止位集。  
  
## <a name="requirements"></a>要求  
 **标头：** FileTracker.h  
  
## <a name="see-also"></a>请参阅  
 [StartTrackingContext](../msbuild/starttrackingcontext.md)
