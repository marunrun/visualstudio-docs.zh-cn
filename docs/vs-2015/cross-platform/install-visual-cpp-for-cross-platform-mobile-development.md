---
title: 安装适用于跨平台移动开发的 Visual C++ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: aaea6b8d-55eb-4427-8185-c050f855c257
caps.latest.revision: 17
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 8046b261021a1147dbf0356c6854968b3d23a1df
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299804"
---
# <a name="install-visual-c-for-cross-platform-mobile-development"></a>Install Visual C++ for Cross-Platform Mobile Development
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于跨平台移动开发的 Visual C++(https://go.microsoft.com/fwlink/p/?LinkId=536383) 是 Visual Studio 2015 的可安装组件。 它包括跨平台 Visual Studio 模板，并安装了跨平台工具和 SDK 以快速启动，而无需自行查找、下载和配置它们。 你可以在 Visual Studio 中使用这些工具轻松创建、编辑、调试和测试跨平台项目。 本主题介绍了如何安装使用 Visual Studio 开发跨平台应用所需的工具和第三方软件。 有关组件的概述，请参阅 [Visual C++ 跨平台移动](https://go.microsoft.com/fwlink/p/?LinkId=536387)  
  
 [要求](#Requirements)   
 [获取工具](#GetTheTools)   
 [安装工具](#InstallTheTools)   
 [Install tools for iOS](#InstallForiOS)   
 [手动安装或更新依赖项](#ThirdParty)  
  
## <a name="Requirements"></a>要求  
  
- 有关安装要求，请参阅 [Visual Studio 2015 系统要求](https://www.visualstudio.com/visual-studio-2015-system-requirements-vs)。  
  
  > [!IMPORTANT]
  > 如果使用的是 Windows 7 或 Windows Server 2008 R2，则可以针对经典 Windows 应用程序、Android Native Activity 应用和库以及适用于 iOS 的应用和代码库开发代码，但不能针对 Windows 应用商店应用或通用 Windows 应用开发代码。  
  
  若要为特定的设备平台创建应用，还需要满足一些附加要求：  
  
- Windows Phone 仿真程序和适用于 Android 的 Microsoft Visual Studio 仿真程序需要可以运行 Hyper-V 的计算机。 必须先启用 Windows 中的 Hyper-V 功能，然后才能安装和运行仿真程序。 有关详细信息，请参阅仿真程序的 [系统要求](https://msdn.microsoft.com/4d5bb438-231a-4cd2-84b7-e9660b0e3baf)。  
  
- Android SDK 附带的 x86 Android 仿真程序在可以运行 Intel HAXM 驱动程序的计算机上工作性能最好。 此驱动程序需要具有 VT-x 和执行禁用位支持的 Intel x64 处理器。 有关详细信息，请参阅 [Intel® 硬件加速执行管理器安装说明 - Microsoft Windows](https://go.microsoft.com/fwlink/p/?LinkId=536385)。  
  
- 若要构建适用于 iOS 的代码，需要 Apple ID、iOS Developer Program 帐户，以及可在 OS X Mavericks 或更高版本上运行 [Xcode 6](https://go.microsoft.com/fwlink/p/?LinkId=536387) 或更高版本的 Mac 计算机。 有关简单的安装步骤，请参阅 [Install tools for iOS](#InstallForiOS)。  
  
## <a name="GetTheTools"></a> 获取工具  
 适用于跨平台移动开发的 Visual C++ 是 Visual Studio Community、Professional 和 Enterprise 版所随附的可安装组件。 若要获取 Visual Studio，请转到 [Visual Studio 2015 下载](https://go.microsoft.com/fwlink/p/?linkid=517106)页面，并下载 Visual Studio 2015 Update 2 或更高版本。  
  
## <a name="InstallTheTools"></a> 安装工具  
 Visual Studio 2015 的安装程序包括安装用于跨平台移动开发的 Visual C++ 的选项。 这将安装 Visual Studio 所需的 C++ 语言工具、模板和组件，Android 生成和调试所需的 GCC 和 Clang 工具集，以及与用于 iOS 开发的 Mac 进行通信的组件。 它还会安装所有第三方工具和支持 iOS 和 Android 应用开发所需的软件开发工具包。 这些大部分第三方工具都是 Android 平台支持所需的开放源代码软件。  
  
- 构建面向 Android 平台的 C++ 代码需要 Android 本机开发工具包 (NDK)。  
  
- Android 生成过程需要 Android SDK、Apache Ant 和 Java SE 开发工具包。  
  
- 适用于 Android 的 Microsoft Visual Studio 仿真程序是用于测试和调试你的代码的可选高性能仿真程序。  
  
#### <a name="to-install-visual-c-for-cross-platform-mobile-development-and-the-third-party-tools"></a>要安装用于跨平台移动开发的 Visual C++ 和第三方工具  
  
1. 运行跟随 [获取工具](#GetTheTools)中的链接下载的 Visual Studio 2015 安装程序。 若要安装可选组件，请选择“自定义” 作为安装类型。 选择“下一步” 以选择要安装的可选组件。  
  
2. 在“选择功能”中，展开“跨平台移动开发” ，然后勾选“Visual C++ 移动开发”。  
  
     ![选择 Visual C&#43; &#43; Mobile 开发](../cross-platform/media/cppmdd-install-vcmdd.png "CPPMDD_Install_VCMDD")  
  
     默认情况下，在选择“Visual C++ 移动开发”时，“编程语言”选项将设置为安装 **Visual C++** ，且“常用的工具和软件开发工具包”选项将设置为安装所需的第三方组件。 必要时可选择其他组件。 **适用于 Android 的 Microsoft Visual Studio 模拟器**也默认处于选中状态。 已安装的组件在列表中显示为非活动状态。  
  
     若要在它们与 Android 和 iOS项目之间构建通用 Windows 应用并共享代码，请在“选择功能”中展开“Windows 和 Web 开发”，然后勾选“通用 Windows 应用开发工具”。 如果不打算构建通用 Windows 应用，则以跳过此选项。  
  
     选择“下一步” 继续。  
  
3. 第三方组件都具有其自己的许可条款。 可以通过选择各个组件旁边的“许可条款” 链接查看许可条款。 选择“安装”，以添加组件并安装 Visual Studio 和适用于跨平台移动开发的 Visual C++。  
  
4. 安装完成后，关闭该安装程序，然后重启计算机。 第三方组件的某些设置操作在计算机重启后才生效。  
  
    > [!IMPORTANT]
    > 你必须重新启动以确保所有软件都得到了正确安装。  
  
     如果未能安装适用于 Android 组件的 Microsoft Visual Studio 模拟器，表示你的计算机可能未启用 Hyper-V。 使用“打开或关闭 Windows 功能”控制面板应用来启用 Hyper-V，然后重新运行 Visual Studio 安装程序。  
  
    > [!NOTE]
    > 如果你的计算机或 Windows 版本不支持 Hyper-V，则不能使用适用于 Android 组件的 Microsoft Visual Studio 模拟器。 Windows 家庭版不包括 Hyper-V 支持。  
  
5. 打开 Visual Studio。 如果这是你第一次运行 Visual Studio，则可能需要一些时间来配置和登录。 Visual Studio 准备就绪后，在“工具” 菜单上选择“扩展和更新”、“更新”。 如果有用于跨平台移动开发的 Visual C++ 或适用于 Android 的 Microsoft Visual Studio 仿真程序的 Visual Studio 可用更新，则安装它们。  
  
## <a name="InstallForiOS"></a> Install tools for iOS  
 可以使用用于跨平台移动开发的 Visual C++ 来编辑、调试 iOS 代码，并将其部署到 iOS 仿真程序或 iOS 设备，但由于许可限制，该代码必须在 Mac 上远程生成。 若要使用 Visual Studio 生成和运行 iOS 应用，必须在 Mac 上安装并配置远程代理。 有关详细的安装说明、先决条件和配置选项信息，请参阅 [Install And Configure Tools to Build using iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。 如果你不是针对 iOS 构建，则可以跳过此步骤。  
  
## <a name="ThirdParty"></a> 手动安装或更新依赖项  
 如果在安装 Visual C++ 移动开发选项时，你决定不使用 Visual Studio 安装程序安装一个或多个第三方依赖项，则可以通过使用 [Install the tools](#InstallTheTools)中的步骤稍后安装它们。 你还可以独立于 Visual Studio 安装或更新它们。  
  
> [!CAUTION]
> 你可以按照任何顺序安装依赖项（不包括 Java）。 必须先安装并配置 JDK 才能安装 Android SDK。  
  
 阅读以下信息并使用这些链接来手动安装依赖项。  
  
- [Java SE 开发工具包](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  
  
   默认情况下，安装程序将 Java 工具放置在以下路径：C:\Program Files (x86)\Java。  
  
- [Android SDK](https://developer.android.com/sdk/index.html#Other)  
  
   在安装过程中按照推荐更新 API。 确保至少安装了 SDK for Android 5.0 Lollipop（API 级别 21）。 默认情况下，安装程序将 Android SDK 放置在以下路径 C:\Program Files (x86)\Android\android-sdk。  
  
   可再次运行 Android SDK 目录中的 SDK 管理器应用，以更新 SDK 并安装可选工具和其他 API 级别。 除非你使用“以管理员身份运行” 运行 SDK Manager 应用，否则安装更新可能会失败。 如果构建 Android 应用存在问题，请检查已安装的 SDK 的 SDK Manager 更新。  
  
   若要使用 Android SDK 附带的某些 Android 仿真程序，则必须安装可选的 Intel HAXM 驱动程序。 可能需要从 Windows 中删除 HYPER-V 功能才能成功安装 Intel HAXM 驱动程序。 必须还原 HYPER-V 功能，以使用 Android 的 Windows Phone 仿真程序和 Microsoft Visual Studio Emulator for Android。  
  
- [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html)  
  
   默认情况下，安装程序将 Android NDK 放置在以下路径：C:\ProgramData\Microsoft\AndroidNDK。 你可再次下载和安装 Android NDK，以更新 NDK 安装。  
  
- [Apache Ant](http://ant.apache.org/bindownload.cgi)  
  
   安装程序将 Apache Ant 默认置于以下路径： C:\Program Files (x86)\Microsoft Visual Studio 14.0\Apps。  
  
- [适用于 Android 的 Microsoft Visual Studio 仿真程序](https://visualstudio.microsoft.com/vs/msft-android-emulator/)  
  
   可以从 Visual Studio 库安装和更新适用于 Android 的 Microsoft Visual Studio 仿真程序。  
  
  在大多数情况下，Visual Studio 可以检测到已安装的第三方软件的配置，并维护内部环境变量中的安装路径。 可以覆盖 Visual Studio IDE 中的这些跨平台开发工具的默认路径。  
  
#### <a name="to-set-the-paths-for-third-party-tools"></a>若要设置第三方工具的路径  
  
1. 在 Visual Studio 菜单栏上依次选择“工具”、“选项”。  
  
2. 在“选项” 对话框框中，展开”跨平台”、“C++”，然后选择“Android”。  
  
     ![Android 工具路径选项](../cross-platform/media/cppmdd-options-android.PNG "CPPMDD_Options_Android")  
  
3. 若要更改工具使用的路径，请选中该路径旁的复选框，并在文本框中编辑文件夹路径。 还可以使用浏览按钮 ( **...** ) 打开“选择位置” 对话框以选择文件夹。  
  
4. 选择“确定” 以保存自定义工具文件夹位置。  
  
## <a name="see-also"></a>请参阅  
 [Install And Configure Tools to Build using iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md)   
 [Visual C++ 跨平台移动](https://www.visualstudio.com/explore/cplusplus-mdd-vs.aspx)
