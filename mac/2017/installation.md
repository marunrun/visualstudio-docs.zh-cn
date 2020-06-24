---
title: 安装 Visual Studio 2017 for Mac
description: 有关如何安装 Visual Studio for Mac 和跨平台开发所需附加组件的说明。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/03/2018
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.custom: video
ms.openlocfilehash: 962ca0cf3960195ffabefb5a9bd2c6cc7e72590c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289412"
---
# <a name="install-visual-studio-2017-for-mac"></a>安装 Visual Studio 2017 for Mac

> [!NOTE]
> Visual Studio 2019 for Mac [现已推出](installation.md?view=vsmac-2019)。 对于较旧版本的 Visual Studio for Mac，请参阅 Visual Studio [下载页](https://my.visualstudio.com/Downloads?q=Visual%20Studio%202017%20for%20Mac)。

## <a name="downgrading-from-visual-studio-2019-for-mac"></a>从 Visual Studio 2019 for Mac 降级？

为获得最佳体验，降级之前，应确保[卸载](uninstall.md) Visual Studio 2019 for Mac。 如果遇到导致下载的问题，请务必通过[报告问题](report-a-problem.md)让我们知道。
 
## <a name="requirements"></a>要求

下载 Visual Studio for Mac 后，要开始开发本机跨平台应用，还需先安装并设置一些其他内容。

要结合使用 iOS 和 Visual Studio，需要以下各项：

- 配备 macOS High Sierra 10.13 或更高版本的 Mac。
- Xcode 9.3 或更高版本。 通常建议使用稳定的最新版本。
- 一个 Apple ID。 如果没有 Apple ID，请在 https://appleid.apple.com 新建一个。 需要 Apple ID 才可安装和登录 Xcode。

## <a name="install"></a>安装

1. 从 [my.visualstudio.com](https://my.visualstudio.com/Downloads?q=Visual%20Studio%202017%20for%20Mac) 下载 Visual Studio for Mac

2. 下载安装包后，单击“VisualStudioForMacInstaller.dmg”文件装载安装程序，然后通过双击徽标运行它，如下图所示：

   ![安装程序对话框](media/installer-image1.png)

3. 系统可能会通过警报对话框发出提示，如下图所示。 在此情况下，请单击“打开”：

   ![警报对话框](media/installer-image2.png)

4. 安装程序会检查系统，确定需要安装或更新的组件：

   ![评估系统](media/installer-image3.png)

5. 之后，会出现一个警报对话框，要求确认隐私和许可条款。 按“继续”按钮接受条款：

   ![许可对话框](media/installer-image4.png)

6. 安装程序会列出缺少和需要下载并安装的所需组件。 在此处选择要下载的产品：

   ![选择项](media/installer-image5.png)

   如果不希望安装所有平台，请参阅以下指南，它们有助于确定要安装的平台：

   * **使用 Xamarin 的应用**：
      - Xamarin.Forms - 选择“Android”和“iOS”平台。
      - 仅限 iOS - 选择“iOS”平台（请注意，需要安装 [Xcode](https://developer.apple.com/xcode/)）。
      - 仅限 Android - 选择“Android”平台（请注意，还应选择相关依赖项）。
      - 仅限 Mac - 选择“macOS”平台（请注意，需要安装 [Xcode](https://developer.apple.com/xcode/)）。
      - 完全跨平台的 Xamarin 应用 - 选择“Android”、“iOS”和“macOS”平台。
   * **.NET Core 应用程序** - 选择“.NET Core”平台。
   * **ASP.NET Core Web 应用程序** - 选择“.NET Core”平台。
   * **跨平台 Unity 游戏开发** - 除 Visual Studio for Mac 之外，无需安装其他任何平台。 若要详细了解如何安装 Unity 扩展，请参阅 [Unity 安装指南](/visualstudio/mac/setup-vsmac-tools-unity)。

   此安装屏幕显示每个组件的版本和大小。 可单击每个组件查看该组件的依赖项列表（对于 Android），该组件下载的其他包（对于 .NET Core），或任何其他所需应用程序（对于 iOS 和 macOS）：

   ![Android 附加依赖项](media/installer-image6.png)

7. 确认选择后，选择“安装和更新”按钮开始安装过程。

8. 安装程序会启动所选项的下载和安装过程：

   ![开始安装](media/installer-image7.png)

   ![下载 Xamarin.Mac](media/installer-image8.png)

   ![完成安装](media/installer-image9.png)

9. 系统可能会提示为完成安装所需的各个组件提升必要的权限。 在此处输入管理员凭据以继续安装过程：

   ![输入权限以继续执行安装程序](media/installer-image10.png)

10. 安装成功后，可通过按“开始”，开始在 Visual Studio 中开发应用：

    ![打开 Visual Studio](media/installer-image11.png)

> [!NOTE]
> 如果在原始安装期间选择不安装平台或工具（通过在步骤 #6 中取消选择相关选项），且希望稍后添加该组件，必须再次运行[安装程序](https://visualstudio.microsoft.com/vs/)。

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>在防火墙或代理服务器后安装 Visual Studio for Mac

若要在防火墙后面安装 Visual Studio for Mac，必须将某些终结点设置为可供访问，以允许下载所需的工具和更新软件。

配置网络以允许访问下列位置：

- [Visual Studio 终结点](/visualstudio/install/install-visual-studio-behind-a-firewall-or-proxy-server)

## <a name="next-steps"></a>后续步骤

安装 Visual Studio for Mac 后，可以开始编写应用代码。 下面的指南逐步介绍了如何完成后续步骤，即编写和部署项目。

### <a name="ios"></a>iOS

1. [Hello，iOS](https://developer.xamarin.com/guides/ios/getting_started/hello,_iOS/)
2. [设备预配](https://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning)（以在设备上运行应用程序）。

### <a name="android"></a>Android

1. [使用 Xamarin Android SDK 管理器](https://developer.xamarin.com/guides/android/getting_started/installation/android-sdk/?ide=xs)
2. [Android SDK 仿真器](https://developer.xamarin.com/guides/android/getting_started/installation/android-emulator/)
4. [设置设备进行开发](https://developer.xamarin.com/guides/android/getting_started/installation/set_up_device_for_development/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>.NET Core 应用、ASP.NET Core Web 应用、Unity 游戏开发

有关其他工作负载，请参阅[工作负载](/visualstudio/mac/workloads)页。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Acquisition/player]

## <a name="see-also"></a>请参阅

- [安装 Visual Studio 2017 (Windows)](/visualstudio/install/install-visual-studio)
