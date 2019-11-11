---
title: 跨平台移动开发示例 | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: bc384c12-fccc-45d7-9fb9-b90d536aa663
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 8eb8b53da30f0c0896ac9576407d34f9a2f9bdbc
ms.sourcegitcommit: 57bc1c3887838d707c13feff72a677b3bad3be4b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72777709"
---
# <a name="cross-platform-mobile-development-examples"></a>跨平台移动开发示例

由“采用 C++ 的移动开发”  工作负载安装的若干模板生成完整的示例，你可以使用这些示例进行学习。 此外，Windows 开发人员中心有若干示例应用程序，你可以在 Visual Studio 中下载并试用。

- [hello-jni Android 应用程序示例](https://code.msdn.microsoft.com/hello-jni-Android-790ab73d)

   此示例是 Android NDK hello-jni 应用程序的端口。 此示例演示一个端到端 Java 本机接口“Hello World”应用。 它从一个在共享库中实现的本机方法中加载字符串，然后在应用中显示。

- [hello-gl2 Android 应用程序示例](https://code.msdn.microsoft.com/hello-gl2-Android-3b61896c)

   此示例是 Android NDK hello-gl2 应用程序的端口。 此示例演示一个端到端 Java 本机接口 Android OpenGL 应用。 它将呈现一个使用 OpenGL ES 2.0 着色器 API 的三角形。

- [Bitmap Plasma Android 应用程序示例](https://code.msdn.microsoft.com/Bitmap-Plasma-Android-77ae296a)

   此示例是 Android NDK Bitmap Plasma 应用程序的端口。 此示例演示一个端到端 Java 本机接口 Android OpenGL ES 2.0 应用程序。 它演示了直接操作 Android 位图像素缓冲区来生成等离子效果。

- [TwoLibs Android 库示例](https://code.msdn.microsoft.com/TwoLibs-Android-Library-6396e5c4)

   此示例是 Android NDK TwoLibs 示例的端口。 它使用动态加载的共享库和静态的 C++ Android 本机库，用于实现从 Java 本机接口应用调用的方法。 此示例是开发者理解如何在 Visual Studio 中使用静态/动态共享库以生成端到端 JNI Android 应用程序的良好开端。

- [Tea Pot Android 应用程序示例](https://code.msdn.microsoft.com/Tea-Pot-Android-Application-e7c05d73)

   此示例是 Android NDK TeaPot 应用程序的端口。 此示例演示一个端到端 Java 本机接口 Android OpenGL ES 2.0 应用程序。

- [MoreTeaPots Android 应用程序示例](https://code.msdn.microsoft.com/MoreTeaPots-Android-a9bd8549)

   此示例是 Android NDK MoreTeaPots 应用程序的端口。 此示例演示一个端到端 Java 本机接口 Android OpenGL 应用程序。

- [test-libstdcpp Android 库示例](https://code.msdn.microsoft.com/test-libstdcpp-Android-00b548f5)

   此示例是 Android NDK test-libstdc++ 示例的端口，专用于 Visual Studio。 此示例是开发人员了解如何使用标准库的良好开端。

  若要在 Visual Studio 中打开其中一个示例，请下载 zip 文件并在资源管理器中打开所下载文件的“属性”  页。 选择“解除阻止”  按钮，然后选择“确定”  。 将 zip 文件的内容解压缩到一个方便的位置，然后在解压缩后的示例中打开 C++ 文件夹，并打开解决方案文件。

  若要生成示例，请按 F7，或在菜单栏上依次选择“生成”、“生成解决方案”    。
