---
title: IDebugCodeContext2::GetDocumentContext |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetDocumentContext
helpviewer_keywords:
- IDebugCodeContext2::GetDocumentContext
ms.assetid: d552cc92-963f-43c1-949f-ae6b63a427b8
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 159bf0bf65aa7ccacabce30360af32bab34eba3a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190985"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取与此代码的上下文相对应的文档上下文。 文档上下文表示对应于源生成的代码，此指令的源文件中的位置。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetDocumentContext(   
   IDebugDocumentContext2** ppSrcCxt  
);  
```  
  
```csharp  
int GetDocumentContext(   
   out IDebugDocumentContext2 ppSrcCxt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppSrcCxt`  
 [out]返回[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)对应于代码上下文的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 通常情况下，文档上下文可以认为的源文件中的位置的代码上下文时的代码指令中的执行流的位置。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
