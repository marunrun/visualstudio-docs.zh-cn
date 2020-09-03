---
title: IDebugProcessSecurity：： GetUserName |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202784"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取端口提供商提供的用户名。  
  
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
 弄一个包含用户名的字符串。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功，则它会返回 `S_OK`。 否则，它将返回错误代码。  
  
## <a name="remarks"></a>备注  
 `GetUserName`返回在 "**附加到进程**" 对话框的 "**用户名**" 列中显示的用户名。 若要查看 "**附加到进程**" 对话框，请在集成开发环境中的 "**工具**" 菜单上单击 "**附加到进程**" [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] (IDE) 。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
