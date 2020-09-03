---
title: VsgDbg::~VsgDbg（析构函数）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c0ae3dd206953e728175f4479920861295feae00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200291"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg（析构函数）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

销毁 `VsgDbg` 类的实例。 如果正在主动记录图形信息，则完成并关闭图形日志文件，并释放在主动捕获图形信息时使用的资源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
~VsgDbg();  
```  
  
## <a name="see-also"></a>另请参阅  
 [VsgDbg::VsgDbg（构造函数）](../debugger/vsgdbg-vsgdbg-constructor.md)
