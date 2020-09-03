---
title: IDiaEnumSegments::Clone | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Clone method
ms.assetid: 93deaac6-72ab-4408-ba14-66174a618757
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1def1f595b1b6afcedc36612f4e1c9cf33882b02
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189932"
---
# <a name="idiaenumsegmentsclone"></a>IDiaEnumSegments::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建与当前枚举数包含相同枚举状态的枚举数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Clone (   
   IDiaEnumSegments** ppenum  
);  
```  
  
#### <a name="parameters"></a>参数  
 ppenum  
 弄返回一个 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md) 对象，该对象包含枚举器的副本。 分段不是重复的，只是枚举器。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
