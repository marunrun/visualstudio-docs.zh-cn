---
title: Visual Studio 调试 (API 参考) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], API reference
ms.assetid: e4e429da-3667-41f7-9158-a8207d13e91a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a2df6d82099a927664620e19096107f283afada
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738174"
---
# <a name="api-reference-visual-studio-debugging"></a>API 引用（Visual Studio 调试）
参考部分包括 API 的概念概述、说明所有 API 元素的语法和用法的指南，以及各种代码示例。 所有引用都按类别的字母顺序列出。

 下表显示了 `HRESULT` 方法返回的公共值。

|名称|说明|值|
|----------|-----------------|-----------|
|S_OK|成功。|0x00000000|
|E_UNEXPECTED|意外故障。|0x8000FFFF|
|E_NOTIMPL|未实现。|0x80004001|
|E_OUTOFMEMORY|没有足够的内存来完成此操作。|0x8007000E|
|E_INVALIDARG|一个或多个参数无效。|0x80070057|
|E_NOINTERFACE|不支持此类接口。|0x80004002|
|E_POINTER|指针无效。|0x80004003|
|E_HANDLE|句柄无效。|0x80070006|
|E_ABORT|操作已中止。|0x80004004|
|E_FAIL|意外故障。|0x80004005|
|E_ACCESSDENIED|常规拒绝访问错误。|0x80070005|

> [!NOTE]
> 当 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 调试方法返回时 `S_OK` ，假定所有 out 参数指针都是有效的，也就是说，返回时不会对 out 参数指针执行任何验证 `S_OK` 。
>
> [!NOTE]
> 无效或 `NULL` [out] 参数可能导致 IDE 崩溃。

## <a name="see-also"></a>另请参阅
- [接口](../../../extensibility/debugger/reference/interfaces-visual-studio-debugging.md)
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [Visual Studio 调试器可扩展性](../../../extensibility/debugger/visual-studio-debugger-extensibility.md)
