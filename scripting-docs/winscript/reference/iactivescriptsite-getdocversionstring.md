---
title: IActiveScriptSite::GetDocVersionString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.GetDocVersionString
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_GetDocVersionString
ms.assetid: ab3f892d-06d3-4cb5-9ea5-20c4a1e518cd
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7327b71329c1f476eab9c27d5e0d5a047664abfa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992740"
---
# <a name="iactivescriptsitegetdocversionstring"></a>IActiveScriptSite::GetDocVersionString
检索唯一标识当前的文档版本的主机定义的字符串。 如果 Windows 脚本 （如下所示使用记事本正在编辑的 HTML 页的情况下） 范围内已更改的相关的文档，脚本引擎可以将它保存以及其保留的状态，强制重新编译下次加载脚本。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocVersionString(  
    BSTR *pbstrVersionString  // address of document version string  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrVersionString`  
 [out]主机定义的文档版本字符串的地址。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_NOTIMPL`不支持此方法。  
  
## <a name="remarks"></a>备注  
 如果`E_NOTIMPL`返回，脚本引擎应假定该脚本是与文档同步。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)