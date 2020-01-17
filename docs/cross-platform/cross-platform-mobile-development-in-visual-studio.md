---
title: Visual Studio 中的跨平台移动开发 | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 8202717a-e990-45cf-b092-438651ccb38a
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- multiple
ms.openlocfilehash: 15c4d31c8cc835884f1093dc78083bbfa9448bc3
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916877"
---
# <a name="cross-platform-mobile-development-in-visual-studio"></a>Visual Studio 中的跨平台移动开发

可使用 Visual Studio 生成适用于 Android、iOS 和 Windows 设备的应用。  设计应用时，可使用 Visual Studio 中的工具轻松添加连接的服务（如 Office 365、Azure App Service 和 Application Insights）。

使用 C# 和 .NET Framework、HTML 和 JavaScript 或者 C++ 生成应用。 还可共享代码、字符串和图像，某些情况下甚至可共享用户界面。

如果想要构建一款游戏或沉浸式图形应用，请安装 Visual Studio tools for Unity，借助 Unity 尽享 Visual Studio 中所有强大的生产力功能。Unity 是一款热门的跨平台游戏/图形引擎和开发环境，主要针对在 iOS、Android、Windows 和其他平台上运行的应用。

## <a name="build-an-app-for-android-ios-and-windows-net-framework"></a>构建面向 Android、iOS 和 Windows 的应用 (.NET Framework)

![设备](../cross-platform/media/homedevices.png "HomeDevices")

借助 Visual Studio Tools for Xamarin，可在同一解决方案中面向 Android、iOS 和 Windows，进而共享代码甚至 UI。

