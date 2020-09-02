---
title: SccIsMultiCheckoutEnabled 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65641803c1fdcb4645bbc20f6cbc845e5d326689
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200059"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数检查源代码管理插件是否允许对文件进行多次签出。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccIsMultiCheckoutEnabled(  
   LPVOID pContext,  
   LPBOOL pbMultiCheckout  
);  
```  
  
#### <a name="parameters"></a>参数  
 pContext  
 中源代码管理插件上下文结构。  
  
 pbMultiCheckout  
 弄指定是否为此项目启用多个签出 (非零表示支持多个签出) 。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|检查已成功。|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 IDE 进行两次检查以确定文件是否可由多个用户同时签出。 首先，源代码管理系统必须支持多个签出。 源代码管理插件可以通过指定在初始化期间指定此功能 `SCC_CAP_MULTICHECKOUT` 。 此后，作为第二个检查，IDE 将调用此函数来确定当前项目是否支持多个签出。 如果所选项目支持多个签出，则插件将返回成功代码，并将设置 `pbMultiCheckout` 为非零 (`TRUE`) 或 `FALSE` 。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
