---
title: SetThreadCount | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- SetThreadCount
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- SetThreadCount
ms.assetid: 335335a5-8ca0-4e18-95f5-62aa6a691386
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 79987c77da7959c4ba37a4ae8e5b689a052cbbbc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193644"
---
# <a name="setthreadcount"></a>SetThreadCount
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

设置全局线程计数，并将该计数分配给当前线程。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT WINAPI SetThreadCount(int threadCount);  
```  
  
#### <a name="parameters"></a>Parameters  
 [in] `threadCount`  
 要使用的线程数。  
  
## <a name="return-value"></a>返回值  
 一个 [HRESULT] (<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) 使用的 [SUCCEEDED] （<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) 位集，如果线程数已更新。  
  
## <a name="requirements"></a>要求  
 **标头：** FileTracker.h