|**了解更多信息**|
|--------------------|
|[安装 Visual Studio](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[了解 Visual Studio 中的 Xamarin](https://visualstudio.microsoft.com/xamarin/) (VisualStudio.com)|
|[Xamarin 移动应用开发文档](/xamarin/) |
|[适用于 Xamarin 应用的 DevOps](/xamarin/tools/ci/devops/) |
|[了解 Visual Studio 中的通用 Windows 应用](https://visualstudio.microsoft.com/vs/universal-windows-platform/) (VisualStudio.com)|
|[了解 Swift 与 C# 之间的相似之处](https://aka.ms/scposter) (download.microsoft.com)|

### <a name="AndroidHTML"></a>通过单个基本代码面向 Android、iOS 和 Windows

 可使用 C# 或 F# 生成面向 Android、iOS 和 Windows 的本机应用（目前不支持 Visual Basic）。  首先，请安装 Visual Studio，在安装程序中选择“使用 .NET 的移动开发”选项  。

 如果已安装 Visual Studio，请重新运行 Visual Studio 安装程序并为 Xamarin 选择相同的“使用 .NET 的移动开发”选项（如上所示）   。

 完成后，“新建项目”  对话框中将显示项目模板。 最简单的 Xamarin 模板查找方法是针对“Xamarin”进行搜索。

 Xamarin 将 Android、iOS 和 Windows 的本机功能公开为 .NET 类和方法。 这意味着，你的应用可不受限制地访问本机 API 和本机用户控件，它们的响应速度可媲美使用本机平台语言编写的应用。

 创建项目之后，可以利用 Visual Studio 的所有工作效率功能。 例如，可使用设计器创建页面，使用 IntelliSense 了解移动平台的本机 API。 准备好运行应用并看到其外观时，可以使用 Android SDK 仿真程序并本机运行 Windows 应用。 还可直接使用受限的 Android 和 Windows 设备。 对于 iOS 项目，请连接到联网的 Mac 并从 Visual Studio 中启动 iOS 仿真程序，或者连接到受限设备。

#### <a name="design-one-set-of-pages-that-render-across-all-devices-by-using-xamarinforms"></a>使用 Xamarin.Forms 设计一组在所有设备中呈现的页面

 根据应用设计的复杂性，可以考虑使用项目模板“移动应用”  组中的 **Xamarin.Forms** 模板生成应用。 Xamarin.Forms 是一个 UI 工具包，可用于创建在 Android、iOS 和 Windows 之间共享的单一界面。  编译 Xamarin.Forms 解决方案时，会分别获得一个 Android 应用、iOS 应用和 Windows 应用。 有关更多详细信息，请参阅[了解关于使用 Xamarin 进行移动开发的信息](/xamarin/cross-platform/get-started/introduction-to-mobile-development/)和 [Xamarin.Forms 文档](/xamarin/xamarin-forms/)。

#### <a name="ShareHTML"></a> 在 Android、iOS 和 Windows 应用间共享代码

 如果不使用 Xamarin.Forms 并选择为每个平台单独设计，可在平台项目（Android、iOS 和 Windows）之间共享大多数的非 UI 代码。 这包括所有的业务逻辑、云集成、数据库访问和其他所有面向 .NET 框架的代码。 唯一不能共享的代码是面向特定平台的代码。

 ![在 Windows、iOS 和 Android UI 之间分享代码](../cross-platform/media/sharecode.png "ShareCode")

 你可以通过使用共享项目、可移植类库项目或同时使用这两种项目来共享你的代码。 你可能会发现有些代码最适合在共享项目中使用，而有些代码在可移植类库项目中使用会发挥更好的效果。

|**了解更多信息**|
|--------------------|
|[共享代码选项](/xamarin/cross-platform/app-fundamentals/code-sharing/) (Xamarin) |
|[.NET 的代码共享选项](/dotnet/standard/cross-platform/) |

### <a name="WindowsHTML"></a>面向 Windows 10 设备

 ![Windows 设备](../cross-platform/media/windowsdevices.png "Windows 设备")

 若想创建面向全部 Windows 10 设备的单个应用，请创建通用 Windows 应用。 将使用单个项目来设计应用，并且无论使用何种设备进行查看，页面都将正确呈现。

 使用通用 Windows 平台 (UWP) 应用项目模板开始设计。 直观地设计页面，然后在预览窗口中将其打开以查看页面在各种类型设备中的显示方式。 如果不喜欢某设备上的页面显示方式，可优化页面以更好地适应屏幕尺寸、分辨率或不同的方向（如横向模式或纵向模式）。 可使用 Visual Studio 中直观的工具窗口和易访问的菜单选项来执行所有这些操作。 如果已准备好运行应用和逐行执行代码，可在“标准”  工作栏的一个下拉列表中找到所有设备仿真程序和不同类型设备的模拟器。

|**了解更多信息**|
|--------------------|
|[通用 Windows 平台简介](/windows/uwp/get-started/universal-application-platform-guide)|
|[创建第一个应用](/windows/uwp/get-started/your-first-app)|
|[开发通用 Windows 平台 (UWP) 的应用](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md)|
|[将应用迁移到通用 Windows 平台 (UWP)](https://msdn.microsoft.com/library/mt148501.aspx)|

::: moniker range="vs-2017"

## <a name="HTML"></a>构建面向 Android、iOS 和 Windows 的应用 (HTML/JavaScript)

 ![Windows、iOS 和 Android 设备](../cross-platform/media/homedevices.png "Windows、iOS 和 Android 设备")

 如果你是一名 Web 开发者且熟悉 HTML 和 JavaScript，则可通过使用适用于 Apache Cordova 的 Visual Studio 工具来面向 Windows、Android 和 iOS。 这些应用可以针对全部三个平台，还可以使用你最熟悉的技能和进程来生成。

 Apache Cordova 是一种包含插件模型的框架。 该插件模型提供了一个 JavaScript API，可用于访问全部 3 个平台（Android、iOS 和 Windows）的本机设备功能。

 由于这些 API 是跨平台的，因此你可以在三个平台之间共享所编写的大部分内容。 这样可以减少开发和维护成本。 此外，无需从头开始。 如果已创建了其他类型的 Web 应用程序，则可以与 Cordova 应用共享这些文件，而无需以任何方式修改或重新设计。

 ![使用 JavaScript 的多设备混合应用](../cross-platform/media/multidevicehybridapps.png "使用 JavaScript 的多设备混合应用")

 首先，请安装 Visual Studio，并在安装过程中选择“使用 Javascript 的移动开发”功能  。 Cordova 工具都会自动安装构建多平台应用所需的所有第三方软件。

 安装扩展后，打开 Visual Studio 并创建空白应用 (Apache Cordova)  项目。 然后，便可使用 JavaScript 或 TypeScript 来开发应用了。 也可以添加插件来扩展应用的功能，编写代码时插件的 API 会出现在 IntelliSense 中。

 如果已准备好运行应用并逐行执行代码，请选择一个仿真程序（如 Apache Ripple 仿真程序或 Android Emulator）或者一个已直接连接到计算机的设备。 然后，启动应用。 如果是在 Windows PC 上开发应用，则甚至可在其中运行。 所有这些选项都作为 Visual Studio Tools for Apache Cordova 的一部分内置在 Visual Studio 中。

 Visual Studio 中仍可使用用于创建通用 Windows 平台 (UWP) 应用的项目模板，因此，如果打算创建仅面向 Windows 设备的应用，则可以放心使用这些模板。 如果决定稍后面向 Android 和 iOS，可始终将代码移植到 Cordova 项目中。

|**了解更多信息**|
|--------------------|
|[安装 Visual Studio](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[用于 Apache Cordova 的 Visual Studio Tools 入门](/visualstudio/cross-platform/tools-for-cordova/)|
|[了解适用于 Android 的 Visual Studio 仿真程序](https://visualstudio.microsoft.com/vs/msft-android-emulator/) (VisualStudio.com)|

::: moniker-end

<a name="CPP"></a>

## <a name="build-an-app-for-android-ios-and-windows-c"></a>生成面向 Android、iOS 和 Windows 的应用 (C++)

![使用 C&#43;&#43; 生成面向 Android、 iOS 和 Windows 的应用](../cross-platform/media/cross_plat_cpp_intro_image.png "Cross_Plat_CPP_Intro_Image")

 首选，安装 Visual Studio 和“使用 C++ 的移动开发”工作负载  。 随后即可生成面向 Android 的本机活动应用程序或面向 Windows 或 iOS 的应用。 必要时可在同一解决方案中面向 Android、iOS 和 Windows，然后使用跨平台静态（或动态）共享库在它们之间共享代码。

 如果需要针对 Android 构建要求任意类型的高级图形操作（如游戏）的应用，可使用 C++ 实现此目的。 从本机活动应用程序 (Android) 项目开始  。 此项目完全支持 Clang 工具链。

 ![本机活动项目模板](../cross-platform/media/cross-plat_cpp_native.png "本机活动项目模板")

 准备好运行应用并看到其外观时，请使用 Android Emulator。 它快速、可靠且易于安装和配置。

 也可以使用 C++ 和通用 Windows 平台 (UWP) 应用项目模板，生成定目标到全部 Windows 10 设备的应用。 有关此操作的详细信息，请参阅本主题中的上述[面向 Windows 10 设备](#WindowsHTML)部分。

 可创建静态（或动态）共享库，在 Android、iOS 和 Windows 间共享 C++ 代码。

 ![静态和动态共享库](../cross-platform/media/cross_plat_cpp_libraries.png "静态和动态共享库")

 可以在 Windows、iOS 或 Android 项目中使用该库（如本节前面部分中所述的库一样）。 还可以在使用 Xamarin、Java 或任何允许在非托管 DLL 中调用函数的语言生成的应用中使用它。

 在这些库中编写代码时，可以使用 IntelliSense 探索 Android 和 Windows 平台的本机 API。 这些库项目与 Visual Studio 调试器完全集成，因此可以使用调试器的所有高级功能设置断点、逐句执行代码以及查找和修复问题。

|**了解更多信息**|
|--------------------|
|[下载 Visual Studio](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[使用 C++ 安装跨平台移动开发](install-visual-cpp-for-cross-platform-mobile-development.md)|
|[了解面向多个平台使用 C++ 的更多信息](https://visualstudio.microsoft.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[安装所需内容，然后针对 Android 创建本机活动应用程序](create-an-android-native-activity-app.md)|
|[了解关于与 Android 和 Windows 应用程序共享 C++ 代码的更多信息](https://visualstudio.microsoft.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[使用 C++ 的跨平台移动开发示例](cross-platform-mobile-development-examples.md)|

<a name="Unity"></a>

## <a name="build-a-cross-platform-game-for-android-ios-and-windows-by-using-visual-studio-tools-for-unity"></a>使用 Visual Studio Tools for Unity 构建面向 Android、iOS 和 Windows 的跨平台游戏

 适用于 Unity 的 Visual Studio 工具是一款免费的 Visual Studio 扩展，用于将 Visual Studio 强大的代码编辑工具、生产力工具和调试工具与 Unity  进行集成。Unity 是一款热门的跨平台游戏/图形引擎和开发环境，针对面向 Windows、iOS、Android 和其他平台（如 Web）的沉浸式应用。

 ![VSTU 开发环境](../cross-platform/media/vstu_overview.png "Visual Studio Tools for Unity 概述")

 借助 Visual Studio Tools Unity (VSTU)，可以使用 Visual Studio 在 C# 中编写游戏和编辑器脚本，随后使用其功能强大的调试器查找和修复错误。 VSTU 的最新版本支持 Unity 2018.1 并且包括以下功能：语法着色 Unity 的 ShaderLab 着色器语言、与 Unity 更好地同步、更丰富地调试、提升了针对 MonoBehavior 向导的代码生成。 VSTU 还提供 Unity 项目文件、控制台消息以及在 Visual studio 中启动游戏的功能，从而使你可以在编写代码时花费更少的时间与 Unity 编辑器进行切换。

|**了解更多信息**|
|--------------------|
|[了解有关使用 Visual Studio 构建 Unity 游戏的更多信息](https://visualstudio.microsoft.com/vs/features/game-development/#tab-4b0d0be8de5f65564ad)|
|[阅读有关 Visual Studio Tools for Unity 的详细信息](../cross-platform/visual-studio-tools-for-unity.md) |
|[开始使用 Visual Studio Tools for Unity](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md) |
|[了解关于 Visual Studio Tools for Unity 2.0 预览版的最新增强功能](https://devblogs.microsoft.com/visualstudio/visual-studio-tools-for-unity-2-0-preview/) （Visual Studio 博客）|
|[观看 Visual Studio Tools for Unity 2.0 预览版的简介视频](https://www.bing.com/videos/search?q=visual+studio+tools+for+unity&qs=n&form=QBVLPG&pq=visual+studio+tools+for+unity&sc=6-29&sp=-1&sk=#view=detail&mid=0A13177F0BC7463A24080A13177F0BC7463A2408) （视频）|
|[了解 Unity](https://unity.com/) （Unity 网站）|

## <a name="see-also"></a>请参阅

- [向 Visual Studio 项目添加 Office 365 API](/office/developer-program/office-365-developer-program)
- [Azure App Service - 移动应用](https://azure.microsoft.com/services/app-service/mobile/)
- [Visual Studio App Center](/appcenter)
