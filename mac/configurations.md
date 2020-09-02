---
title: 了解生成配置
description: 本文介绍 Visual Studio for Mac 中的各种生成配置
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.assetid: 78107CFA-9308-4293-A92A-9B552A259E15
ms.openlocfilehash: d1511434a34017a7f0f7da65fe1ea6956d45d497
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "71128403"
---
# <a name="understanding-build-configurations"></a>了解生成配置

在开发过程中，可以存储不同的解决方案配置和项目属性以便在各种生成中使用。 由 Visual Studio for Mac 使用模板创建的项目通常包括“调试”和“发布”配置，分别支持应用的调试和部署。 

若要创建自定义配置，请参阅[创建和编辑生成配置](/visualstudio/mac/create-and-edit-configurations)。

>[!NOTE]
>本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅[了解生成配置](/visualstudio/ide/understanding-build-configurations)。

## <a name="solution-configurations"></a>解决方案配置

解决方案配置用于指定解决方案中所有项目的配置。 通过使用“生成”>“配置”项下的“配置映射”选项卡，可以为打开的解决方案中的每一项分配一个目标配置********。 下图对此进行了演示：

![配置映射选项](media/projects-and-solutions-image3.png)

有关配置的详细信息，请参阅 James Montemagno 的[配置管理器](https://www.youtube.com/watch?v=tjSdkqYh5Vg)视频。

## <a name="project-build-configurations"></a>项目生成配置

项目往往有多个配置。 项目针对的配置和平台结合使用以指定在生成时要使用的属性。 生成时在这些配置之间进行切换可以得到不同的输出。 例如，调试配置将输出调试符号，使得调试程序可以从有故障的应用程序的堆栈跟踪中解决函数名称、参数或变量。 尽管此附加信息在开发期间很有用，但它会导致文件大小膨胀，并且不适合分发。

每个平台都有针对自己生成特定的配置。 可以通过导航到“项目选项”对话框中的“生成”部分来访问项目的生成配置页面********。 要打开此对话框，请右键单击项目并选择“选项”，或在解决方案资源管理器中双击项目****。

## <a name="run-configuration"></a>运行配置

Visual Studio for Mac 允许设置运行配置__。 在工具栏的下拉列表中，运行配置显示在生成配置选择器旁，如下所示：

![“运行配置”下拉列表](media/projects-and-solutions-image8.png)

运行配置是一组包含名称和多个配置的执行选项，其中名称和这些配置根据不同用途在项目中进行了定义。 运行配置根据项目级进行定义，虽然可添加所需的数量，但将为每个可执行项目自定创建默认值。 某些项目类型自动生成其他运行配置。 例如，watchOS 项目可生成速览和通知配置。

配置可以与其他开发者共享（此时配置存储在 .csproj 文件中），或保留在本地（此时存储在 .user 文件中）。

### <a name="android-run-configurations"></a>Android 运行配置

Android 项目的运行配置可以在运行或调试项目时指定要启动的特定活动、服务或广播接收器。 可以传递额外的意向数据并设置意向标记，以测试不同启动条件下的组件。

`MainLauncher` 以外的活动需要添加将 `Exported=true` 添加到活动属性，以在物理设备上调试或定义意图筛选器。

## <a name="examples-of-data-that-might-be-included-in-run-configurations"></a>运行配置中可能包含的数据的示例

以下列表提供可能包含在运行配置中的数据的一些示例：

* 常规 .NET 项目
  * 可选的启动应用
  * 启动参数
  * 工作目录
  * 环境变量
  * Mono 运行时选项（仅在 Mono 上运行时使用）
* Android 项目
  * 入口点（活动、服务、接收器）
  * 意向参数和数据
* iOS 项目
  * 模式（常规、后台获取）
* iOS 扩展项目
  * 启动应用：默认或自定义
* WatchKit 项目
  * 模式（速览、通知）
  * 通知有效负载

## <a name="see-also"></a>另请参阅

- [了解生成配置（Windows 上的 Visual Studio）](/visualstudio/ide/understanding-build-configurations)
