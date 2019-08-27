---
title: SccCheckout 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f23290ebfadd1b6e3d34f808d5ea0ccccbb3c319
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200151"
---
# <a name="scccheckout-function"></a>SccCheckout 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有了完全限定的文件名的列表，此函数将它们签出到本地驱动器。 注释应用于签出的所有文件。注释参数可以是`null`字符串。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccCheckout (  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LPCSTR    lpComment,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 pvContext  
 [in]源控制插件上下文结构。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 nFiles  
 [in]选择要签出文件的数量。  
  
 lpFileNames  
 [in]要签出的文件的完全限定的本地路径名称的数组。  
  
 lpComment  
 [in]若要应用于每个签出所选文件的注释。  
  
 fOptions  
 [in]命令标志 (请参阅[位标志由特定命令](../extensibility/bitflags-used-by-specific-commands.md))。  
  
 pvOptions  
 [in]源代码管理插件特定选项。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|签出成功。|  
|SCC_E_FILENOTCONTROLLED|所选的文件不是源代码管理下。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|  
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|  
|SCC_E_NONSPECIFICERROR|非特定故障。 未签出文件。|  
|SCC_E_ALREADYCHECKEDOUT|用户已签出该文件。|  
|SCC_E_FILEISLOCKED|文件被锁定，因此禁止创建新的版本。|  
|SCC_E_FILEOUTEXCLUSIVE|另一个用户都对此文件进行独占签出。|  
|SCC_I_OPERATIONCANCELED|在完成之前已取消操作。|  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
