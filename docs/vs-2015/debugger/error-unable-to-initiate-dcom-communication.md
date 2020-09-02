---
title: 错误：无法启动 DCOM 通信 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.unmarshal_server_failed
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 2a7b27e6-2526-4f32-bc4d-eaee447f24ec
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fff1c56915fe4a06d66bdb08ce60219642933b1b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682531"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>错误：无法启动 DCOM 通信
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当本地计算机尝试与远程计算机通信时，发生 DCOM 错误。 这是由于远程服务器上存在防火墙或远程计算机上的 Windows 身份验证已中断。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 如果远程计算机已启用 Windows 防火墙，请参阅在 [设备上设置远程工具](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) ，以获取有关如何为本地调试配置防火墙的说明。  
  
- 若要还原 Windows 身份验证，请尝试重新启动本地计算机和远程计算机。 检查本地和远程计算机上的事件日志以找出 Kerberos 错误，并与域管理员联系以了解已知问题。  
  
## <a name="see-also"></a>另请参阅  
 [远程调试](../debugger/remote-debugging.md)
