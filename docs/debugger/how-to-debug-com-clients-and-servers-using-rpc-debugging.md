---
title: 使用 RPC 调试来调试 COM 客户端和服务器 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- RPC (Remote Procedure Call), debugging COM clients and servers
- COM, debugging
- RPC (Remote Procedure Call)
- RPC (Remote Procedure Call), debugging
- COM clients, debugging
- COM servers, debugging
- out-of-process remote procedure call debugging
- remote debugging, RPC (Remote Procedure Call)
- in-process remote procedure call debugging
ms.assetid: 3e8526c8-43b5-4b87-8e0d-b22c24f0a3ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83fdfa65f4efb6f0bc0b99eac27ae0e57c79e3cd
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733694"
---
# <a name="how-to-debug-com-clients-and-servers-using-rpc-debugging"></a>如何：使用 RPC 调试来调试 COM 客户端和服务器
可以使用远程过程调用 (RPC) 调试来调试 COM 客户端/服务器应用程序。 必须启用 RPC 调试才能使用它。 启用 RPC 调试后，当单步执行来自客户端的服务器调用时，调试器会附加到服务器上，使你能调试其代码。 附加调试器后，就可以对客户端和服务器进程使用所有的调试器功能。

### <a name="to-enable-rpc-debugging"></a>启用 RPC 调试

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在“选项”对话框中，单击“调试”文件夹。

3. 单击“本机”页。

4. 选中“RPC 调试”复选框。

    > [!NOTE]
    > 必须拥有“管理员”或“超级用户”权限，才能调试 RPC 调用。

    > [!NOTE]
    > 仅当将本机调试器附加到远程服务器时，RPC 才能进入运行 Microsoft Windows Vista 的远程服务器并单步执行。 否则，RPC 调用将失败并且不显示错误消息。 或者，RPC 调用可以完成，但无法单步执行 RPC 调用。

## <a name="see-also"></a>请参阅
- [调试 COM 服务器和容器](../debugger/com-server-and-container-debugging.md)
- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)