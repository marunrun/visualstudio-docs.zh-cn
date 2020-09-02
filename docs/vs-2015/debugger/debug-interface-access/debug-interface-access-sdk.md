---
title: 调试接口访问 SDK |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ddaea95bc879364de99c0ec01213cda30fa4e7d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197625"
---
# <a name="debug-interface-access-sdk"></a>调试接口访问 SDK
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Microsoft 调试接口访问软件开发工具包 (DIA SDK) 提供对存储在程序数据库 ( .pdb 中的调试信息的访问) Microsoft 后置编译器工具生成的文件。 由于后置编译器工具生成的 .pdb 文件的格式经历了恒定的修订，因此，公开格式是不切实际的。 使用 DIA API，你可以开发搜索和浏览存储在 .pdb 文件中的调试信息的应用程序。 例如，此类应用程序可以是报表堆栈跟踪信息和分析性能数据。  
  
## <a name="in-this-section"></a>本节内容  
 [入门](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)  
 概述 DIA SDK 功能，并指定 DIA SDK 的安装位置以及所需的标头和库文件。  
  
 [查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)  
 提供有关如何使用 DIA API 查询 .pdb 文件的说明。  
  
 [符号和符号标记](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)  
 讨论如何在 DIA API 中使用符号和符号标记。  
  
 [引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)  
 包含 DIA API 的接口、方法、枚举和结构。  
  
 [Dia2dump 示例](../../debugger/debug-interface-access/dia2dump-sample.md)  
 阐释如何使用 DIA API 搜索和浏览调试信息。  
  
 [Dia2dump.cpp 源文件](../../debugger/debug-interface-access/dia2dump-cpp-source-file.md)  
 [Dia2dump 示例](../../debugger/debug-interface-access/dia2dump-sample.md)用于演示 DIA API 的源代码。
