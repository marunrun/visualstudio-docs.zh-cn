---
title: 项目和解决方案
description: 本文档概述了 Visual Studio for Mac 中的项目和解决方案。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/23/2019
ms.assetid: 8254505D-D96E-48BD-8A5E-CF6A917897EA
ms.openlocfilehash: b66a1dfbe0569c501d05b34425e198f1501438ca
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67691277"
---
# <a name="projects-and-solutions-in-visual-studio-for-mac"></a>Visual Studio for Mac 中的项目和解决方案

本文概述 Visual Studio for Mac 中的项目和解决方案概念   。

> [!NOTE] 
> 本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅 [Visual Studio 中的项目和解决方案](/visualstudio/ide/solutions-and-projects-in-visual-studio)。

## <a name="projects"></a>项目

在 Visual Studio for Mac 中创建新的应用程序、网站等内容时，要从项目开始。 项目包含编译可执行文件、库或网站中所需的全部文件（源代码、图像、数据文件等）。

项目由包含 xml 的文件（如 C# 项目的 `.csproj`）定义，其中 xml 定义文件和文件夹层次结构、文件路径以及项目特定设置（如生成设置）。

当 Visual Studio for Mac 加载项目时，Solution Pad 使用项目文件显示项目中的文件和文件夹。 编译期间，MSBuild 读取项目文件中的设置以创建可执行文件。

## <a name="solutions"></a>解决方案

（  解决方案是将一个或多个相关项目分组到一起的容器。） 解决方案由格式唯一的文本文件（扩展名 `.sln`）描述；不应对其进行手动编辑。

## <a name="managing-projects-in-the-solution-pad"></a>在 Solution Pad 中管理项目

创建或加载项目之后，可以使用 Solution Pad 查看和管理项目或解决方案以及其中包含的文件。 下图显示具有包含两个项目的 .NET Core 解决方案的 Solution Pad：

![包含多个项目的示例解决方案](media/solution-example.png)

通过双击项目或解决方案名称或右键单击并选择“选项”，可以同时管理项目和解决方案的属性  。

有关这些选项的详细信息，请参阅[管理解决方案和项目属性](managing-solutions-and-project-properties.md)一文。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的解决方案和项目 (Windows)](/visualstudio/ide/solutions-and-projects-in-visual-studio)
