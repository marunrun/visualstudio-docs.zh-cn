---
title: 生成操作
description: 本文介绍可用于 C# 项目的各种生成操作
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 5399BCB1-E317-4C7B-87B1-C531E985DE6E
ms.openlocfilehash: d55ab6aea15dbad7f1cbd718136fba261dfa1c69
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "74983258"
---
# <a name="build-actions"></a>生成操作

Visual Studio for Mac 项目中的所有文件都具有生成操作。 该操作控制生成期间文件会发生什么情况。 可通过右键单击任意文件并浏览到“生成操作”对其进行设置，如下所示  ：

![从解决方案资源管理器选择编译生成操作](media/projects-and-solutions-image1.png)

C# 项目的一些常见生成操作为：

* **无** - 文件不属于任何一种生成 - 它包括在项目中为了便于从 IDE 轻松访问。
* **编译** - 文件将被传递到 C# 编译器作为源文件。
* **嵌入式资源** - 文件将被传递到 C# 编译器作为嵌入程序集中的资源。 来自 [ 命名空间的 ](/dotnet/api/system.reflection.assembly.getmanifestresourcestream)Assembly.GetManifestResourceStream`System.Reflection` 可用于从程序集中读取文件。
* **内容** - 对于 ASP.NET 项目，将在部署站点时包含这些文件，作为站点的一部分。 对于 Xamarin.iOS 和 Xamarin.Mac 项目，它们会被包含在应用程序包中。

可在解决方案资源管理器中选择多个文件，这样便可同时设置多个文件的生成操作。

此外，还有针对特定项目的生成操作。 Xamarin.iOS 项目具有 BundleResource  生成操作，用于将文件添加为应用程序包的一部分。 有关 Xamarin.Android 特定生成操作的信息，请参阅[生成过程](/xamarin/android/deploy-test/building-apps/build-process#Build_Actions)指南。

## <a name="see-also"></a>另请参阅

- [生成操作（Windows 上的 Visual Studio）](/visualstudio/ide/build-actions)