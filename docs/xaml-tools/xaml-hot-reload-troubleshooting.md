---
title: 排查 XAML 热重载问题
description: 修复了 XAML 热重载可能会遇到的问题。
ms.date: 09/04/2019
ms.topic: troubleshooting
helpviewer_keywords:
- xaml edit and continue, troubleshooting
- xaml hot reload, troubleshooting
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 73d8653b2bcf06801c18e21d9a13b21843abc7d7
ms.sourcegitcommit: 9de7d25056da59df0941508c80c0b12766ba6580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2020
ms.locfileid: "82921249"
---
# <a name="troubleshooting-xaml-hot-reload"></a>排查 XAML 热重载问题

此故障排除指南包括的详细说明应解决阻止 XAML 热重载正常工作的大多数问题。

WPF 和 UWP 应用支持 XAML 热重载。 有关操作系统和工具要求的详细信息，请参阅[通过 Xaml 热重载编写和调试正在运行的 xaml 代码](xaml-hot-reload.md)。

## <a name="hot-reload-is-not-available"></a>热重载不可用

调试应用时，如果在应用内工具栏中看到消息 "热重载不可用"，请按照本文中所述的说明解决此问题。

## <a name="verify-that-xaml-hot-reload-is-enabled"></a>验证是否启用了 XAML 热重载

默认情况下启用此功能。 开始调试应用时，请确保看到应用内工具栏，该工具栏确认 XAML 热重载可用：

![XAML 热重载可用](../debugger/media/xaml-hot-reload-available.png)

如果看不到应用内工具栏，请打开 "**常规****调试** > **选项** > "。 请确保选择 "**启用 xaml 的 UI 调试工具**并**启用 xaml 热重载**" 这两个选项。

![启用 XAML 热重载](../debugger/media/xaml-hot-reload-enable.png)

如果选择了这些选项，则请跳到 "实时可视化树" （**调试** > **Windows** > **实时可视化树**），并确保已选中 "**在应用程序工具栏中显示运行时工具**" 按钮（位于最左侧）。

![启用 XAML 热重载](../debugger/media/xaml-hot-reload-show-runtime-tools.png)

## <a name="verify-that-you-use-start-debugging-rather-than-attach-to-process"></a>验证是否使用 "启动调试" 而不是 "附加到进程"

XAML 热重载要求在应用程序启动`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`时将环境变量设置为1。 Visual Studio 会自动将其设置为 "**调试** > " "**启动调试**" （或**F5**）命令的一部分。 如果要将 XAML 热重载与**Debug** > **Attach to Process**命令一起使用，则需自行设置环境变量。

> [!NOTE]
> 若要设置环境变量，请使用 "开始" 按钮搜索 "环境变量"，然后选择 "**编辑系统环境变量**"。 在打开的对话框中，选择 "**环境变量**"，然后将其添加为用户变量，并将值设置`1`为。 若要清理，请在完成调试后删除变量。

## <a name="verify-that-your-msbuild-properties-are-correct"></a>验证 MSBuild 属性是否正确

默认情况下，调试配置中包含源信息。 它通过项目文件中的 MSBuild 属性（例如 * .csproj）进行控制。 对于 WPF，属性是`XamlDebuggingInformation`，它必须设置为。 `True` 对于 UWP，属性为`DisableXbfLineInfo`，它必须设置为。 `False` 例如：

WPF：

`<XamlDebuggingInformation>True</XamlDebuggingInformation>`

UWP

`<DisableXbfLineInfo>False</DisableXbfLineInfo>`

## <a name="verify-that-you-are-using-the-correct-build-configuration-name"></a>验证您使用的是正确的生成配置名称

必须手动设置正确的 MSBuild 属性以支持 XAML 热重载（请参阅上一节），或者必须使用默认的生成配置名称（调试）。 如果未正确设置 MSBuild 属性，自定义生成配置名称将不起作用，也不会发布版本。

## <a name="verify-that-your-xaml-file-has-no-errors"></a>验证你的 XAML 文件没有错误

如果 XAML 文件在**错误列表**中显示错误，则 Xaml 热重载可能不起作用。

## <a name="see-also"></a>另请参阅

[通过 XAML 热重载编写和调试正在运行的 XAML 代码](xaml-hot-reload.md)
