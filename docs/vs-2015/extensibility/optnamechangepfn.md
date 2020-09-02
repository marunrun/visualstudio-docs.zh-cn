---
title: OPTNAMECHANGEPFN |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4969dff811b6517c0274a35884703a9dc0c693cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194107"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

这是使用选项) 调用 [SccSetOption](../extensibility/sccsetoption-function.md) (指定的回调函数 `SCC_OPT_NAMECHANGEPFN` ，用于将源代码管理插件所做的名称更改传递回 IDE。  
  
## <a name="signature"></a>签名  
  
```cpp#  
typedef void (*OPTNAMECHANGEPFN)(  
   LPVOID pvCallerData,  
   LPCSTR pszOldName,  
   LPCSTR pszNewName  
);  
```  
  
## <a name="parameters"></a>参数  
 pvCallerData  
 中使用 option) 在先前对 [SccSetOption](../extensibility/sccsetoption-function.md) (的调用中指定的用户值 `SCC_OPT_USERDATA` 。  
  
 pszOldName  
 中文件的原始名称。  
  
 pszNewName  
 中文件已重命名为的名称。  
  
## <a name="return-value"></a>返回值  
 无。  
  
## <a name="remarks"></a>备注  
 如果在源代码管理操作期间重命名了某个文件，则源代码管理插件可以通过此回调通知 IDE 有关名称更改的信息。  
  
 如果 IDE 不支持此回调，则它将不会调用 [SccSetOption](../extensibility/sccsetoption-function.md) 来指定它。 如果插件不支持此回调，则在 `SCC_E_OPNOTSUPPORTED` `SccSetOption` IDE 尝试设置回调时，它将从函数返回。  
  
## <a name="see-also"></a>另请参阅  
 [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccSetOption](../extensibility/sccsetoption-function.md)
