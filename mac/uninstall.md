---
title: 卸载 Visual Studio for Mac
description: 卸载 Visual Studio for Mac 和相关工具的说明。
author: asb3993
ms.author: amburns
ms.date: 05/06/2018
ms.technology: vs-ide-install
ms.assetid: 4EB95F75-BC2E-4982-9564-2975805712D8
ms.openlocfilehash: 1ce74098cc8e6e4fa6856d94b7b8d99d96a1f3ab
ms.sourcegitcommit: 6f3cf7a1bfc81a61f9a603461a1c34fd2221f100
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957412"
---
# <a name="uninstalling-visual-studio-for-mac"></a>卸载 Visual Studio for Mac

可根据本指南导航到相关部分，单独卸载 Visual Studio for Mac 中的每个组件，或使用[卸载脚本](#uninstall-script)部分提供的脚本卸载所有内容。

如果之前已在计算机上安装 Xamarin Studio，则除了执行以下步骤外，可能还需按照 [Xamarin 卸载](/xamarin/cross-platform/get-started/installation/uninstalling-xamarin#uninstall-xamarin-studio-on-mac)指南中的说明进行操作。

> [!NOTE]
> 此信息仅从计算机的 Visual Studio 2019 for Mac 或 Visual Studio 2017 for Mac 中删除。 要卸载 Visual Studio Code，请参阅[此问题](https://github.com/Microsoft/vscode/issues/52151)了解详细信息。

## <a name="uninstall-script"></a>卸载脚本

可使用两个脚本来卸载计算机上的 Visual Studio for Mac 以及所有组件：

- [Visual Studio 和 Xamarin 脚本](#visual-studio-for-mac-and-xamarin-script)
- [.NET Core 脚本](#net-core-script)

以下部分提供有关下载和使用脚本的信息。

### <a name="visual-studio-for-mac-and-xamarin-script"></a>Visual Studio for Mac 和 Xamarin 脚本

可通过使用[卸载脚本](https://raw.githubusercontent.com/MicrosoftDocs/visualstudio-docs/master/mac/resources/uninstall-vsmac.sh)一次性卸载 Visual Studio 和 Xamarin 组件。

卸载脚本中包含本文中出现的大部分命令。 由于可能存在外部依赖项，因此脚本中省略了三个主要部分。 若要将此删除，请跳转到下面的相关部分，并手动删除：

- **[卸载 Mono](#uninstall-mono-sdk-mdk)**
- **[卸载 Android AVD](#uninstall-android-avd)**
- **[卸载 Android SDK 和 Java SDK](#uninstall-android-sdk-and-java-sdk)**

要运行脚本，请执行以下步骤：

1. 右键单击脚本并选择“另存为”以在 Mac 上保存文件  。
2. 打开“终端”，并将工作目录更改为下载脚本的位置：

    ```bash
    cd /location/of/file
    ```

3. 使脚本可执行，并通过 **sudo** 运行它：

    ```bash
    chmod +x ./uninstall-vsmac.sh
    sudo ./uninstall-vsmac.sh
    ```

4. 最后，删除卸载脚本，并删除停靠位置中的 Visual Studio for Mac（如果有）。

### <a name="net-core-script"></a>.NET Core 脚本

.NET Core 的卸载脚本位于 [dotnet cli 存储库](https://raw.githubusercontent.com/dotnet/cli/master/scripts/obtain/uninstall/dotnet-uninstall-pkgs.sh)

要运行脚本，请执行以下步骤：

1. 右键单击脚本并选择“另存为”以在 Mac 上保存文件  。
2. 打开“终端”，并将工作目录更改为下载脚本的位置：

    ```bash
    cd /location/of/file
    ```

3. 使脚本可执行，并通过 **sudo** 运行它：

    ```bash
    chmod +x ./dotnet-uninstall-pkgs.sh
    sudo ./dotnet-uninstall-pkgs.sh
    ```

4. 最后，删除 .NET Core 卸载脚本。

## <a name="uninstall-visual-studio-for-mac"></a>卸载 Visual Studio for Mac

从 Mac 中卸载 Visual Studio 的第一步是在 /Applications 目录中找到 Visual Studio.app，并将其拖动到回收站    。 或者，单击右键并选择“移到回收站”，如下图所示  ：

![将 Visual Studio 应用程序移动到回收站](media/uninstall-image1.png)

删除此应用包会一并删除 Visual Studio for Mac，但文件系统上仍可能存在其他与 Xamarin 相关的文件。

要删除 Visual Studio for Mac 的所有痕迹，请在终端运行以下命令：

```bash
sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
rm -rf ~/Library/Application\ Support/VisualStudio/7.0/LocalInstall/Addins/
rm -rf ~/Library/Application\ Support/VisualStudio/8.0/LocalInstall/Addins/
```

可能还要删除以下包含各种 Xamarin 文件和文件夹的目录。 不过，这样做前，应注意此目录包含 Android 签名密钥。 有关详细信息，请参阅 **[卸载 Android SDK 和 Java SDK](#uninstall-android-sdk-and-java-sdk)** 部分：

```bash
rm -rf ~/Library/Developer/Xamarin
```

## <a name="uninstall-mono-sdk-mdk"></a>卸载 Mono SDK (MDK)

Mono 是 Microsoft .NET Framework 的开放源代码实现，可供所有 Xamarin 产品（Xamarin.iOS、Xamarin.Android 和 Xamarin.Mac）使用，让用户能使用 C# 开发这些平台。

> [!WARNING]
> 除 Visual Studio for Mac 之外，还有其他应用程序使用 Mono，例如 Unity。
> 卸载 Mono 前，请确保 Mono 上没有其他依赖项。

若要从计算机删除 Mono Framework，请在终端运行以下命令：

```bash
sudo rm -rf /Library/Frameworks/Mono.framework
sudo pkgutil --forget com.xamarin.mono-MDK.pkg
sudo rm -rf /etc/paths.d/mono-commands
```

## <a name="uninstall-xamarinandroid"></a>卸载 Xamarin.Android

安装和使用 Xamarin.Android 需要许多必备项，例如 Android SDK 和 Java SDK。

使用以下命令删除 Xamarin.Android：

```bash
sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework
```

### <a name="uninstall-android-sdk-and-java-sdk"></a>卸载 Android SDK 和 Java SDK

开发 Android 应用程序需要 Android SDK。 要完全删除 Android SDK 的所有部分，请在 ~/Library/Developer/Xamarin/ 中找到相关文件，并将其移到回收站   。

> [!WARNING]
> 应注意，Visual Studio for Mac 生成的 Android 签名密钥位于 `~/Library/Developer/Xamarin/Keystore` 中。 请务必适当备份，或避免在要保留密钥存储时删除此目录。

不必卸载 Java SDK (JDK)，因为它已预先打包为 Mac OS X/macOS 一部分。

### <a name="uninstall-android-avd"></a>卸载 Android AVD

> [!WARNING]
> 除 Visual Studio for Mac 之外，还有其他应用程序使用 Android AVD 和这些附加 Android 组件，如 Android Studio。删除此目录可能导致 Android Studio 中的项目中断。

要删除任何 Android AVD 和附加 Android 组件，请使用以下命令：

```bash
rm -rf ~/.android
```

要仅删除 Android AVD，请使用以下命令：

```bash
rm -rf ~/.android/avd
```

## <a name="uninstall-xamarinios"></a>卸载 Xamarin.iOS

Xamarin.iOS 支持使用 C# 或 F# 通过 Visual Studio for Mac 开发 iOS 应用程序。

在终端使用以下命令从文件系统删除所有 Xamarin.iOS 文件：

```bash
rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg
sudo pkgutil --forget com.xamarin.xamarin.ios.pkg
```

## <a name="uninstall-xamarinmac"></a>卸载 Xamarin.Mac

可使用以下两个命令分别彻底删除 Mac 上的产品和许可证，进而从计算机上删除 Xamarin.Mac：

```bash
sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac
```

## <a name="uninstall-workbooks-and-inspector"></a>卸载工作簿和检查器

从 1.2.2 开始，可通过运行以下命令从终端卸载 Xamarin Workbooks 和 Xamarin Inspector：

```bash
sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
```

需要在旧版本手动删除以下项目：

* 在 `"/Applications/Xamarin Workbooks.app"` 删除 Workbooks 应用
* 在 `"Applications/Xamarin Inspector.app"` 删除 Inspector 应用
* 删除加载项：`"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Interactive"` 和 `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Inspector"`
* 在 `/Library/Frameworks/Xamarin.Interactive.framework` 和 `/Library/Frameworks/Xamarin.Inspector.framework` 删除 Inspector 和支持文件

## <a name="uninstall-the-xamarin-profiler"></a>卸载 Xamarin Profiler

```bash
sudo rm -rf "/Applications/Xamarin Profiler.app"
```

## <a name="uninstall-the-visual-studio-installer"></a>卸载 Visual Studio 安装程序

使用以下命令删除 Xamarin 通用安装程序的所有痕迹：

```bash
rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/
rm -rf ~/Library/Preferences/Xamarin/
rm -rf "~/Library/Preferences/Visual Studio/"
```

* * * 





## <a name="uninstall-visual-studio-2019-for-mac-preview"></a>卸载 Visual Studio 2019 for Mac 预览版

Visual Studio 2019 for Mac 预览版作为单独的预览版发布，可用于通过并排安装来继续使用 Visual Studio 2017 for Mac。

现在，Visual Studio 2019 for Mac 已经发布，可以安全地删除 Visual Studio 2019 for Mac 预览版应用程序了。

要卸载预览版应用程序包，请在 Applications 文件夹中选择“Visual Studio (预览版)”，然后单击“移到垃圾桶”，如下图所示    ：

![在查找器中选择“移到垃圾桶”选项](media/uninstall-remove-vspreview.png)

还可以使用以下命令删除预览版 plist 文件：

```bash
rm -rf ~/Library/Preferences/com.microsoft.visual-studio-preview.plist
```

## <a name="see-also"></a>请参阅

- [卸载 Visual Studio (Windows)](/visualstudio/install/uninstall-visual-studio)