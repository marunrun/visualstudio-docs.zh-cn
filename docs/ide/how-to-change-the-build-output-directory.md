---
title: 如何：更改生成输出目录
ms.date: 05/15/2019
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- output directory, changing
ms.assetid: a8333c89-afb2-4b1d-b2e2-9146da852402
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e006be2099d5132ce7445f1e8fe74b0f2752c260
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416809"
---
# <a name="how-to-change-the-build-output-directory"></a>如何：更改生成输出目录

可以在预配置的基础上指定项目生成的输出的位置（用于调试、发布或两者）。

## <a name="change-the-build-output-directory"></a>更改生成输出目录

1. 要打开项目的属性页面，右键单击“解决方案资源管理器”中的项目节点，然后选择“属性”   。

2. 根据项目类型选择相应的选项卡：

   - 对于 C#，选择“生成”选项卡  。
   - 对于 Visual Basic，选择“编译”选项卡  。
   - 对于 C++ 或 JavaScript，选择“常规”选项卡  。

3. 在顶部的配置下拉列表中，选择你想要更改其输出文件位置的配置（“调试”、“发布”或“所有配置”）    。

4. 在页面上找到输出路径条目，路径条目根据项目类型而有所不同：

   - C# 和 JavaScript 项目的输出路径 
   - Visual Basic 项目的生成输出路径 
   - Visual C++ 项目的输出目录 

   键入要生成输出的路径（绝对或相对于根项目目录），或选择“浏览”，浏览到该文件夹  。

   ![Visual Studio C# 项目的输出路径属性](media/output-path.png)

> [!TIP]
> 如果系统未将输出生成到指定位置，请在 Visual Studio 的菜单栏上选择该位置，确保构建相应的配置（例如“调试”或“发布”）   。
>
> ![在 Visual Studio 2019 中生成配置选取器](media/build-configuration-chooser.png)

## <a name="see-also"></a>请参阅

- [项目设计器的“生成”页 (C#)](../ide/reference/build-page-project-designer-csharp.md)
- [常规属性页（项目）](/cpp/build/reference/general-property-page-project)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)