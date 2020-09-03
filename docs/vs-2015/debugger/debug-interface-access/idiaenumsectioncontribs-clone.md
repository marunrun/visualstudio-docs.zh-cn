---
title: IDiaEnumSectionContribs：： Clone |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Clone method
ms.assetid: 81d3f3a7-3684-4e5c-b028-29b268684a2c
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 56267cbbffd6b5ff123dcf08ee71200a9b343fac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190025"
---
# <a name="idiaenumsectioncontribsclone"></a>IDiaEnumSectionContribs::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建与当前枚举数包含相同枚举状态的枚举数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Clone(   
   IDiaEnumSectionContrib** ppenum  
);  
```  
  
#### <a name="parameters"></a>参数  
 ppenum  
 弄返回一个 [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) 对象，该对象包含枚举器的副本。 部分发布不是重复的，只是枚举器。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
