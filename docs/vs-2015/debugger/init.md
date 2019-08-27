---
title: Init | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: c55ddec8-9101-4673-979b-4109caca9146
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ea9f8a24d342668b3574c3798a32c58c124aca7b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185847"
---
# <a name="init"></a>Init
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

准备图形诊断的应用内组件来主动捕获图形信息并将其记录到图形日志文件。  
  
## <a name="syntax"></a>语法  
  
```cpp  
void Init(  
  std::function<void (int len, wchar_t * pszBuffer)> vsgLogGetter  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `vsgLogGetter`  
 一个可调用的实体（如函数、函数指针、lambda 或函数对象），它可将由 `wchar_t` 组成的缓冲区长度和指向该缓冲区的指针用作参数，并返回 `void`。 通过调用此可调用的实体，可确定将用于记录图像信息的文件名，并在返回前将其写入指定的缓冲区中。  
  
## <a name="remarks"></a>备注  
 在通过将其构造函数的 `Init` 参数指定为 `VsgDbg` 来构造 `bDefaultInit` 类的实例时将自动调用 `true` 函数；否则，必须在主动捕获并记录图形信息之前显式调用 `Init`。  
  
 可通过调用 `UnInit` 来完成并关闭活动图形日志文件，然后通过再次调用 `Init` 捕获更多的图形信息并将这些信息记录到新图形日志文件。 您可使用相同的 `VsgDbg` 实例将此操作重复所需次数以创建多个单独的图形日志文件。  
  
## <a name="see-also"></a>请参阅  
 [UnInit](../debugger/init.md)
