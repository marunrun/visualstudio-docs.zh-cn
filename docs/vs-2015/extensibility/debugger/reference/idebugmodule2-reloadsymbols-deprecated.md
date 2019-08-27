---
title: IDebugModule2::ReloadSymbols_Deprecated |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugModule2::ReloadSymbols
helpviewer_keywords:
- IDebugModule2::ReloadSymbols method
ms.assetid: 0f9f0133-7d58-4cd9-a6ca-1141e095749d
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ce816e20e59d407f9b3cd84e3dffa703d84a324
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189541"
---
# <a name="idebugmodule2reloadsymbolsdeprecated"></a>IDebugModule2::ReloadSymbols_Deprecated
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

已过时。 不要使用。 重新加载此模块的符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT ReloadSymbols(   
   LPCOLESTR pszUrlToSymbols,  
   BSTR*     pbstrDebugMessage  
);  
```  
  
```csharp  
int ReloadSymbols(   
   string     pszUrlToSymbols,  
   out string pbstrDebugMessage  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszUrlToSymbols`  
 [in]指向符号存储区的路径。  
  
 `pbstrDebugMessage`  
 [out]返回信息性消息，例如状态或错误消息，显示模块窗口中的模块名称的右侧。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 调试引擎应始终返回`E_FAIL`。  
  
## <a name="remarks"></a>备注  
 不再支持此方法。 实现[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)方法相反。  
  
## <a name="see-also"></a>请参阅  
 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)   
 [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)
