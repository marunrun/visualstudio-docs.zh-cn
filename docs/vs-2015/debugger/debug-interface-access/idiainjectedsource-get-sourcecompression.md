---
title: IDiaInjectedSource：： get_sourceCompression |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_sourceCompression method
ms.assetid: 854b142f-23a9-466c-bf7f-98e581d5abcd
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8e8cafcaf3d245ac2310b93c16812327c381854d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192429"
---
# <a name="idiainjectedsourceget_sourcecompression"></a>IDiaInjectedSource::get_sourceCompression
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索使用的源压缩的指示器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_sourceCompression (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回使用的源压缩的指示器。 如果值为零，则表示未使用源压缩。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法返回的值特定于所使用的编译器。 例如，编译器可能使用运行长度编码或 Huffman 样式压缩。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
