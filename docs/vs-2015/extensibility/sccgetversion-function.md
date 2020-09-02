---
title: SccGetVersion 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a4e548f1f2b82a97206cdf41174a8c1c7d61e885
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200047"
---
# <a name="sccgetversion-function"></a>SccGetVersion 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数获取源代码管理插件支持的源代码管理插件 API 版本号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
LONG SccGetVersion(void);  
```  
  
#### <a name="parameters"></a>参数  
 无。  
  
## <a name="return-value"></a>返回值  
 一个 `LONG` 数据类型，它包含受支持的源代码管理插件 API 的版本号：  
  
|WORD|说明|  
|----------|-----------------|  
|HIWORD|主版本|  
|LOWORD|次要版本|  
  
## <a name="remarks"></a>备注  
 例如，如果源代码管理插件支持源代码管理插件 API 版本1.3，则此函数将返回0x0103。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
