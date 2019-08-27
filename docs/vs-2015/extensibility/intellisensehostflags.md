---
title: IntelliSenseHostFlags |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IntellisenseHostFlags
helpviewer_keywords:
- IntelliSense, IntellisenseHostFlags enumeration
- IntellisenseHostFlags enumeration
ms.assetid: 0930640b-eb84-48ef-a8f7-d4268f55c99c
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 12945998b215e9082591fad514bd9c16ab789405
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203882"
---
# <a name="intellisensehostflags"></a>IntelliSenseHostFlags
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定 IntelliSense 主机标志。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum IntellisenseHostFlags  
{  
    IHF_READONLYCONTEXT      = 0x00000001  
    IHF_NOSEPARATESUBJECT    = 0x00000002  
    IHF_SINGLELINESUBJECT    = 0x00000004  
    IHF_FORCECOMMITTOCONTEXT = 0x00000008  
    IHF_OVERTYPE             = 0x00000010  
};  
```  
  
#### <a name="parameters"></a>参数  
  
|成员|描述|  
|-------------|-----------------|  
|`IHF_READONLYCONTEXT`|上下文缓冲区是只读的。|  
|`IHF_NOSEPARATESUBJECT`|没有使用者的文本。 上下文缓冲区包含 IntelliSense 目标 (意味着`!IHF_READONLYCONTEXT`)。|  
|`IHF_SINGLELINESUBJECT`|不支持多行的主题文本。|  
|`IHF_FORCECOMMITTOCONTEXT`|与 `CanCommitIntoReadOnlyBuffer` 相同。|  
|`IHF_OVERTYPE`|应在改写模式下编辑 （在使用者或上下文）。|  
  
## <a name="requirements"></a>要求  
 SingleFileeditor.idl  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop>
