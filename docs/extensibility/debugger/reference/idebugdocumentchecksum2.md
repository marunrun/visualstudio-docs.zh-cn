---
title: IDebugDocumentChecksum2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b4bfc51595e6414a3760d4e57ab6f9791259f83
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341289"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
表示调试文档的校验和并可将组件之间传递校验和。

## <a name="syntax"></a>语法

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口可以由任何公开的组件实现[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)接口。 但是，它主要由实现的调试引擎，以便可以传递回 IDE 并查找源时，使用符号文件 (*.pdb) 中嵌入的校验和。

## <a name="methods"></a>方法
 下表显示的方法`IDebugDocumentChecksum2`。

|方法|描述|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|检索要使用的字节的最大数目的文档校验和算法标识符。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll