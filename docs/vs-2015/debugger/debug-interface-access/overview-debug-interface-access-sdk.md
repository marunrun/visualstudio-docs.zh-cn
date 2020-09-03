---
title: 概述 (调试接口访问 SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- user-defined types
- .dbg files
- modules
- interfaces [DIA SDK]
- DBG files
- procedures [DIA SDK]
- executable files
- COM objects, in DIA SDK
- compilands
- executable images
ms.assetid: 720b4479-a8bc-4fec-860e-80c1a0780405
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7374b03da42e34e8ac3be8c7cc570769d9cfd1ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179199"
---
# <a name="overview-debug-interface-access-sdk"></a>概述（调试接口访问 SDK）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用 DIA SDK 访问 Microsoft 调试信息。 DIA SDK 提供了基于 COM 的 API 集，无需在 Microsoft 更改调试信息格式时重写代码。 使用 DIA SDK 还可以读取一组以前版本的调试信息，这些信息位于 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 版本5.0 及更高版本生成的 .pdb 和 dbg 文件中。  
  
 DIA SDK 中的每个接口都表示不同的 COM 对象，但在其他情况下除外。 附加接口，因此其他对象是通过显式查询（如 [IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) 或 [IDiaSession：： findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)）创建的，而不是通过调用现有的 `QueryInterface` 接口指针来创建的。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)   
 [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
