---
title: 在 Android 和 iOS 上生成 OpenGL ES 应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 76a67886-df57-4a81-accb-2e3c2eaf607b
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: b235576f21b63a7be4170f36abf58bed9fab9df3
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923852"
---
# <a name="build-an-opengl-es-application-on-android-and-ios"></a>在 Android 和 iOS 上生成 OpenGL ES 应用程序

可以为共享通用代码的 iOS 应用和 Android 应用创建 Visual Studio 解决方案和项目。 本文将指导你完成有关创建简单 iOS 应用和 Android 本机活动应用的解决方案模板。 应用具有共同的 C++ 代码，该代码使用 OpenGL ES 在每个平台上显示相同的动画旋转多维数据集。 OpenGL ES（OpenGL for Embedded Systems 或 GLES）是多种移动设备支持的 2D 和 3D 图形 API。

## <a name="requirements"></a>要求

在可以创建用于 iOS 和 Android 的 OpenGL ES 应用之前，确保你已满足所有系统要求。 如果尚未满足要求，请在 Visual Studio 安装程序中安装使用 C++ 的移动开发工作负载。 若要针对 iOS 进行生成，请包括可选的 C++ iOS 开发工具。 若要针对 Android 进行生成，请安装 C++ Android 开发工具和所需的第三方工具：Android NDK、Apache Ant、Google Android 仿真器和 Intel 硬件加速执行管理器。 接下来，配置 Intel HAXM 和 Android 仿真器以在系统上运行。 有关详细信息和详细说明，请参阅[安装用于跨平台移动开发的 Visual C++](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)。 若要生成和测试 iOS 应用，将需要一台 Mac 计算机，并根据安装说明进行设置安装。 有关如何为 iOS 开发进行设置的详细信息，请参阅[安装并配置使用 iOS 进行生成的工具](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。

## <a name="create-a-new-opengles-application-project"></a>创建新的 OpenGLES 应用程序项目

在本教程中，你首先创建一个新的 OpenGL ES 应用程序项目，然后在适用于 Android 的 Visual Studio 仿真程序中生成并运行默认应用。 接下来生成适用于 iOS 的应用并在 iOS 设备上运行该应用。

1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”    。

1. 在  “新建项目”对话框中，在  “模板”下，选择“Visual C++”   >   “跨平台”，然后选择“OpenGLES 应用程序(Android、iOS)”  模板。

1. 为应用命名（例如 `MyOpenGLESApp`），然后选择 **确认**。

   ![新的 OpenGLES 应用程序项目](../cross-platform/media/cppmdd_opengles_newproj.PNG "CPPMDD_OpenGLES_NewProj")

   Visual Studio 创建新的解决方案并打开解决方案资源管理器。

   ![解决方案资源管理器中的 MyOpenGLESApp](../cross-platform/media/cppmdd_opengles_solexpl.PNG "CPPMDD_OpenGLES_SolExpl")

   新的 OpenGL ES 应用程序解决方案包括三个库项目和两个应用程序项目。 库文件夹包含一个共享代码项目和两个引用共享代码的特定于平台的项目：

- `MyOpenGLESApp.Android.NativeActivity` 包含引用和粘附代码，可将应用作为本机活动在 Android 上实现。 粘附代码入口点在 main.cpp 中实现，它包括 `MyOpenGLESApp.Shared` 中的公共共享代码。  预编译头位于 pch.h。  此本机活动应用项目编译为一个由 `MyOpenGLESApp.Android.Packaging` 项目选取的共享库 (.so) 文件。 

- `MyOpenGLESApp.iOS.StaticLibrary` 创建一个 iOS 静态库 (.a) 文件，其中包含 `MyOpenGLESApp.Shared` 中的共享代码。  它链接到由 `MyOpenGLESApp.iOS.Application` 项目创建的应用。

- `MyOpenGLESApp.Shared` 包含跨平台运行的共享代码。 它使用预处理器宏进行特定于平台代码的条件编译。 共享代码由 `MyOpenGLESApp.Android.NativeActivity` 和 `MyOpenGLESApp.iOS.StaticLibrary` 的项目引用拾取。

该解决方案包含两个项目来生成适用于 Android 和 iOS 平台的应用：

- `MyOpenGLESApp.Android.Packaging` 创建 .apk 文件，用于 Android 设备或仿真程序上的开发。  此文件包括在此设置清单属性的资源和 AndroidManifest.xml 文件。 它还包括控制 Ant 生成过程的 build.xml 文件。  默认情况下，它被设置为启动项目，因此可从 Visual Studio 直接部署和运行它。

- MyOpenGLESApp.iOS.Application 包含资源和 Objective-C 粘附代码，以用于创建链接到 `MyOpenGLESApp.iOS.StaticLibrary` 中 C++ 静态库代码的 iOS 应用。  此项目创建一个生成包，该包通过 Visual Studio 和远程代理传输到你的 Mac。 当创建此项目时，Visual Studio 将发送文件和命令以在 Mac 上生成并部署应用。

## <a name="build-and-run-the-android-app"></a>生成并运行 Android 应用

由模板创建的解决方案将 Android 应用设置为默认项目。  你可以生成并运行此应用以验证安装和设置。 对于初始测试，在由适用于 Android 的仿真器安装的其中一个设备配置文件上运行该应用。 如果想要在其他目标上测试应用，可加载目标仿真程序或将设备连接到计算机。

### <a name="to-build-and-run-the-android-native-activity-app"></a>若要生成并运行 Android 本机活动应用

1. 如果尚未选中，则从“解决方案平台”  下拉列表中选择“x86”  。

   ![将解决方案平台设置为 x86](../cross-platform/media/cppmdd_opengles_solutionplat.png "CPPMDD_OpenGLES_SolutionPlat")

   使用 x86 指定仿真器目标。 若要针对一种设备，则基于设备处理器选择解决方案平台。 如果未显示“解决方案平台”  列表，则从“添加/删除按钮”  列表中选择“解决方案平台”  ，然后选择你的平台。

1. 在“解决方案资源管理器”中，打开 `MyOpenGLESApp.Android.Packaging` 项目的快捷菜单，然后选择“生成”。  

   ![生成 Android 打包项目](../cross-platform/media/cppmdd_opengles_andbuild.png "CPPMDD_OpenGLES_AndBuild")

   “输出”窗口显示 Android 共享库和 Android 应用的生成过程的输出。

   ![为 Android 项目生成输出](../cross-platform/media/cppmdd_opengles_andoutput.png "CPPMDD_OpenGLES_AndOutput")

1. 选择其中一个仿真 Android 设备配置文件作为部署目标。

   ![选择部署目标](../cross-platform/media/cppmdd_opengles_pickemulator.png "CPPMDD_OpenGLES_PickEmulator")

   如果你已安装了其他仿真程序或连接了一个 Android 设备，则可在部署目标下拉列表中选择它们。 若要运行该应用，生成的解决方案平台必须与目标设备的平台匹配。

1. 按下 F5 启动调试，或按下 Shift+F5 来在不进行调试的情况下启动。

   Visual Studio 启动仿真程序，需要几秒钟时间来加载和部署代码。 下面介绍了此应用如何显示在仿真器中：

   ![在 Android 仿真器中运行的应用](../cross-platform/media/cppmdd_opengles_andemulator.png "CPPMDD_OpenGLES_AndEmulator")

   一旦你的应用启动，你可以设置断点，并使用调试器逐步调试代码，检查局部变量并监视值。

1. 按下 Shift+F5 来停止调试。  

   仿真程序是一个继续运行的单独进程。 你可多次编辑、编译和部署代码到同一仿真程序。 应用将显示在仿真程序中的应用集合上，它可以从那里直接启动。

   生成的 Android 本机活动应用和库项目将 C++ 共享代码放入包含“粘附”代码的动态库中，从而与 Android 平台连接。 大部分应用代码位于库中，并且清单、资源和生成说明位于打包项目中。 共享代码从 NativeActivity 项目中的 main.cpp 调用。 有关如何对 Android 本机活动进行编程的详细信息，请参阅 Android 开发人员 NDK [概念](https://developer.android.com/ndk/guides/concepts.html) 页。

   Visual Studio 使用 Android NDK（其将 Clang 用作平台工具集）构建 Android 本机活动项目。 Visual Studio 将 NativeActivity 项目中的属性映射到用于在目标平台上进行编译、链接和调试的选项。 有关详细信息，打开 MyOpenGLESApp.Android.NativeActivity 项目的“属性页”  对话框。 有关命令行开关的详细信息，请参阅 [Clang 编译器用户手册](http://clang.llvm.org/docs/UsersManual.html)。

## <a name="build-and-run-the-ios-app-on-an-ios-device"></a>在 iOS 设备上生成并运行 iOS 应用

iOS 应用项目在 Visual Studio 中创建和编辑，但由于授权限制，它必须从 Mac 生成和部署。 Visual Studio 与在 Mac 上运行的远程代理进行通信，以传输项目文件并执行生成、部署和调试命令。 在生成 iOS 应用前设置和配置 Mac 和 Visual Studio 以进行通信。 有关详细说明，请参阅[安装并配置使用 iOS 进行生成的工具](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。 远程代理在 Mac 上运行且与 Visual Studio 配对后，则可以生成并运行 iOS 应用以验证安装和设置。

若要将 iOS 应用部署到 iOS 设备，还必须在 Mac 的 Xcode 上设置自动签名。 自动签名自动管理应用签名，并创建预配配置文件以对应用生成进行签名。

### <a name="to-set-up-automatic-signing-on-xcode"></a>在 Xcode 上设置自动签名

1. 如果尚未设置，请在 Mac 上安装 [Xcode](https://developer.apple.com/xcode/downloads/) 版本 10.2.1 或更高版本。

1. 在 Mac 上打开 Xcode 应用。

1. 创建新的“单视图应用程序”  Xcode 项目。 在项目创建期间填写必填字段。 值可以是任意的，因为该项目仅用于创建预配配置文件，该配置文件稍后用于对应用生成进行签名。

1. 将在 [Apple 开发人员计划](https://developer.apple.com/programs/)帐户中注册的 Apple ID 添加到 Xcode。 你的 Apple ID 用作签名标识以对应用进行签名。 若要添加 Xcode 中的签名标识，请打开 Xcode  菜单并选择  “首选项”。 选择“帐户”  并单击“添加按钮(+)”以添加你的 Apple ID。 有关详细说明，请参阅[添加 Apple ID 帐户](https://help.apple.com/xcode/mac/current/#/devaf282080a)。

1. 从 Xcode 项目的“常规”设置中，将“捆绑标识符”  的值更改为 `com.<NameOfVSProject>`，其中 `<NameOfVSProject>` 与你创建的 Visual Studio 解决方案项目同名。 例如，如果已在 Visual Studio 上创建名为 `MyOpenGLESApp` 的项目，则将“捆绑标识符”  设置为 `com.MyOpenGLESApp`。

   ![Xcode 捆绑标识符](../cross-platform/media/cppmdd-opengles-iosxcodeid.png "CPPMDD_OpenGLES_iOSXcodeId")

1. 若要启用自动签名，请选中 “自动管理签名**”。

   ![Xcode 自动签名](../cross-platform/media/cppmdd-opengles-iosxcodesign.png "CPPMDD_OpenGLES_iOSXcodeSign")

1. 选择添加为开发团队  的 Apple ID 的团队名称。

   ![Xcode 团队](../cross-platform/media/cppmdd-opengles-iosxcodeteam.png "CPPMDD_OpenGLES_iOSXcodeTeam")

### <a name="to-build-and-run-the-ios-app-on-an-ios-device"></a>在 iOS 设备上生成并运行 iOS 应用

1. 在 Mac 上运行远程代理，并验证 Visual Studio 是否与远程代理配对。 若要启动远程代理，请打开终端应用窗口并输入 `vcremote`。 有关详细信息，请参阅[在 Visual Studio 中配置远程代理](../cross-platform/install-and-configure-tools-to-build-using-ios.md#ConfigureVS)。

   ![运行 vcremote 的 Mac 终端窗口](../cross-platform/media/cppmdd_common_vcremote.png "CPPMDD_common_vcremote")

1. 将 iOS 设备连接到 Mac。 首次将设备连接到计算机后，会出现询问你是否信任计算机访问设备的警报。 使设备能够信任 Mac 计算机。

1. 在 Visual Studio 上，如果尚未选中，请基于你的设备处理器从“解决方案平台”  下拉列表中选择解决方案平台。 在此示例中为 ARM64  处理器。

   ![将解决方案平台设置为 ARM64](../cross-platform/media/cppmdd-opengles-pickplatformarm64.png "CPPMDD_OpenGLES_SolutionPlatARM64")

1. 在“解决方案资源管理器”中，打开 MyOpenGLESApp.iOS.Application 项目的快捷菜单，然后选择“卸载项目”以卸载项目  。

1. 再次，打开已卸载的 MyOpenGLESApp.iOS.Application 项目的快捷菜单，然后选择“编辑 project.pbxproj”  以编辑项目文件。 在 `project.pbxproj` 文件中，查找 `buildSettings` 属性并使用 Apple 团队 ID 添加 `DEVELOPMENT_TEAM`。 以下屏幕截图显示 Apple 团队 ID 的 `123456ABC` 的示例值。 可以从 Xcode 中找到 Apple 团队 ID 的值。 转到“生成设置”  并将鼠标悬停在开发团队名称上以显示工具提示。 工具提示显示团队 ID。

   ![设置开发团队](../cross-platform/media/cppmdd-opengles-iosdevelopmentteam.png "CPPMDD_OpenGLES_iOSDevelopmentTeam")

1. 关闭 `project.pbxproj` 文件，然后打开已卸载的 MyOpenGLESApp.iOS.Application 项目的快捷菜单，然后选择“重新加载项目”  以重新加载项目。

1. 现在，通过打开 MyOpenGLESApp.iOS.Application 项目的快捷菜单并选择“生成”来生成该项目  。

   ![生成 iOS 应用程序项目](../cross-platform/media/cppmdd_opengles_iosbuild.png "CPPMDD_OpenGLES_iOSBuild")

   “输出”窗口显示 iOS 静态库和 iOS 应用的生成过程的输出。 在 Mac 上，运行远程代理的终端窗口显示命令和文件传输活动。

   在 Mac 计算机上，系统可能会提示你允许 codesign 访问密钥链。 选择“允许”以继续。 

1. 选择工具栏上的 iOS 设备以在连接到 Mac 的设备上运行该应用。 如果应用不启动，请验证设备是否为已部署的应用程序提供在设备上执行的权限。 可以通过转到设备上的“设置”   > “常规”   > “设备管理”  来设置此权限。 选择你的开发人员应用帐户，信任你的帐户并验证该应用。 尝试从 Visual Studio 再次运行该应用。

   ![iOS 设备上的 iOS 应用](../cross-platform/media/cppmdd-opengles-iosdevice.png "CPPMDD_OpenGLES_iOSDevice")

   启动应用后，你可以设置断点，并使用 Visual Studio 调试器检查局部变量、查看调用堆栈并监视值。

   ![iOS 应用中断点处的调试器](../cross-platform/media/cppmdd_opengles_iosdebug.png "CPPMDD_OpenGLES_iOSDebug")

1. 按下 Shift+F5 来停止调试。  

   生成的 iOS 应用和库项目将 C++ 代码放入仅实现共享代码的静态库。 大多数应用程序代码位于 `Application` 项目中。 此模板项目中对共享库代码的调用在 GameViewController.m 文件中进行。  若要生成 iOS 应用，Visual Studio 将使用 Xcode 平台工具集，这要求与在 Mac 上运行的远程客户端进行通信。

   Visual Studio 传输项目文件并发送命令到远程客户端以生成使用 Xcode 的应用。 远程客户端将生成状态信息返回到 Visual Studio。 如果应用已成功生成，你就可以使用 Visual Studio 发送命令来运行和调试应用。 Visual Studio 中的调试器控制在连接到 Mac 的 iOS 设备上运行的应用。 Visual Studio 将 StaticLibrary 项目中的属性映射到用于在目标 iOS 平台上进行编译、链接和调试的选项。 若要了解编译器命令行选项的详细信息，请打开 MyOpenGLESApp.iOS.StaticLibrary 项目的  “属性页”对话框。

## <a name="customize-your-apps"></a>自定义应用

可修改共享的 C++ 代码以添加或更改常用功能。 必须更改 `MyOpenGLESApp.Android.NativeActivity` 和 `MyOpenGLESApp.iOS.Application` 项目中对共享代码的调用以匹配。 可使用预处理器宏来指定公共代码中特定于平台的部分。 预处理器宏 `__ANDROID__` 在你针对 Android 进行生成时进行了预定义。 预处理器宏 `__APPLE__` 在你针对 iOS 进行生成时进行了预定义。

若要查看特定项目平台的 IntelliSense，请在编辑器窗口顶部导航栏中的上下文切换器下拉列表中选择项目。

![在编辑器中投射上下文切换器下拉列表](../cross-platform/media/cppmdd_opengles_contextswitcher.png)

当前项目所使用的代码中的 IntelliSense 问题都标有红色的波浪线。 其他项目中的问题都标有紫色波浪线。 Visual Studio 不支持 Java 或 Objective-C 文件的代码着色或 IntelliSense。 但是，仍可以修改源文件和更改资源来设置应用程序名称、图标和其他实现详细信息。
