---
title: " (调试接口访问 SDK) 的接口 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- interfaces [DIA SDK]
- DIA SDK, interfaces
ms.assetid: 62aee7c3-d314-4272-a32b-b2818f32fab8
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5eaf63ac57610e9ebde6703f0b5c15bf9607fdde
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150862"
---
# <a name="interfaces-debug-interface-access-sdk"></a>接口（调试接口访问 SDK）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

方法在目录中的每个接口下按字母顺序列出，在 "接口" 页上按 Vtable 顺序列出。  
  
## <a name="in-this-section"></a>本节内容  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)  
 提供对 DIA SDK 如何计算调试对象的虚拟和相对虚拟地址的控制。  
  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)  
 启动对调试符号源的访问。  
  
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)  
 提供对调试数据流中的记录的访问。  
  
 [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)  
 枚举数据源中包含的各种调试流。  
  
 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)  
 枚举数据源中包含的各种帧数据元素。  
  
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)  
 枚举数据源中包含的各种注入的源。  
  
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)  
 枚举数据源中包含的各个行号。  
  
 [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)  
 枚举数据源中包含的各种节发布。  
  
 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)  
 枚举数据源中包含的各个段。  
  
 [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)  
 枚举数据源中包含的各种源文件。  
  
 [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)  
 枚举可用的各种堆栈帧。  
  
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)  
 枚举数据源中包含的各种符号。  
  
 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)  
 枚举数据源中包含的各种符号，按地址进行枚举。  
  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)  
 枚举数据源中包含的各个表。  
  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)  
 公开堆栈帧的详细信息。  
  
 [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)  
 公开模块或图像的基位置和内存偏移量的详细信息。  
  
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)  
 访问存储在 DIA 数据源中的程序源代码。  
  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)  
 访问描述从图像的字节块到源文件行号的映射过程的信息。  
  
 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)  
 接收来自 DIA 符号定位过程的回调，从而使用户界面能够报告位置尝试的进度。  
  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)  
 接收来自 DIA 符号定位过程的回调，以允许对查找过程施加限制。  
  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)  
 允许读取 DIA 属性集的持久性属性。  
  
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)  
 使客户端应用程序能够提供文件位置指定的可执行文件的字节数。  
  
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)  
 使客户端应用程序能够提供相对虚拟地址指定的可执行文件的字节数。  
  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)  
 检索描述节内容的数据，即由编译单位提供给图像的连续内存块。  
  
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)  
 将数据从节号映射到地址空间的段。  
  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)  
 提供调试符号的查询上下文。  
  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)  
 表示一个源文件。  
  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)  
 公开堆栈帧的属性。  
  
 [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)  
 提供用 PDB 文件执行堆栈审核的方法。  
  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)  
 在调用 [IDiaFrameData：： execute](../../debugger/debug-interface-access/idiaframedata-execute.md) 方法之间维护堆栈上下文。  
  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)  
 使用程序调试数据库 (PDB) 文件，有助于遍历堆栈。  
  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)  
 介绍符号实例的属性。  
  
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)  
 枚举 DIA 数据源表。  
  
## <a name="related-sections"></a>相关章节  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)  
 描述 DIA SDK 的各种接口使用的枚举和结构。  
  
 [常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)  
 介绍 DIA SDK 中可用的常量。  
  
## <a name="see-also"></a>另请参阅  
 [引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
