---
title: 错误：站点使用 IP 地址 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.webdbg_siteusesipaddress
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: b2b8ddc8-746d-46e3-87a6-b956b1ee048d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 46eace1c566a2810c5914a49654f8393f425fdee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155749"
---
# <a name="error-site-uses-ip-address"></a>错误：站点使用 IP 地址
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

调试器尝试自动附加到正在使用 IP 地址的 Web 应用程序时，会发生该错误。 如果在 IIS 中将“网站标识”更改为“使用特定 IP 地址”，会发生这种情况   。  
  
 要使自动附加能够工作，需要创建具有特定 IP 地址而不只是计算机名称的项目。 否则，调试器会将计算机名称更改为 localhost，而这会导致无法将调试谓词发送到 IIS。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
1. 改用手动附加（从“调试”菜单中选择“附加到进程”）  。  
  
     — 或 —  
  
2. 更改“IIS 网站标识”设置  。  
  
## <a name="see-also"></a>请参阅  
 [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
