---
title: 管理项目和解决方案属性
description: 本文介绍如何在 Visual Studio for Mac 中管理项目和解决方案的属性
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/09/2020
ms.assetid: 75247EB8-323A-4AFD-A451-6703A03D5D1F
ms.openlocfilehash: 0c3277df3be22658acf85a4f0607ed9ad0308b5c
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "94492992"
---
# <a name="managing-project-and-solution-properties"></a>管理项目和解决方案属性

## <a name="project-options"></a>项目选项

项目选项特定于每个项目，影响项目的编写、生成和运行方式。 与作为特定于用户的设置的 Visual Studio for Mac 首选项不同，项目选项存储在项目 (.csproj) 文件中，因此其他开发者可以正确生成和运行项目。 具有特定项目选项可使多名开发者同时处理同一文档而不影响文件格式。

若要打开 Visual Studio for Mac 中的项目选项，请双击项目名称，或右键单击以打开上下文菜单，并选择“选项”：

![上下文菜单中的选项](media/projects-and-solutions-image2.png)

可编辑的选项包括用于生成、运行和设置源代码的选项以及版本控制。

项目选项分为五个不同类别：

* 常规 - 可在此处设置名称、描述和默认命名空间等项目信息，以及项目位置。
* 生成 - 用于为可移植类库设置或更改 PCL 配置文件。 也支持设置自定义命令、配置和编译器选项。 也可在此设置输出路径和程序集名称。
* 运行 - 用于为每个项目创建自定义运行配置。
* 源代码 - 控制多种不同文件类型和命名约定的格式。 还可在此处设置命名策略和默认标头样式。
* 版本控制 - 在项目中使用版本控制时用于设置提交消息样式的选项。

每个项目都可包含特定项目选项，具体取决于平台。 例如，Xamarin.Android 项目（如下图中所示）具有与 Android 生成相关的选项（如链接器选项）和与应用程序相关的选项（如权限）：

![Android 项目选项](media/projects-and-solutions-image5.png)

Xamarin.iOS 具有与捆绑签名相关的选项（如要使用的所需预配配置文件）：

![iOS 项目选项](media/projects-and-solutions-image6.png)

## <a name="solution-options"></a>解决方案选项

解决方案选项与项目选项类似，但包括整个解决方案范围。 这些选项提供了设置作者信息、生成设置、代码格式样式和版本控制的方法，也提供了在解决方案中分配启动项目的方法。  可通过“项目”>“解决方案选项”菜单项，或通过解决方案窗口中“解决方案”上的“选项”上下文菜单项，或通过双击解决方案窗口中的“解决方案”，来访问解决方案选项对话框 ：

![解决方案选项](media/projects-and-solutions-image7.png)

## <a name="see-also"></a>另请参阅

* [管理项目和解决方案属性（Windows 上的 Visual Studio）](/visualstudio/ide/managing-project-and-solution-properties)