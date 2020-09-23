---
title: 本地计算机上的防火墙 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.firewall.localmachine
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
ms.openlocfilehash: 6b729c3e7e82a13d86aed16dfb52fda6864aa7f9
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852701"
---
# <a name="error-firewall-on-local-machine"></a>错误：本地计算机上的防火墙
本地计算机（运行 Visual Studio 的计算机）上的 Internet 连接防火墙未设置为允许远程调试。 为了使用默认传输进行托管或本机远程调试，必须为 DCOM 通信打开 TCP 135 端口。 必须打开文件和打印机共享，且必须将 devenv.exe 添加到例外列表。 可能还需要打开某些 IPSEC 端口。

 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。