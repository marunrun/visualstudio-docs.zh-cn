---
title: SuspendTracking | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- SuspendTracking
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- SuspendTracking
ms.assetid: f5e06e5a-8083-444c-99c1-07ba834226b5
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3b2d7811a40e87cb5fd19785fc387aad02a7ad07
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201749"
---
# <a name="suspendtracking"></a>SuspendTracking
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在当前上下文中暂停跟踪。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT WINAPI SuspendTracking(void);  
```  
  
## <a name="return-value"></a>返回值  
 一个 [HRESULT] (<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) 使用的 [SUCCEEDED] （<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) 如果跟踪暂停位集。  
  
## <a name="requirements"></a>要求  
 **标头：** FileTracker.h  
  
## <a name="see-also"></a>请参阅  
 [ResumeTracking](../msbuild/resumetracking.md)
