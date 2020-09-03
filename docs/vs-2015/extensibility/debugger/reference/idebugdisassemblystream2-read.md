---
title: IDebugDisassemblyStream2：： Read |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 520c801a0603f2c6d3228ae95ad144827eac0088
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203004"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

从反汇编流中的当前位置开始读取指令。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Read(   
   DWORD                     dwInstructions,  
   DISASSEMBLY_STREAM_FIELDS dwFields,  
   DWORD*                    pdwInstructionsRead,  
   DisassemblyData*          prgDisassembly  
);  
```  
  
```csharp  
int Read(   
   uint                           dwInstructions,  
   enum_DISASSEMBLY_STREAM_FIELDS dwFields,  
   out uint                       pdwInstructionsRead,  
   DisassemblyData[]              prgDisassembly  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwInstructions`  
 中要反汇编的指令数。 此值也是数组的最大长度 `prgDisassembly` 。  
  
 `dwFields`  
 中 [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) 枚举中的标志的组合，指示要填写的字段 `prgDisassembly` 。  
  
 `pdwInstructionsRead`  
 弄返回实际反汇编的指令数。  
  
 `prgDisassembly`  
 弄一个 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 结构数组，其中使用反汇编的代码填充，每个反汇编指令一个结构。 此数组的长度由 `dwInstructions` 参数决定。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 可以通过调用 [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md) 方法来获取当前范围内可用的指令的最大数量。  
  
 从中读取下一条指令的当前位置可以通过调用 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) 方法进行更改。  
  
 `DSF_OPERANDS_SYMBOLS`可以将标志添加到 `DSF_OPERANDS` 参数中的标志 `dwFields` ，以指示在反汇编指令时应使用符号名称。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)   
 [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)   
 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)   
 [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)   
 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
