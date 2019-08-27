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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194107"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

这是对的调用中指定的回调函数[SccSetOption](../extensibility/sccsetoption-function.md) (使用选项`SCC_OPT_NAMECHANGEPFN`)，用于告知名称所做的更改源代码管理插件返回到 IDE。  
  
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
 [in]对上一个调用中指定的用户值[SccSetOption](../extensibility/sccsetoption-function.md) (使用选项`SCC_OPT_USERDATA`)。  
  
 pszOldName  
 [in]原始文件的名称。  
  
 pszNewName  
 [in]文件的名称已重命名为。  
  
## <a name="return-value"></a>返回值  
 无。  
  
## <a name="remarks"></a>备注  
 如果在源代码管理操作期间重命名文件，源代码管理插件可以通知有关通过此回调的名称更改 IDE。  
  
 如果 IDE 不支持此回调，它将不会调用[SccSetOption](../extensibility/sccsetoption-function.md)指定它。 如果该插件不支持此回调，它将返回`SCC_E_OPNOTSUPPORTED`从`SccSetOption`时 IDE 会尝试设置回调的功能。  
  
## <a name="see-also"></a>请参阅  
 [通过 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccSetOption](../extensibility/sccsetoption-function.md)
