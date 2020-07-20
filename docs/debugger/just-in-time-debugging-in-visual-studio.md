---
title: 禁用实时调试器 | Microsoft Docs
ms.date: 05/23/2018
ms.topic: troubleshooting
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
ms.assetid: 14972d5f-69bc-479b-9529-03b8787b118f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3155c2cdc9ea3dc5208a52e5fe37f697a4ad5ef6
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86386116"
---
# <a name="disable-the-just-in-time-debugger"></a>禁用实时调试器

当正在运行的应用中出现错误时，“实时调试器”对话框可能会打开并阻止该应用继续运行。

实时调试器提供了启动 Visual Studio 来调试错误的选项。 必须安装 Visual Studio 或其他选定的调试器，才能查看有关该错误的详细信息或尝试对其进行调试。

如果你已是 Visual Studio 用户，并想要尝试对错误进行调试，请参阅[使用实时调试器进行调试](../debugger/debug-using-the-just-in-time-debugger.md)。 如果无法修复此错误，或​​者想阻止实时调试器打开，则可以[从 Visual Studio 中禁用实时调试](debug-using-the-just-in-time-debugger.md#BKMK_Enabling)。

如果你先前安装了 Visual Studio 但已将其卸载，则可能需要[从 Windows 注册表中禁用实时调试](debug-using-the-just-in-time-debugger.md#disable-just-in-time-debugging-from-the-windows-registry)。

如果尚未安装 Visual Studio，则可以通过禁用脚本调试或服务器端调试来阻止实时调试。

- 如果要尝试运行 Web 应用，请禁用脚本调试：

  在 Windows“控制面板” > “网络和 Internet” > “Internet 选项”中，选择“禁用脚本调试(Internet Explorer)”和“禁用脚本调试(其他)”    。 确切的步骤和设置取决于你的 Windows 和浏览器版本。

  ![JIT Internet 选项](../debugger/media/jitinternetoptions.png "JIT Internet 选项")

- 如果要在 IIS 中托管 ASP.NET Web 应用，请禁用服务器端调试：

  1. 在 IIS 管理器“功能视图”的“ASP.NET”部分下，双击“.NET 编译”，或选择它，然后选择“操作”窗格中的“打开功能”    。
  1. 在“行为” > “调试”下，选择“False”  。 在较早版本的 IIS 中，步骤有所不同。

禁用实时调试后，应用可能能够处理错误并正常运行。

如果应用仍存在未处理的错误，你可能会看到错误消息，或者应用可能会崩溃或停止响应。 在错误得到修复之前，应用不会正常运行。 你可以尝试与应用的所有者联系，并要求他们对其进行修复。
