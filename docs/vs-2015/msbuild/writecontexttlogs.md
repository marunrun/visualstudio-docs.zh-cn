---
title: WriteContextTLogs | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- WriteContextTLogs
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- WriteContextTLogs
ms.assetid: ffc6c7be-3f22-4624-9ffc-0122fe72b6ec
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7bba9c5b46aa01cddca4de5c8e1347b540999289
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156452"
---
# <a name="writecontexttlogs"></a>WriteContextTLogs
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

写入当前上下文的日志文件。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT WINAPI WriteContextTLogs(LPCTSTR intermediateDirectory, LPCTSTR tlogRootName);  
```  
  
#### <a name="parameters"></a>参数  
 [in] `intermediateDirectory`  
 存储跟踪日志的目录。  
  
 [in] `tlogRootName`  
 日志文件名的根名称。  
  
## <a name="return-value"></a>返回值  
 一个 [HRESULT] (<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) 使用的 [SUCCEEDED] （<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) 如果跟踪上下文创建位集。  
  
## <a name="requirements"></a>要求  
 **标头：** FileTracker.h  
  
## <a name="see-also"></a>请参阅  
 [WriteAllTLogs](../msbuild/writealltlogs.md)
