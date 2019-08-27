---
title: StartTrackingContextWithRoot | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- StartTrackingContextWithRoot
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- StartTrackingContextWithRoot
ms.assetid: f6ef2b76-8035-4a14-8195-aa221c46ef48
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68e80da01a0ab1ad59bbb5bdb06c92c1a11a8ac1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182326"
---
# <a name="starttrackingcontextwithroot"></a>StartTrackingContextWithRoot
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用指定根标记的响应文件启动跟踪上下文。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT WINAPI StartTrackingContextWithRoot(LPCTSTR intermediateDirectory, LPCTSTR taskName, LPCTSTR rootMarkerResponseFile);  
```  
  
#### <a name="parameters"></a>参数  
 [in] `intermediateDirectory`  
 存储跟踪日志的目录。  
  
 [in] `taskName`  
 标识跟踪上下文。 此名称用于创建日志文件名。  
  
 [in] `rootMarkerResponseFile`  
 包含根标记的响应文件的路径名称。 根名称用于将上下文的所有跟踪聚集在一起。  
  
## <a name="return-value"></a>返回值  
 一个 [HRESULT] (<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) 使用的 [SUCCEEDED] （<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) 如果跟踪上下文创建位集。  
  
## <a name="requirements"></a>要求  
 **标头：** FileTracker.h  
  
## <a name="see-also"></a>请参阅  
 [StartTrackingContext](../msbuild/starttrackingcontext.md)
