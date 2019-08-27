---
title: 接口 （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- interfaces [DIA SDK]
- DIA SDK, interfaces
ms.assetid: 62aee7c3-d314-4272-a32b-b2818f32fab8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7f60f4b9018f5b2fff9a5426c28dba40177d9ae9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840686"
---
# <a name="interfaces-debug-interface-access-sdk"></a>接口（调试接口访问 SDK）
下的内容和 Vtable 顺序中的接口上的表中每个接口，方法是按字母顺序列出。

## <a name="in-this-section"></a>本节内容

[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)

提供了控制 DIA SDK 如何计算的调试对象的虚拟和相对虚拟地址。

[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)

启动的调试符号的源的访问。

[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)

提供了对调试数据流中记录的访问。

[IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)

枚举数据源中包含的各种调试流。

[IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

枚举数据源中包含的各种框架的数据元素。

[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

枚举数据源中包含的各种插入的源。

[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

枚举数据源中包含的各种行号。

[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

枚举数据源中包含的各个部分贡献。

[IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

枚举数据源中包含的各个部分。

[IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

枚举数据源中包含的各种源文件。

[IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)

枚举可用的各种堆栈帧。

[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

枚举数据源中包含的各种符号。

[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)

通过地址来枚举数据源中包含的各种符号。

[IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)

枚举数据源中包含的各个表。

[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)

公开一个堆栈帧的详细信息。

[IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)

公开的模块或映像的基的位置和内存偏移量的详细信息。

[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

访问程序源代码存储在 DIA 数据源。

[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)

介绍从图像的文字字节块映射到源文件行号的过程的访问信息。

[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)

从 DIA 符号查找过程，从而使一个用户界面来报告进度的位置尝试接收回调。

[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)

接收来自 DIA 符号查找过程，从而限制强加于查找过程的回调。

[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

允许你读取 DIA 属性集的持久性属性。

[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)

允许客户端应用程序提供的按文件位置指定的可执行文件的字节数。

[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)

允许客户端应用程序提供的可执行文件的相对虚拟地址由指定的字节数。

[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)

描述了部分内容中检索数据，也就是说，连续内存块归功于图像编译单位。

[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)

将数据从节号线段的地址空间的映射。

[IDiaSession](../../debugger/debug-interface-access/idiasession.md)

提供调试符号的查询上下文。

[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)

表示一个源代码文件。

[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)

显示堆栈帧的属性。

[IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)

提供方法来执行堆栈遍历使用 PDB 文件。

[IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)

维护之间的调用堆栈上下文[idiaframedata:: Execute](../../debugger/debug-interface-access/idiaframedata-execute.md)方法。

[IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)

便于遍历堆栈使用程序调试数据库 (PDB) 文件。

[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

描述符号实例的属性。

[IDiaTable](../../debugger/debug-interface-access/idiatable.md)

枚举 DIA 数据源表。

## <a name="related-sections"></a>相关章节
[枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)

介绍枚举和结构由 DIA SDK 的各种接口。

[常量（调试接口访问 SDK）](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)

介绍在 DIA SDK 中提供的常量。

## <a name="see-also"></a>请参阅

- [引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)