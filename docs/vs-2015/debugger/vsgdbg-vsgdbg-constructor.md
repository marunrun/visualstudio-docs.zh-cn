---
title: 'Vsgdbg:: Vsgdbg （构造函数） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f3bd179aea7d961df6145b7af2f074927fcdc3e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157443"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg（构造函数）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

构造 `VsgDbg` 类的实例（准备或不准备图形诊断的应用内组件）来根据指定的布尔型参数主动捕获并记录图形信息（默认情况下）。  
  
## <a name="syntax"></a>语法  
  
```cpp  
VsgDbg(  
  bDefaultInit  
);  
```  
  
#### <a name="parameters"></a>参数  
 `bDefaultInit`  
 如果指定图形诊断的应用内组件准备主动捕获并记录图形信息，则为 `true`；如果指定应用此时不应准备主动捕获并记录图形信息，则为 `false`。  
  
## <a name="remarks"></a>备注  
 当与调用的构造函数`bDefaultInit`设置为`true`，图形日志文件的文件名由如何`DONT_SAVE_VSGLOG_TO_TEMP`和`VSG_DEFAULT_RUN_FILENAME`预处理器符号定义之前`vsgcapture.h`包含应用程序中。  
  
 如果在 `bDefaultInit` 设置为 `false` 的情况下调用构造函数，则图形诊断的应用内组件可准备以通过调用 `Init` 函数主动捕获图形信息并在稍后记录该信息。  
  
## <a name="see-also"></a>请参阅  
 [VsgDbg::~VsgDbg（析构函数）](../debugger/vsgdbg-tilde-vsgdbg-destructor.md)   
 [Init](../debugger/init.md)   
 [DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)   
 [VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)
