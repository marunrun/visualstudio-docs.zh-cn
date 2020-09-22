---
title: IDiaSession::put_loadAddress | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f697384874726904960fc5ba04733c3acfe1cd06
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840328"
---
# <a name="idiasessionput_loadaddress"></a>IDiaSession::put_loadAddress
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置与此符号存储区中的符号对应的可执行文件的加载地址。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT put_loadAddress (   
   ULONGLONG NewVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `NewVal`  
 中可执行文件的加载地址。  
  
## <a name="remarks"></a>备注  
 符号虚拟地址 (VA) 属性使用此方法的值进行计算。 除非将该属性设置为非零，否则不会计算虚拟地址。  
  
> [!NOTE]
> 如果需要使用符号上的任何虚拟属性，则在获取 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) 对象时和开始使用对象之前，必须调用此方法。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
