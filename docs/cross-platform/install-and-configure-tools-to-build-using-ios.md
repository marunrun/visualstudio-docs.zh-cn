---
title: 安装并配置使用 iOS 进行构建的工具 | Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: d0c311c9-9eb9-42c5-ba07-25604362cd28
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 411ab7f097a82fa850e3850c662d378f51ffd548
ms.sourcegitcommit: 32144a09ed46e7223ef7dcab647a9f73afa2dd55
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586822"
---
# <a name="install-and-configure-tools-to-build-using-ios"></a>安装并配置使用 iOS 进行构建的工具

可以使用用于跨平台移动开发的 Visual C++ 来编辑、调试 iOS 代码，并将其部署到 iOS 仿真程序或 iOS 设备，但由于许可限制，该代码必须在 Mac 上远程生成和运行。 若要使用 Visual Studio 生成和运行 iOS 应用，需要在 Mac 上安装并配置远程代理 [vcremote](https://go.microsoft.com/fwlink/p/?LinkId=534988)。 该远程代理会处理来自 Visual Studio 的生成请求，并在连接到 Mac 的 iOS 设备上或 Mac 上的 iOS 仿真程序中运行应用。

> [!NOTE]
> 有关使用云托管的 Mac 服务而不是 Mac 的信息，请参阅[配置 Visual Studio 以连接到云托管的 Mac](/visualstudio/cross-platform/tools-for-cordova/tips-workarounds/host-a-mac-in-the-cloud?view=toolsforcordova-2017#configure-visual-studio-to-connect-to-your-cloud-hosted-mac)。 此说明适用于使用 Visual Studio Tools for Apache Cordova 进行生成。 要通过 C++ 使用指令进行生成，请将 vcremote 替换为 remotebuild。

使用 iOS 进行生成的工具安装完成后，请参阅本主题，了解如何快速配置和更新远程代理以便在 Visual Studio 中和 Mac 上进行 iOS 开发。

## <a name="prerequisites"></a>系统必备

若要安装和使用远程代理以开发 iOS 代码，必须首先具备以下先决条件：

- 运行 macOS Mojave 10.14 版或更高版本的 Mac 计算机

- [Apple ID](https://appleid.apple.com/)

- 有效的 [Apple 开发人员计划](https://developer.apple.com/programs/)帐户

   可以获得一个允许将应用旁加载到 iOS 设备的免费帐户，该帐户仅用于测试，不适用于分发。

- [Xcode](https://developer.apple.com/xcode/downloads/) 10.2.1 版或更高版本

   可从 App Store 下载 Xcode。

- Xcode 命令行工具

   若要安装 Xcode 命令行工具，请打开 Mac 上的 Terminal 应用并输入以下命令：

   `xcode-select --install`

- 在 Xcode 中配置的 Apple ID 帐户作为用于对应用进行签名的签名标识

   若要查看或设置 Xcode 中的签名标识，打开 **Xcode** 菜单并选择  “首选项”。 选择“帐户”  并选择你的 Apple ID，然后选择“查看详细信息”  按钮。 有关详细说明，请参阅 [Add your Apple ID account](https://help.apple.com/xcode/mac/current/#/devaf282080a)（添加 Apple ID 帐户）。
   
   有关签名要求的详细信息，请参阅 [What is app signing](https://help.apple.com/xcode/mac/current/#/dev3a05256b8)（什么是应用签名）。 

- 如果你使用 iOS 设备进行开发，Xcode 中已为你的设备配置了预配配置文件

   Xcode 提供自动签名，并根据需要创建签名证书。 有关 Xcode 自动签名的详细信息，请参阅 [automatic signing](https://help.apple.com/xcode/mac/current/#/dev80cc24546)（自动签名）。

   如果要进行手动签名，则需要为应用创建预配配置文件。 有关创建预配配置文件的详细信息，请参阅[创建开发预置描述文件](https://help.apple.com/developer-account/#/devf2eb157f8)。 

- [Node.js](https://nodejs.org/) 8.11.3 版和 npm 5.6.0 版

   在 Mac 上安装 Node.js 8.11.3 版。 如果安装 Node.js 包，该包应随附 npm 5.6.0 版。 请注意，其他版本的 Node.js 和 npm 可能不支持远程代理 vcremote 中使用的一些模块，这可能导致 vcremote 安装失败。

## <a name="Install"></a> 安装适用于 iOS 的远程代理

当安装用于跨平台移动开发的 Visual C++ 时，Visual Studio 可以与 [vcremote](https://go.microsoft.com/fwlink/p/?LinkId=534988)进行通信，这是一个在 Mac 上运行的远程代理，用于传输文件、生成和运行 iOS 应用，以及发送调试命令。

安装远程代理之前，请确保已经满足[先决条件](#prerequisites)并安装了[用于跨平台移动开发的 Visual C++](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md#install-the-tools)。

### <a name="DownloadInstall"></a> 下载和安装远程代理

- 在 Mac 上的 Terminal 应用中，输入：

   `sudo npm install -g --unsafe-perm vcremote`

   全局安装 ( **-g**) 开关是推荐使用而不是必须使用的。

   在安装期间，vcremote 将被安装在你的 Mac 上，同时将激活开发人员模式。 同时还会安装[Homebrew](https://brew.sh/) 以及 vcremote lib 和 vcremote-utils 这两个 npm 包。 安装完成后，可以忽略有关跳过可选依赖项的警告。

   > [!NOTE]
   > 若要安装 Homebrew，你必须具有 sudo（管理员）访问权限。 如果你不想以 sudo 份安装 vcremote，你可以在 usr/local 位置手动安装 Homebrew 并将其 bin 文件夹添加到你的路径。 有关详细信息，请参阅 [Homebrew 文档](https://github.com/Homebrew/homebrew/wiki/Installation)。 若要手动启用开发人员模式，请在 Terminal 应用中输入以下命令： `DevToolsSecurity -enable`

如果更新到新版本的 Visual Studio，那么必须将远程代理也更新到最新版本。 若要更新远程代理，请重复下载并安装远程代理的步骤。

## <a name="Start"></a> 启动远程代理

必须运行远程代理才能通过 Visual Studio 生成并运行 iOS 代码。 Visual Studio 必须先与远程代理配对，然后才能进行通信。 默认情况下，远程代理在安全的连接模式下运行，此模式下需要 PIN 才能与 Visual Studio 配对。

### <a name="RemoteAgentStartServer"></a> 若要启动远程代理

- 在 Mac 上的 Terminal 应用中，输入：

   `vcremote`

   这将启动默认生成目录为 ~/vcremote 的远程代理。 有关其他配置选项，请参阅 [Configure the remote agent on the Mac](#ConfigureMac)。

第一次启动代理和每次创建新客户端证书时，将向你提供在 Visual Studio 中配置代理所需的信息，包括主机名、端口和 PIN。

![使用 vcremote 生成安全 PIN](../cross-platform/media/cppmdd_vcremote_generateclientcert.png "CPPMDD_vcremote_generateClientCert")

如果打算在 Visual Studio 中使用主机名配置远程代理，请使用该主机名从 Windows 对 Mac 进行 ping 操作，以确认它是可连接的。 否则，你可能需要使用 IP 地址。

生成的 PIN 是一次性的，并仅在有限时间内有效。 如果在此有限时间内未将 Visual Studio 与远程代理进行配对，则需要生成一个新的 PIN。 有关详细信息，请参阅 [Generate a new security PIN](#GeneratePIN)。

你可以在非安全模式下使用远程代理。 在非安全模式下，无需使用 PIN 即可将远程代理与 Visual Studio 进行配对。

#### <a name="to-disable-secured-connection-mode"></a>禁用安全连接模式

- 若要禁用 vcremote 中的安全连接模式，请在 Mac 上的 Terminal 应用中输入以下命令：

   `vcremote --secure false`

#### <a name="to-enable-secured-connection-mode"></a>启用安全连接模式

- 若要启用安全连接模式，请输入此命令：

   `vcremote --secure true`

启动远程代理后，即可从 Visual Studio 使用该代理，直到你停用它。

#### <a name="to-stop-the-remote-agent"></a>停用远程代理

- 在正在运行 vcremote 的终端窗口中，输入 Control+C   。

## <a name="ConfigureVS"></a> 在 Visual Studio 中配置远程代理

若要从 Visual Studio 连接到远程代理，必须在 Visual Studio 选项中指定远程配置。

### <a name="to-configure-the-remote-agent-from-visual-studio"></a>从 Visual Studio 配置远程代理

1. 如果代理尚未在 Mac 上运行，请遵循 [启动远程代理](#Start)中的步骤。 你的 Mac 必须正在运行 vcremote，Visual Studio 才能顺利配对、连接和生成项目。

1. 在你的 Mac 上，获取 Mac 的主机名或 IP 地址。

   可以通过在终端窗口中使用 **ifconfig** 命令来获取 IP 地址。 请使用活动网络接口下列出的 inet 地址。

1. 在 Visual Studio 菜单栏上，依次选择“工具”  和“选项”  。

1. 在“选项”  对话框中，展开“跨平台”  、“C++”  和“iOS”  。

1. 在“主机名”  和“端口”  字段，输入远程代理在启动时指定的值。 主机名可以是 DNS 名或 Mac 的 IP 地址。 默认端口为 3030。

   > [!NOTE]
   > 如果无法使用主机名 ping Mac，则可能需要使用 IP 地址。

1. 如果以默认安全连接模式使用远程代理，请勾选“安全”  复选框，然后在 **Pin** 字段输入由远程代理指定的 PIN 值。 如果以非安全连接模式使用远程代理，请清除“安全”  复选框并将 **Pin** 字段留空。

1. 选择“配对”  以启用配对。

   ![为 iOS 版本配置 vcremote 连接](../cross-platform/media/cppmdd_options_ios.PNG "CPPMDD_Options_iOS")

   除非更改主机名或端口，否则配对会一直存在。 如果在“选项”  对话框中更改了主机名或端口，要撤销此更改，请选择“还原”  按钮以还原到上一配对。

   如果配对失败，请按照 [Start the remote agent](#Start)中的步骤验证远程代理是否正在运行。 如果生成远程代理 PIN 后已经过了很久，请在 Mac 上执行 [Generate a new security PIN](#GeneratePIN) 中的步骤，然后重试。 如果你使用的是 Mac 的主机名，请转而尝试在“主机名”  字段中使用 IP 地址。

1. 更新“远程根目录”字段中的文件夹名称，以在 Mac 上的主 (~) 目录中指定远程代理所用的文件夹   。 默认情况下，远程代理会使用 /Users/`username`/vcremote 作为远程根目录。

1. 选择“确定”  以保存远程配对连接设置。

你每次在 Visual Studio 时，它会使用相同信息连接到 Mac 上的远程代理。 除非你在 Mac 上生成了新的安全证书，或其主机名或 IP 地址发生了更改，否则，你无需再次将 Visual Studio 与远程代理进行配对。

## <a name="GeneratePIN"></a> Generate a new security PIN

当你第一次启动远程代理时，生成的 PIN 在有限的时间（默认 10 分钟）内有效。 如果在此有限时间段内未将 Visual Studio 与远程代理进行配对，则需要生成一个新的 PIN。

### <a name="to-generate-a-new-pin"></a>生成新的 PIN

1. 停止代理，或在你的 Mac 上打开另一个 Terminal 应用窗口并使用它输入命令。

1. 在 Terminal 应用中输入此命令：

   `vcremote generateClientCert`

   远程代理将生成一个新的临时 PIN。 若要使用新的 PIN 配对 Visual Studio，请重复 [在 Visual Studio 中配置远程代理](#ConfigureVS)中的步骤。

## <a name="GenerateCert"></a> 生成新的服务器证书

出于安全目的，将 Visual Studio 与远程代理配对的服务器证书关联到你的 Mac 的 IP 地址或主机名。 如果这些值已更改，则必须生成一个新的服务器证书，然后使用新值重新配置 Visual Studio。

### <a name="to-generate-a-new-server-certificate"></a>生成新的服务器证书

1. 停用 vcremote 代理。

1. 在 Terminal 应用中输入此命令：

   `vcremote resetServerCert`

1. 当提示进行确认时，请输入 `Y`。

1. 在 Terminal 应用中输入此命令：

   `vcremote generateClientCert`

   将生成一个新的临时 PIN。

1. 若要使用新的 PIN 配对 Visual Studio，请重复 [在 Visual Studio 中配置远程代理](#ConfigureVS)中的步骤。

## <a name="ConfigureMac"></a> Configure the remote agent on the Mac

你可以使用各种命令行选项配置远程代理。 例如，你可以指定用于接收版本请求的端口以及要在文件系统上进行维护的最大生成数量。 默认限制为 10 个生成。 远程代理会在关机时删除超过最大数量的生成。

### <a name="to-configure-the-remote-agent"></a>配置远程代理

- 若要查看远程代理命令的完整列表，请在 Terminal 应用中输入：

   `vcremote --help`

- 要禁用安全模式并启用简单的基于 HTTP 的连接，请输入：

   `vcremote --secure false`

   如果使用此选项，请在 Visual Studio 中配置代理时清除“安全”  复选框，并将“Pin”  字段留空。

- 要为远程代理文件指定位置，请输入：

   `vcremote --serverDir directory_path`

   其中， *directory_path* 是 Mac 上放置日志文件、生成项和服务器证书的位置。 默认情况下，此位置为 /Users/\<username>/vcremote  。 生成项会在此位置按照生成号进行整理。

- 若要使用后台进程以将 `stdout` 和 `stderr` 捕获至名为 server.log 的文件，请输入：

   `vcremote > server.log 2>&1 &`

   server.log 文件可能有助于解决生成问题。

- 若要通过使用配置文件而不是命令行参数来运行代理，请输入：

   `vcremote --config config_file_path`

   其中， *config_file_path* 是 JSON 格式配置文件的路径。 启动选项及其值不得包含短划线。

## <a name="troubleshoot-the-remote-agent"></a>对远程代理进行故障排除

### <a name="debugging-on-an-ios-device"></a>在设备 iOS 上进行调试

如果在 iOS 设备上进行调试不起作用，则用于与 iOS 设备通信的工具 [ideviceinstaller](https://github.com/libimobiledevice/ideviceinstaller) 可能存在故障。 此工具通常在安装 vcremote 时从 Homebrew 安装。 请按照以下步骤解决该问题。

打开终端应用并按顺序运行以下步骤来更新 ideviceinstaller 及其依赖项：

1. 确保 Homebrew 已更新

   `brew update`

1. 卸载 libimobiledevice 和 usbmuxd

   `brew uninstall --ignore-dependencies libimobiledevice`

   `brew uninstall --ignore-dependencies usbmuxd`

1. 安装最新版本的 libimobiledevice 和 usbmuxd

   `brew install --HEAD usbmuxd`

   `brew unlink usbmuxd`

   `brew link usbmuxd`

   `brew install --HEAD libimobiledevice`

1. 卸载并重新安装 ideviceinstaller

   `brew uninstall ideviceinstaller`

   `brew install ideviceinstaller`

尝试列出设备上安装的应用，以验证 ideviceinstaller 是否可以与设备通信：

`ideviceinstaller -l`

如果 ideviceinstaller 出现故障导致无法访问文件夹 `/var/db/lockdown`，请通过以下方式来更改文件夹的权限：

`sudo chmod 777 /var/db/lockdown`
    
然后，再次验证 ideviceinstaller 是否可以与设备通信。

## <a name="see-also"></a>请参阅

- [安装用于跨平台移动开发的 Visual C++](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)
