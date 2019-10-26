---
title: 禁用实时调试器 |Microsoft Docs
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
ms.openlocfilehash: 0024716875dce7e81567d60a6e61069be64ec185
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911455"
---
# <a name="disable-the-just-in-time-debugger"></a>禁用实时调试器

当正在运行的应用程序中出现错误时，可以打开 "实时调试器" 对话框，并阻止应用程序继续。

实时调试器提供了启动 Visual Studio 以调试错误的选项。 必须安装[Visual Studio](https://visualstudio.microsoft.com/)或另一个选定的调试器，才能查看有关错误的详细信息或尝试对其进行调试。

如果你是 Visual Studio 用户，并且想要尝试调试错误，请参阅[使用实时调试器进行调试](../debugger/debug-using-the-just-in-time-debugger.md)。 如果无法修复此错误，或要使实时调试器无法打开，则可以[从 Visual Studio 中禁用实时调试](debug-using-the-just-in-time-debugger.md#BKMK_Enabling)。

如果已安装 Visual Studio，但不再执行此操作，则可能需要[从 Windows 注册表中禁用实时调试](debug-using-the-just-in-time-debugger.md#disable-just-in-time-debugging-from-the-windows-registry)。

如果尚未安装 Visual Studio，则可以通过禁用脚本调试或服务器端调试来阻止实时调试。

- 如果要尝试运行 web 应用，请禁用脚本调试：

  在 Windows**控制面板**中 > **网络和 Internet** > **Internet 选项**"，选择"**禁用脚本调试（Internet Explorer）** "和"**禁用脚本调试（其他）** "。 确切的步骤和设置取决于你的 Windows 和你的浏览器的版本。

  ![JIT Internet 选项](../debugger/media/jitinternetoptions.png "JIT internet 选项")

- 如果要在 IIS 中托管 ASP.NET web 应用，请禁用服务器端调试：

  1. 在 IIS 管理器的 "**功能视图**" 的 " **ASP.NET** " 部分下，双击 " **.net 编译**"，或选择它，然后在 "**操作**" 窗格中选择 "**打开功能**"。
  1. 在 "**行为** > **调试**" 下，选择 " **False**"。 较早版本的 IIS 中的步骤不同。

禁用实时调试后，应用可能能够处理错误并正常运行。

如果应用仍出现未处理的错误，则可能会显示错误消息，或者应用可能会崩溃或挂起。 在修复错误之前，应用不会正常运行。 你可以尝试联系应用的所有者，并要求他们对其进行修复。
