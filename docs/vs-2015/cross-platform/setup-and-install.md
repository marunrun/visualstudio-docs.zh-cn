---
title: 设置和安装 | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 2cfcad00-352c-4161-814c-f5ae32d8ada8
caps.latest.revision: 19
ms.author: crdun
manager: crdun
ms.openlocfilehash: 646d8949004f44041fe75d1c6fed2e6f989b92c9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435289"
---
# <a name="setup-and-install"></a>设置和安装
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要使用 Xamarin 从常见的 C#/.NET 代码基础生成本机 iOS、Android 和 Windows 应用，你需要具备以下项目：  
  
- 若要使用 Windows 和 Android 应用：需具备安装了 Visual Studio 2015 和 Xamarin 4 的 Windows 开发计算机（详见下方注释）。 （还可按照 [Xamarin 直接安装](https://developer.xamarin.com/guides/cross-platform/getting_started/requirements/#install) (xamarin.com) 中的说明使用 Visual Studio 2013。）   
  
- 若要使用 iOS 应用：需具备安装了 XCode 和 Xamarin 且采用 OS X Yosemite (10.10.5) 或更高版本的 Mac。  
  
  可同时设置 Windows 和 Mac 计算机，在这些安装程序运行期间，可通过[了解如何使用 Xamarin 进行移动开发](../cross-platform/learn-about-mobile-development-with-xamarin.md)阅读和观看必要的背景材料。  
 
如果在执行此设置和安装后使用 Xamarin 时遇到问题，请在 [ forums.xamarin.com](http://forums.xamarin.com/) 上发布你的问题。
  
> [!NOTE]
> 自 2016 年 3 月 31 日起，所有版本的 Visual Studio 中均随附所有 Xamarin，无需额外费用，且不需要单独的许可证。 Xamarin Studio Community for Mac 向学生、OSS 开发者和小型团队免费提供。 请注意，对于使用早期 Xamarin 许可证配置的 Visual Studio 现有安装，必须将 Xamarin 更新到版本 4.0.3.214 或更高版本。 为此，请转到“工具”>“选项”>“Xamarin”>“其他”，单击“立即检查”链接，然后下载 4.0.3.214 更新。 重启 Visual Studio 时，请转到“工具”>“Xamarin 帐户...”，然后应会看到更新后的状态。  
  
 **在本主题中：**  
  
- [先决条件](#prereq)  
  
- [Windows 设置（Visual Studio 和 Xamarin）](#windows)  
  
- [Mac 设置（Apple ID、Xcode 和 Xamarin）](#mac)  
  
## <a name="prereq"></a> 先决条件  
  
1. 为了面向 Windows 和 Android：  
  
    1. 建议：如果没有 Android 设备，请使用运行 Windows 8 或更高版本的 Windows 物理计算机（非 VM），它允许你使用适用于 Android 且基于 Hyper-V 的快速 Visual Studio 模拟器。 （我们是否提到过你需要物理计算机而不是 VM？）  
  
    1. 可使用带 Windows 7 或更早版本的计算机，此时会将 Xamarin Player 用作 Android 仿真程序。 
    
    1. 无论哪种配置，均直接在连接的物理设备上直接运行应用。  
  
1. 为了面向 iOS：  
  
    1. 使用联网的 Mac 或 Mac mini，其中配有运行 OS X 10.10.5 或更高版本的 OS X Yosemite（Xcode 7.1 所必需）。  
  
    1. 在 Windows (7+) 计算机上使用 Visual Studio 作为主要开发环境时，联网的 Mac 只需要编译和调试 iOS 应用、附加到 iOS 模拟器或受限设备，并使用 Visual Studio 中的情节提要设计器进行用户界面设计。 较早的 Mac 型号完全可满足此辅助角色的需求。  
  
## <a name="windows"></a>Windows 设置（Visual Studio 和 Xamarin）  
  
> [!TIP]
> 这些说明适用于 Visual Studio 2015。 若要在 Visual Studio 2013 中使用 Xamarin（需要 Update 2），请按照 [ Xamarin 直接安装](https://developer.xamarin.com/guides/cross-platform/getting_started/requirements/#install) (xamarin.com) 的说明操作。  
  
1. [下载并启动Visual Studio 2015 任何版本（Community、Professional 或 Enterprise）的安装程序](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 。 Visual Studio 2015 Community 是免费版本；Professional 和Enterprise 版本可免费试用 30 天，30 天后需购买许可证。  
  
   1. 如果已安装 Visual Studio，请打开“控制面板”>“程序和功能”，选择“Visual Studio 2015”项，然后单击“更改”。 安装程序打开时，单击“修改”并跳到下面的步骤 3。  
  
2. （仅限新安装）在安装程序中，选择“自定义”安装：  
  
    ![选择 Visual Studio 安装中的“自定义”选项](../cross-platform/media/cross-plat-xamarin-setup-1.png "Cross-Plat Xamarin Setup 1")  
  
3. 选中以下选框：  
  
   1. “跨平台移动开发”>“C#/.NET (Xamarin)”。 这也将自动选择“常用工具和软件开发工具包”下的各种 Android 工具。 此选项还应更新现有的所有 Xamarin 安装。  
  
        ![选择“跨平台移动开发”下的 Xamarin 选项](../cross-platform/media/cross-plat-xamarin-setup-2.png "Cross-Plat Xamarin Setup 2")  
  
   2. 对于 Windows 8 +:**跨平台移动开发 > Microsoft Visual Studio Emulator for Android**。 注意：如果使用 Windows 7 或更早版本的计算机，或在 Mac 上运行 Windows，请确保*取消勾选*此项。 请参阅步骤 5 后的“Windows 计算机上模拟器的相关备注”。 如果只打算在物理 Android 设备上调试，也可不勾选此项。  
  
   3. （可选）如果计划面向 Windows 设备，还请勾选“Windows 和 Web 开发”>“通用 Windows 应用开发工具”和/或“Windows 8.1 和 Windows Phone 8.0/8.1 工具”。 其中包括安装需要较长下载时间的仿真程序映像的选项；你稍后可以随时返回 Visual Studio 安装程序添加它们。  
  
4. 单击“安装”按钮，让程序运行。 同样，这将需要一些时间才能完成，在此期间可继续查看 Mac 安装说明并浏览[了解如何使用 Xamarin 进行移动开发](../cross-platform/learn-about-mobile-development-with-xamarin.md)。  
  
5. 安装完成后，请启动 Visual Studio 并在系统提示时使用你的 Microsoft 帐户进行登录（此帐户即用于 Windows 的帐户）。 然后通过“工具”>“选项”>“Xamarin”或者“工具”>“选项”>“Xamarin”>“其他”中的“立即检查”链接检查 Xamarin 更新：  
  
    ![在 Visual Studio 选项中检查 Xamarin 更新](../cross-platform/media/cross-plat-xamarin-setup-3.png "Cross-Plat Xamarin Setup 3")  
  
   > [!NOTE]
   > 如前所述，请确保将 Xamarin 更新到版本 4.0.3.214 或更高版本，避免早期 Xamarin 许可证的问题。  

   如果在“工具”>“选项”中没有看到 Xamarin 的选项，请仔细检查安装或尝试重启 Visual Studio。 还可在“选项”对话框中搜索 Xamarin。
      
6. 对于 Windows 7 及更早版本或者在 Mac 上运行 Windows，请使用 [Android SDK 模拟器](https://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debug-on-emulator/android-sdk-emulator/)（若没有物理设备）。 请参见下面的注释。  
  
   **请注意有关在 Windows 上的仿真程序的计算机：** 由于 Cpu 支持一次只有一个虚拟化技术，因此最好在开发计算机上具有仅使用一种。 有 3 种主要的虚拟化技术，分别是：Hyper-V（由适用于 Android 的 Visual Studio 模拟器和 Windows Phone 模拟器使用）、Virtual Box（由 Genymotion 使用）和 Intel HAXM（由 Android SDK 模拟器使用）。 由于 Hyper-V 和 Virtual Box 之间的各种问题，最好在任意给定计算机上仅使用一种模拟器，因此建议在 Windows 8 和更高版本的计算机上使用 Hyper-V，在 Windows 7 和更早版本上以及在 Mac 上运行 Windows 时使用 Intel HAXM 模拟器。  
  
## <a name="mac"></a>Mac 设置（Apple ID、Xcode 和 Xamarin）  
  
1. 如果尚无 Apple ID，请在 [https://appleid.apple.com](https://appleid.apple.com/) 处创建免费 Apple ID。 这是安装和登录 Xcode 所必需的。  
  
2. 从 [https://developer.apple.com/xcode/](https://developer.apple.com/xcode/) 处下载并安装 Xcode，并如[将帐户添加到 XCode](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/AddingYourAccounttoXcode/AddingYourAccounttoXcode.html#//apple_ref/doc/uid/TP40013839-CH40-SW1) (apple.com) 中所述添加你的 Apple ID。  
  
3. 按照 [安装和配置 Xamarin.iOS](http://developer.xamarin.com/guides/ios/getting_started/installation/mac/) (xamarin.com) 上的说明下载和安装 Xamarin。  
  
4. 在 Windows 和 Mac 计算机上安装好 Xamarin 后，请按照[连接到 Mac](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/xamarin-mac-agent/) (xamarin.com) 上的说明操作，以便可通过 Windows 计算机上的 Visual Studio 针对 iOS 和 Mac 进行开发。  
  
     请注意，这两台计算机必须位于同一本地网络。
