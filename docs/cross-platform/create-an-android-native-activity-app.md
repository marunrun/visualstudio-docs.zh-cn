---
title: 创建 Android 本机活动应用 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 884014b1-5208-45ec-b0da-ad0070d2c24d
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: ac2f040addb4c387afe0b325fe53b6a9c289f33a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62819590"
---
# <a name="create-an-android-native-activity-app"></a>创建 Android 本机活动应用

当为跨平台移动开发选项安装 Visual C++ 时，Visual Studio 2015 可用于创建完全正常运行的 Android 本机活动应用。 Android 本机开发工具包 (NDK) 是一个工具集，让你能够使用纯 C/C++ 代码实现大部分的 Android 应用。 一些 Java JNI 代码充当粘附，使 C/C++ 代码可以与 Android 进行交互。 Android NDK 引入了使用 Android API 级别 9 创建本机活动应用的功能。 本机活动代码很受欢迎，可创建使用 Unreal 引擎或 OpenGL 的游戏和图形密集型应用。 本主题将指导你创建使用 OpenGL 的简单本机活动应用。 其他主题向开发人员演示有关编辑、生成、调试和部署本机活动代码的生命周期。

## <a name="requirements"></a>要求

在创建 Android 本机活动应用前，你必须确保已满足所有系统要求，并在 Visual Studio 2015 中安装了 Visual C++ 移动开发选项。 有关详细信息，请参阅 [Install Visual C++ for Cross-Platform Mobile Development](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)。 确保所需的第三方工具和 SDK 包括在安装中，且已安装适用于 Android 的 Microsoft Visual Studio 仿真程序。

## <a name="create-a-new-native-activity-project"></a>创建新的本机活动项目

在本教程中，首先将创建一个新的 Android 本机活动项目，然后在适用于 Android 的 Visual Studio 仿真程序中生成并运行默认应用。

1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”。

2. 在“新建项目”对话框中，在“模板”下，选择“Visual C++” > “跨平台”，然后选择“本机活动应用程序 (Android)”模板。

3. 为应用命名（例如 `MyAndroidApp`），然后选择 **确认**。

    ![创建本机活动项目](../cross-platform/media/cppmdd_newproject.PNG "CppMDD_NewProject")

    Visual Studio 创建新的解决方案并打开解决方案资源管理器。

    ![解决方案资源管理器中的本机活动项目](../cross-platform/media/cppmdd_rc_na_solutionexp.PNG "CPPMDD_RC_NA_SolutionExp")

   新的 Android 本机活动应用解决方案包括两个项目：

- `MyAndroidApp.NativeActivity` 包含应用的引用和粘附代码，以作为本机活动在 Android 上运行。 粘附代码的入口点的实现位于 main.cpp。 预编译头位于 pch.h。 本机活动应用项目编译为一个由打包项目选取的共享库 .so 文件。

- `MyAndroidApp.Packaging` 创建 .apk 文件，用于 Android 设备或仿真程序上的开发。 这包括在此设置清单属性的资源和 AndroidManifest.xml 文件。 它还包括控制 Ant 生成过程的 build.xml 文件。 默认情况下，它被设置为启动项目，因此可从 Visual Studio 直接部署和运行它。

## <a name="build-and-run-the-default-android-native-activity-app"></a>生成和运行默认的 Android 本机活动应用

生成并运行由此模板生成的应用，以验证你的安装和设置。 对于此初始测试，在其中一个由适用于 Android 的 Visual Studio 仿真程序安装的设备配置文件上运行该应用。 如果想要在其他目标上测试应用，可加载目标仿真程序或将设备连接到计算机。

## <a name="to-build-and-run-the-default-native-activity-app"></a>生成并运行默认本机活动应用

1. 如果尚未选中，则从“解决方案平台”下拉列表中选择“x86”。

     ![解决方案平台下拉列表 x86 选择](../cross-platform/media/cppmdd_rc_na_solution_x86.png "CPPMDD_RC_NA_Solution_x86")

     如果未显示“解决方案平台”列表，则从“添加/删除按钮”列表中选择“解决方案平台”，然后选择所需平台。

2. 在菜单栏上，依次选择“生成” > “生成解决方案”。

     “输出”窗口显示针对解决方案中两个项目的生成过程的输出。

3. 选择其中一个 VS 仿真程序 Android Phone (x86) 配置文件作为部署目标。

     如果你已安装了其他仿真程序或连接了一个 Android 设备，则可在部署目标下拉列表中选择它们。

4. 按下 F5 启动调试，或按下 Shift+F5 以在不进行调试的情况下启动。

     以下是适用于 Android 的 Visual Studio 仿真程序中的默认应用。

     ![运行你的应用的仿真程序](../cross-platform/media/cppmdd_emulator_running_app.PNG "CppMDD_Emulator_Running_App")

     Visual Studio 启动仿真程序，需要几秒钟时间来加载和部署你的代码。 一旦你的应用启动，你可以设置断点，并使用调试器逐步调试代码，检查局部变量并监视值。

5. 按下 Shift+F5 来停止调试。

     仿真程序是一个继续运行的单独进程。 你可多次编辑、编译和部署代码到同一仿真程序。