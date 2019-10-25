---
title: 概述（调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e4269c620247f256d2cfae2e84b76ff60fcf9ba
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738609"
---
# <a name="overview-debug-interface-access-sdk"></a>概述（调试接口访问 SDK）
使用 DIA SDK 访问 Microsoft 调试信息。 DIA SDK 提供了基于 COM 的 API 集，无需在 Microsoft 更改调试信息格式时重写代码。 DIA SDK 还允许您从 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 版本5.0 及更高版本生成的一组以前版本的调试信息中进行读取。

 DIA SDK 中的每个接口都表示不同的 COM 对象，但在其他情况下除外。 附加接口以及其他对象通过显式查询（如[IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)或[IDiaSession：： findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)）创建，而不是通过对现有接口指针调用 `QueryInterface` 来创建。

## <a name="see-also"></a>请参阅
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)