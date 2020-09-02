---
title: 错误：无法连接到计算机 &lt;name&gt;。 网络上找不到该计算机。 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.remote.dcom_disabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- DCOM, unable to connect error
ms.assetid: b584b5db-ef52-45ed-8561-1314da3cc5b8
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dd1402a476ce2dceaaaf78580b36db20c3eed24f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682560"
---
# <a name="error-unable-to-connect-to-the-machine-ltnamegt-the-machine-cannot-be-found-on-the-network"></a>错误：无法连接到计算机 &lt;name&gt;。 网络上找不到该计算机。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果满足下列某项条件，则会发生此行为：  
  
- 您与远程计算机的连接中断。  
  
- 您在远程计算机上的用户帐户被禁用。  
  
- 您在远程计算机上的密码过期。  
  
### <a name="to-resolve-this-behavior"></a>解决此问题  
  
- 确保本地计算机和远程计算机处于同一个网络中。 若要执行此操作，请使用 Microsoft Windows 资源管理器（或文件资源管理器）尝试访问远程计算机。  
  
     \- 和 -  
  
- 确保您用来连接远程计算机的用户帐户是启用的。  
  
     \- 和 -  
  
- 确保您用来连接远程计算机的密码是有效的并且尚未过期。  
  
## <a name="see-also"></a>另请参阅  
 [在设备上设置远程工具](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)   
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
