---
title: IDebugDisassemblyStream2：： Seek |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Seek
helpviewer_keywords:
- IDebugDisassemblyStream2::Seek
ms.assetid: afec3008-b1e0-4803-ad24-195dbfb6497e
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d774cc0bf6bca1278423249960bbc5233aa6ad37
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203022"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

相对于指定位置，将给定数量的指令移动到反汇编流中的读取指针。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Seek(   
   SEEK_START          dwSeekStart,  
   IDebugCodeContext2* pCodeContext,  
   UINT64              uCodeLocationId,  
   INT64               iInstructions  
);  
```  
  
```csharp  
int Seek(   
   enum_SEEK_START    dwSeekStart,  
   IDebugCodeContext2 pCodeContext,  
   ulong              uCodeLocationId,  
   long               iInstructions  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwSeekStart`  
 中 [SEEK_START](../../../extensibility/debugger/reference/seek-start.md) 枚举中的一个值，该值指定开始查找进程的相对位置。  
  
 `pCodeContext`  
 中 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象，表示查找操作所相对的代码上下文。 仅当使用时才使用此参数 `dwSeekStart`  =  `SEEK_START_CODECONTEXT` ; 否则，此参数将被忽略，并且可以为 null 值。  
  
 `uCodeLocationId`  
 中查找操作所相对的代码位置标识符。 如果使用此参数，则使用此参数 `dwSeekStart`  =  `SEEK_START_CODELOCID` ; 否则，将忽略此参数，并可将其设置为0。 有关代码位置标识符的说明，请参阅 [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) 方法的 "备注" 部分。  
  
 `iInstructions`  
 中相对于中指定的位置移动的指令数 `dwSeekStart` 。 如果向后移动，此值可以为负数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果查找位置到可用指令列表之外的点，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果查找到列表开头之前的位置，则将读取位置设置为列表中的第一个指令。 如果 "查看" 的位置晚于列表末尾，则会将 "读取位置" 设置为列表中的最后一个指令。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)   
 [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
