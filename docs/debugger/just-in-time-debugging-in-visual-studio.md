---
title: 禁用在实时调试器 |Microsoft Docs
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
ms.openlocfilehash: 8c848281a89213a216bd8ec3ac1e651b6dfc32e4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905707"
---
# <a name="disable-the-just-in-time-debugger"></a>禁用实时调试器

实时调试器对话框中可能会打开正在运行的应用，在发生错误时，并阻止该应用程序继续。

实时调试器提供的选项以启动 Visual Studio 来调试错误。 您必须具有[Visual Studio](http://visualstudio.microsoft.com)或另一个选定的调试器安装以查看有关错误的详细的信息或尝试对其进行调试。

如果你是 Visual Studio 用户，并想要尝试调试错误，请参阅[使用实时调试器进行调试](../debugger/debug-using-the-just-in-time-debugger.md)。 如果无法修复此错误，或想要保留打开实时调试器，你可以[禁用在实时调试从 Visual Studio](debug-using-the-just-in-time-debugger.md#BKMK_Enabling)。

如果必须安装 Visual Studio，但不是能再执行操作，可能需要[禁用在实时调试从 Windows 注册表](debug-using-the-just-in-time-debugger.md#disable-just-in-time-debugging-from-the-windows-registry)。

如果您尚未安装 Visual Studio，可以阻止在实时调试通过禁用脚本调试或服务器端调试。

- 如果您正在尝试运行 web 应用，禁用脚本调试：

  在 Windows 中**Control Panel** > **网络和 Internet** > **Internet 选项**，选择**禁用脚本调试 （Internet 资源管理器）** 并**禁用脚本调试 （其他）** 。 确切的步骤和设置取决于您的 Windows 和你的浏览器版本。

  ![JIT Internet 选项](../debugger/media/jitinternetoptions.png "JIT internet 选项")

- 如果要承载在 IIS 中的 ASP.NET web 应用，请禁用服务器端调试：

  1. 在 IIS 管理器**功能视图**下**ASP.NET**部分中，双击 **.NET 编译**，或选择它，然后选择**打开功能**中**操作**窗格。
  1. 下**行为** > **调试**，选择**False**。 步骤是在较旧版本的 IIS 不同。

禁用在实时调试后，应用程序可能能够处理错误和正常运行。

如果应用程序仍然具有未处理的错误，可能会看到错误消息，或应用程序可能会崩溃或挂起。 修复该错误之前，应用程序不会正常运行。 你可以尝试以与应用程序的所有者联系并要求他们修复此错误。
