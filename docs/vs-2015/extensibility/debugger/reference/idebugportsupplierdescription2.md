---
title: IDebugPortSupplierDescription2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e3da559a2d843ddb1129236966093b8a41f4234b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538559"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

使[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]UI 来显示内的文本**传输信息**一部分**附加到进程**对话框。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPortSupplierDescription2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 此接口由端口提供程序实现。  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDebugPortSupplierDescription2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|检索端口提供程序的说明和描述性元数据。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
