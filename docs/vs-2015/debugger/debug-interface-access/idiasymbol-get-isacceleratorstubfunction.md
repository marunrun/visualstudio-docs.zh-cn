---
title: IDiaSymbol：： get_isAcceleratorStubFunction |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: cc4ea375-76f6-4ba8-baed-c5fa82108137
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 69f82f836be6ab91fe73af5a0febf7a39723b191
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199899"
---
# <a name="idiasymbolget_isacceleratorstubfunction"></a>IDiaSymbol::get_isAcceleratorStubFunction
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指示符号是否对应于为对应于调用的快捷键编译的着色器的顶级函数符号 `parallel_for_each` 。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_isAcceleratorStubFunction(   
   BOOL* pFlag);  
```  
  
#### <a name="parameters"></a>参数  
 `pFlag`  
 弄指向 `BOOL` 的指针，该指针指示符号是否对应于为对应于调用的快捷键编译的着色器的顶级函数符号 `parallel_for_each` 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
