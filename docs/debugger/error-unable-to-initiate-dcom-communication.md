---
title: 错误：无法启动 DCOM 通信 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.unmarshal_server_failed
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1112ec72e8aca764f749a6d8f1925302f569b17e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62850077"
---
# <a name="error-unable-to-initiate-dcom-communication"></a>错误：无法启动 DCOM 通信
当本地计算机尝试与远程计算机通信时，发生 DCOM 错误。 这是由于远程服务器上存在防火墙或远程计算机上的 Windows 身份验证已中断。

### <a name="to-correct-this-error"></a>更正此错误

- 如果远程计算机已启用 Windows 防火墙，请参阅[远程调试](../debugger/remote-debugging.md)有关如何配置防火墙以便进行本地调试的说明。

- 若要还原 Windows 身份验证，请尝试重新启动本地计算机和远程计算机。 检查本地和远程计算机上的事件日志以找出 Kerberos 错误，并与域管理员联系以了解已知问题。

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)