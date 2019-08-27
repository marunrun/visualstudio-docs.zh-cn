---
title: SccGetUserOption 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetUserOption
helpviewer_keywords:
- SccGetUserOption function
ms.assetid: 17863747-1901-4c53-a2b3-ed996085e120
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bd00a2b669b806b09a6ae221b2ba2e03f8d45ceb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200072"
---
# <a name="sccgetuseroption-function"></a>SccGetUserOption 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数检索各种特定于用户的选项。  
  
## <a name="syntax"></a>语法  
  
```cpp  
SCCRTN SccGetUserOption(  
   LPVOID pContext,  
   LONG nOption,  
   LPLONG lpVal  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 pContext  
 [in]源控件插件上下文指针。  
  
 nOption  
 [in]若要检索 （有关可能的选项，请参阅备注） 的选项。  
  
 lpVal  
 [out]与选项相关联的值。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|SCC_OK|已成功检索选项。|  
|SCC_E_OPNOTSUPPORTED|不支持选项。|  
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|  
  
## <a name="remarks"></a>备注  
 此命令支持以下选项：  
  
|用户选项|描述|  
|-----------------|-----------------|  
|`SCC_USEROPT_CHECKOUT_LOCALVER`|确定用户是否想要签出本地版本的文件。 `lpVal` 分配`SCC_USEROPT_COLV_YES`（用户想要签出本地文件） 或`SCC_USEROPT_COLV_NO`。|  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [错误代码](../extensibility/error-codes.md)
