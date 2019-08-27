---
title: IDebugProperty3::CreateObjectID | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0035faad9078acd70886d597f039c0d8de5ee12f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63403210"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建此属性的唯一 ID，以确保它是唯一的而所有其他属性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CreateObjectID(  
   void  
);  
```  
  
```csharp  
int CreateObjectID();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 当会话调试管理器想要确保此属性唯一地标识在所有其他属性之间时，调用此方法。 调试引擎 (DE) 支持此方法，除非已唯一标识它可以处理的属性。 如果设备不支持此方法，它将返回`E_NOTIMPL`。  
  
 使用创建的任何唯一 ID`CreateObjectID`时销毁[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)调用方法; 这也表示用于唯一地标识此属性需要的结束。  
  
> [!NOTE]
> 没有方法来检索此唯一 ID，因此 DE 可以随意的唯一 Id 时`CreateObjectID`调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
