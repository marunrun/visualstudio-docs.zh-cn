---
title: 使用 C++ 进行跨平台移动开发 | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 0bb872d6-981b-4c96-9143-fcec5336bf0d
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 61bb3e17b104759995852959a7396d5a76927cfb
ms.sourcegitcommit: 8a96a65676fd7a2a03b0803d7eceae65f3fa142b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72589044"
---
# <a name="cross-platform-mobile-development-with-c"></a>使用 C++ 进行跨平台移动开发

你可以使用 Visual Studio 中提供的跨平台工具为 iOS、Android 和 Windows 设备生成本机 C++ 应用。  使用 C++ 的移动开发是 Visual Studio 安装程序中提供的一种工作负载。 它安装了 SDK 以及共享库和本机应用的跨平台开发所需的工具。 安装后，你可以使用 C++ 创建在 iOS 和 Android 设备和平台、Windows、Windows 应用商店和 Xbox 上运行的代码。

为多个平台编写代码常常让人头疼。 面向 iOS、Android 和 Windows 的主要开发语言和工具因平台而异。 但是，所有平台都支持用 C++ 编写代码。 这是可用于实现跨平台重用核心代码的公分母。 用 C++ 编写的本机代码可能具有更高的性能，同时可避免反向工程的影响。 在创建用于多个平台的应用时，代码重用可以节约时间和精力。

使用用于跨平台移动开发的 C++ 进行开发具有以下优点：

- **安装简便。** Visual Studio 安装程序将获取并安装所需的第三方工具，以及构建适用于 Android 和 iOS 的应用或库所需的 SDK。 配置和安装很简单，并且主要是自动进行的。

- **功能强大且熟悉的生成环境。** 使用 Visual Studio 模板轻松创建可共享的跨平台解决方案和项目。 使用一个通用接口管理所有项目的属性。 在 Visual Studio 编辑器中编辑你的所有代码，并利用内置的跨平台 IntelliSense 补全代码和突出显示错误。

- **统一的调试体验。** 使用 Visual Studio 中世界一流的调试工具监视所有平台上的 C++ 代码并逐步执行代码：Android 设备和仿真器、iOS 模拟器和设备以及 Windows 或 Windows 应用商店设备和仿真器。

## <a name="get-the-tools"></a>获取工具

使用 C++ 的移动开发是 Visual Studio 附带的可安装工作负载。 有关系统必备和安装说明，请参阅[使用 C++ 安装跨平台移动开发](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)。 若要生成用于 iOS 的代码，你还需要 Mac 计算机和 Apple iOS 开发人员帐户。 有关详细信息，请参阅[安装并配置使用 iOS 进行构建的工具](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。

## <a name="come-up-to-speed"></a>加快速度

如果你来自 Android 或 iOS 开发部门，我们可以向你提供有关如何入门的有用资料。 Visual Studio 是一个表现力和功能均十分强大的开发环境。 若要了解如何使用，请阅读 [Android 开发人员入门](/previous-versions/windows/apps/dn275875\(v=win.10\))或 [iOS 开发人员入门](/previous-versions/windows/apps/jj657966\(v=win.10\))。 这些文章将向你介绍 Visual Studio 以及开发用于 Windows 和 Windows 应用商店的跨平台应用时所需的概念。 若要开始编写你的第一个用于 iOS 和 Android 的跨平台应用，请参阅[在 Android 和 iOS 上生成 OpenGL ES 应用程序](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)。

使用 C++ 的移动开发工作负载包括多个模板，可帮助你开始编写应用：

- OpenGLES 2 应用程序（Android、iOS 和 Windows Universal）

  创建包含一组项目的解决方案，用于构建 Android 本机活动应用、iOS 应用、通用 Windows 应用以及共享的 C++ 代码库。 这些应用使用通过使用公共 C++ OpenGL ES 代码创建的特定于平台的库，以在每个应用中绘制相同的旋转立方体。 若要使用此模板，则在安装 Visual Studio 时，必须随附通用 Windows 应用开发工具工作负载  。

- Native-Activity 应用程序(Android)

  创建一个完整的 C++ OpenGL 应用作为 Android 本机活动项目。

- OpenGLES 应用程序(Android、iOS)

  创建一个解决方案，其中包括一组用于构建 Android 本机活动应用和 iOS 应用的项目。 这些应用使用通过使用公共 C++ OpenGL ES 代码创建的特定于平台的库，以在每个应用中绘制相同的旋转立方体。

- 共享库 (Android、iOS)

  创建一个解决方案，其中包括在共享项目中使用公共 C++ 代码创建 Android 动态库 (.so) 文件和 iOS 静态库 (.a) 文件的项目。

- 基本应用程序（Android、Ant）

  创建仅使用 Java 源代码和 Ant 生成系统的 Android "Hello，World" 应用项目。

- 基本应用程序（Android、Gradle）

  创建仅使用 Java 源代码和 Gradlet 生成系统的 Android "Hello，World" 应用项目。

- 基本库（Android、Ant）

  创建仅使用 Java 源代码和 Ant 生成系统的 Android "Hello，World" 库项目。

- 基本库（Android、Gradle）

  创建仅使用 Java 源代码和 Gradle 生成系统的 Android "Hello，World" 库项目。

- 动态共享库(Android)

  通过使用 C++ 代码创建一个 Android 动态库 (.so) 文件。

- OpenGLES 2 应用程序 (iOS)

  创建具有一组项目的解决方案，用于构建 OpenGL ES 2 iOS 应用。 该应用使用 C++ OpenGL ES 代码库在 iOS 应用中绘制旋转立方体。 该应用是用于查看如何将 C++ 库导入 iOS 应用的良好起点。

- 静态库(Android)

  创建一个项目以构建用于 Android 的静态库。 你仅能链接 Android 应用中的一个动态库，但你可以链接到任意数量的静态库。

- 静态库(iOS)

  创建一个项目以构建用于 iOS 的静态库。

- 生成文件项目(Android)

  为你自己的 Android 生成文件项目创建项目包装。

## <a name="try-out-sample-code"></a>试用示例代码

下载演示如何创建可以在 Windows、Android 和 iOS 应用中使用的共享代码库的示例。 并且，查看如何创建用于 Android 的完整本机活动应用的示例。 若要开始操作，请参见[跨平台移动开发示例](../cross-platform/cross-platform-mobile-development-examples.md)。

## <a name="see-also"></a>请参阅

[使用 C++ 安装跨平台移动开发](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)\
[安装并配置使用 iOS 进行构建的工具](../cross-platform/install-and-configure-tools-to-build-using-ios.md)\
[创建 Android 本机活动应用](../cross-platform/create-an-android-native-activity-app.md)\
[在 Android 和 iOS 上生成 OpenGL ES 应用程序](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)\
[跨平台移动开发示例](../cross-platform/cross-platform-mobile-development-examples.md)
