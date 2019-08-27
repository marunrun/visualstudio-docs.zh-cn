---
title: 安装适用于跨平台移动开发的 Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2018
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: aaea6b8d-55eb-4427-8185-c050f855c257
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 261d26307a212fa44506b21caadf4b7351453e06
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261097"
---
# <a name="install-cross-platform-mobile-development-with-c"></a>使用 C++ 安装跨平台移动开发

可以在 Visual Studio 中使用 C++ 生成 Windows 桌面应用、通用 Windows 平台 (UWP) 应用、Linux 应用以及现在可生成的适用于 Android 和 iOS 的应用。 使用 C++ 的移动开发工作负载是 Visual Studio 中的一组可安装组件，其中包括跨平台的 iOS、Android 和 UWP Visual Studio 模板。 它安装了所需的跨平台工具和 SDK 以快速启动，而无需自行查找、下载和配置它们。 可以在 Visual Studio 中使用这些工具轻松创建、编辑、调试和测试跨平台项目。 本主题介绍了如何使用 Visual Studio 安装在 C++ 内开发跨平台应用所需的工具和第三方软件。 有关概述，请参阅 [Visual C++ 跨平台移动](https://visualstudio.microsoft.com/vs/features/cplusplus-mdd/)

## <a name="requirements"></a>要求

- 有关安装要求，请参阅 [Visual Studio 产品系列系统要求](/visualstudio/productinfo/vs2017-system-requirements-vs)。

   > [!IMPORTANT]
   > 如果使用的是 Windows 7 或 Windows Server 2008 R2，则可以针对 Windows 桌面应用程序、Android Native Activity 应用和库以及适用于 iOS 的应用和代码库开发代码，但不能针对 Windows Phone 或 UWP 应用开发代码。

若要为特定的设备平台创建应用，还需要满足一些附加要求：

- Windows Phone 仿真程序和适用于 Android 的 Microsoft Visual Studio 仿真程序需要可以运行 Hyper-V 的计算机。 必须先启用 Windows 中的 Hyper-V 功能，然后才能安装和运行仿真程序。 有关详细信息，请参阅仿真程序的[系统要求](system-requirements-for-the-visual-studio-emulator-for-android.md)。

- Android SDK 附带的 x86 Android 仿真程序在可以运行 Intel HAXM 驱动程序的计算机上工作性能最好。 此驱动程序需要具有 VT-x 和执行禁用位支持的 Intel x64 处理器。 有关详细信息，请参阅 [Intel® 硬件加速执行管理器 (Intel® HAXM)](https://go.microsoft.com/fwlink/p/?LinkId=536385)。

- 生成适用于 iOS 的代码，需要 Apple ID、iOS Developer Program 帐户，以及可在 OS X Mavericks（版本 10.9）或更高版本上运行 [Xcode](https://go.microsoft.com/fwlink/p/?LinkId=536387) 版本 6 或更高版本的 Mac 计算机。 有关安装步骤的链接，请参阅[安装适用于 iOS 的工具](#install-tools-for-ios)。

## <a name="get-the-tools"></a>获取工具

在 Visual Studio Community、Visual Studio Professional 和 Visual Studio Enterprise 版本中提供使用 C++ 的移动开发。 要获得 Visual Studio，可转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页进行下载。 从 Visual Studio 2015 开始提供跨平台移动开发工具。

## <a name="install-the-tools"></a>安装工具

适用于 Visual Studio 2017 的 Visual Studio 安装程序包含使用 C++ 的移动开发工作负载，该工作负载可安装 Visual Studio 中进行 Android 和 iOS 开发所需的 C++ 语言工具、模板和组件。 它将安装 Android 生成和调试需要的 GCC 和 Clang 工具集，以及与用于 iOS 开发的 Mac 进行通信的组件。 它还会安装所有第三方工具和支持 iOS 和 Android 应用开发所需的软件开发工具包。 这些大部分第三方工具都是 Android 平台支持所需的开放源代码软件。

- 构建面向 Android 平台的 C++ 代码需要 Android 本机开发工具包 (NDK)。

- Android 生成过程需要 Android SDK、Apache Ant 和 Java SE 开发工具包。

- Google Android 模拟器和 Intel 硬件加速执行管理器是可选组件，但推荐使用。 可以直接在 Android 设备上开发和调试，但在桌面上使用模拟器进行调试通常更为容易。 Microsoft 还提供一个可单独安装的适用于 Android 的 Visual Studio 模拟器。

### <a name="install-the-mobile-development-with-c-workload"></a>安装使用 C++ 的移动开发工作负载

1. 从“开始”菜单运行“Visual Studio 安装程序”。

1. 如果已经安装了 Visual Studio，则可以为想要修改的已安装 Visual Studio 版本选择“修改”按钮。 否则，请选择“安装”以安装 Visual Studio。

1. 选中“工作负载”选项卡后，向下滚动并在 Visual Studio 安装程序中选择“使用 C++ 的移动开发”工作负载。 选中此工作负载后，也会选中 C++ 开发所需的其他组件。 还可以选择其他工作负载和单个组件同时进行安装。 要生成同时面向 UWP 的跨平台代码，请选择“通用 Windows 平台开发”工作负载。

1. 在“安装详细信息”窗格中，展开“使用 C++ 的移动开发”。 在“可选”部分，你可以选择其他版本的 NDK、Google Android 模拟器、Intel 硬件加速执行管理器以及 IncrediBuild 生成加速工具。

1. 默认情况下，工作负载包含一个或多个 Android SDK 安装程序组件。 提供 Android SDK 的其他版本。 要安装其中一个版本，请选择“单个组件”选项卡，然后向下滚动到“SDK、库和框架”部分进行选择。

1. 选择“修改”或“安装”按钮以安装“使用 C++ 的移动开发”工作负载以及选择的其他工作负载和可选组件。

   安装完成后，关闭该安装程序，然后重启计算机。 第三方组件的某些设置操作在计算机重启后才生效。

   > [!IMPORTANT]
   > 你必须重新启动以确保所有软件都得到了正确安装。

1. 打开 Visual Studio。

> [!NOTE]
> 如果使用的是 Visual Studio 2015，请参阅[安装适用于跨平台移动开发的 Visual C++ (Visual Studio 2015)](install-visual-cpp-for-cross-platform-mobile-development.md?view=vs-2015)

## <a name="install-tools-for-ios"></a>Install tools for iOS

可以使用适用于跨平台移动开发的 Visual C++ 来编辑、调试 iOS 代码，并将其部署到 iOS 仿真程序或 iOS 设备，但由于许可限制，该代码必须在 Mac 上远程生成。 若要使用 Visual Studio 生成和运行 iOS 应用，必须在 Mac 上安装并配置远程代理。 有关安装说明、先决条件和配置选项的详细信息，请参阅[安装并配置使用 iOS 进行构建的工具](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。 如果你不是针对 iOS 构建，则可以跳过此步骤。

## <a name="install-or-update-dependencies-manually"></a>手动安装或更新依赖项

安装“使用 C++ 的移动开发”工作负载（或安装 Visual Studio 2015 中的“Visual C++ 移动开发”选项）时，如果你决定不使用 Visual Studio 安装程序安装一个或多个第三方依赖项，则可以通过使用[“安装工具”](#install-the-tools)中的步骤稍后安装它们。 Visual Studio 安装程序会定期更新以安装最新的第三方组件。 可以使用它来安装更新的 SDK 和 NDK。 你还可以独立于 Visual Studio 安装或更新它们。

> [!CAUTION]
> 你可以按照任何顺序安装依赖项（不包括 Java）。 必须先安装并配置 JDK 才能安装 Android SDK。

阅读以下信息并使用这些链接来手动安装依赖项。

- [Java SE 开发工具包](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

   默认情况下，安装程序将 Java 工具放置在以下路径：C:\Program Files (x86)\Java。

- [Android SDK](https://developer.android.com/sdk/index.html#command-tools)

   在安装过程中按照推荐更新 API。 确保至少安装了 SDK for Android 5.0 Lollipop（API 级别 21）。 默认情况下，安装程序将 Android SDK 放置在以下路径 C:\Program Files (x86)\Android\android-sdk。

   可再次运行 Android SDK 目录中的 SDK 管理器应用，以更新 SDK 并安装可选工具和其他 API 级别。 除非你使用“以管理员身份运行”  运行 SDK Manager 应用，否则安装更新可能会失败。 如果构建 Android 应用存在问题，请检查已安装的 SDK 的 SDK Manager 更新。

   若要使用 Android SDK 附带的某些 Android 仿真程序，则必须安装可选的 Intel HAXM 驱动程序。 可能需要从 Windows 中删除 HYPER-V 功能才能成功安装 Intel HAXM 驱动程序。 必须还原 HYPER-V 功能，以使用 Android 的 Windows Phone 仿真程序和 Microsoft Visual Studio Emulator for Android。 有关详细信息，请参阅 [Android 模拟器硬件加速](https://docs.microsoft.com/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin)。

- [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html)

   默认情况下，安装程序将 Android NDK 放置在以下路径：C:\ProgramData\Microsoft\AndroidNDK。 你可再次下载和安装 Android NDK，以更新 NDK 安装。

- [Apache Ant](https://ant.apache.org/bindownload.cgi)

   默认情况下，安装程序将 Apache Ant 放置在以下路径：C:\Program Files (x86)\Microsoft Visual Studio 14.0\Apps。

- [适用于 Android 的 Microsoft Visual Studio 仿真程序](https://aka.ms/vscomemudownload)

   适用于 Android 的 Microsoft Visual Studio 模拟器是用于测试和调试代码的可选模拟器。 发布适用于 Android 的 Visual Studio 模拟器后，Google 更新了其 Android 模拟器，以通过 Intel 的 HAXM 使用硬件加速。 建议尽可能使用 Google 加速模拟器，因为它可以访问最新的 Android OS 映像和 Google Play 服务。

在大多数情况下，Visual Studio 可以检测到已安装的第三方软件的配置，并维护内部环境变量中的安装路径。 可以覆盖 Visual Studio IDE 中的这些跨平台开发工具的默认路径。

#### <a name="to-set-the-paths-for-third-party-tools"></a>若要设置第三方工具的路径

1. 在 Visual Studio 菜单栏上依次选择“工具” > “选项”。

1. 在“选项”对话框中，选择“跨平台” > “C++” > “Android”。

   ![Android 工具路径选项](../cross-platform/media/cppmdd_options_android.PNG "CPPMDD_Options_Android")

1. 若要更改工具使用的路径，请选中该路径旁的复选框，并在文本框中编辑文件夹路径。 还可以使用浏览按钮 (**...**) 打开“选择位置”  对话框以选择文件夹。

1. 选择“确定”  以保存自定义工具文件夹位置。

## <a name="see-also"></a>请参阅

- [安装并配置使用 iOS 进行构建的工具](install-and-configure-tools-to-build-using-ios.md)
- [Visual C++ 跨平台移动](https://go.microsoft.com/fwlink/p/?LinkId=536383)
