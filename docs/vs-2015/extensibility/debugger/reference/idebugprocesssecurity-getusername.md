---
title: IDebugProcessSecurity::GetUserName |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 17a6ef52d7df1c60b0cb6581a7e15eeaf67e7875
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202784"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

从端口提供程序获取用户名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetUserName(  
    BSTR *pbstrUserName  
);  
```  
  
```csharp  
int GetUserName (  
    string pbstrUserName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrUserName`  
 [out]包含的用户名称的字符串。  
  
## <a name="return-value"></a>返回值  
 如果此方法成功，它将返回`S_OK`。 否则，它返回一个错误代码。  
  
## <a name="remarks"></a>备注  
 `GetUserName` 返回在显示的用户名**用户名**的列**附加到进程**对话框。 若要查看**附加到进程**对话框中，单击**附加到进程**上**工具**菜单中的[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]集成的开发环境 (IDE)。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
