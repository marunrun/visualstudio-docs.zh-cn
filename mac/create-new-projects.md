---
title: 创建新项目和解决方案
description: 本文介绍如何在 Visual Studio for Mac 中创建项目和解决方案
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/23/2019
ms.assetid: 5880BB10-0A12-47E2-8A82-7A2D59C4D579
ms.openlocfilehash: dbfc0d951524bb9ffbbd4a2366679cfc6ae41925
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67693055"
---
# <a name="creating-a-new-project"></a>创建新项目

## <a name="opening-the-project-creation-dialog"></a>打开“项目创建”对话框

可通过多种方式在 Visual Studio for Mac 中创建新项目。 首次打开 Visual Studio for Mac 时，将显示欢迎屏幕。 可在此处选择“新建”，随即将转到项目创建屏幕  。

> [!TIP]
> 此外，在欢迎屏幕中，还可以打开并搜索最近的项目和解决方案。 还可以通过转到菜单栏并依次选择“文件”、“最近使用的解决方案”来打开最近使用的项目 

![包含新建项目选项的欢迎屏幕](media/first-run-project.png)

如果 Visual Studio for Mac 已打开，并且已加载解决方案，可以通过转到菜单栏并依次选择“文件”、“新建解决方案”来创建新解决方案  。 通过此方法创建新解决方案将关闭已加载的解决方案。

## <a name="creating-a-new-project-from-a-template"></a>根据模板创建新项目

默认情况下，“新建项目”对话框将按“最近使用”排序显示最近使用的模板   。

如果不想使用最近使用的模板，可以从对话框左侧的类别中进行选择。 每个类别包含多个项目模板，你可以随意选择。 单击项目类型可查看屏幕右侧的描述。

![“新建项目”屏幕](media/project-creation-screen.png)

## <a name="configuring-your-new-project"></a>配置新项目

选择项目模板后，以下屏幕将显示设置项目所需的任何配置步骤；这些步骤可能因项目类型而所有不同。

所有项目都需要一个新项目以及存储文件的位置。 如果项目属于新解决方案，而不是将添加到现有解决方案，则还需要提供解决方案名称。

在此阶段，还可以选择配置 Git 源代码管理选项。 下图是配置 .NET Core 项目的最终步骤示例：

![配置新项目](media/configure-new-project.png)

## <a name="adding-additional-projects-to-a-solution"></a>向解决方案添加其他项目

可通过右键单击 Solution Pad 中的解决方案并依次选择“添加”、“添加新项目”，或者依次选择“添加”、“添加现有项目”，向解决方案添加其他项目   。

添加新项目将引导你完成项目创建步骤，如[配置新项目](#configuring-your-new-project)中所示。

选择添加现有项目，你将能浏览计算机上的现有项目并将其添加到解决方案。

## <a name="see-also"></a>请参阅

- [创建解决方案和项目（Windows 上的 Visual Studio）](/visualstudio/ide/creating-solutions-and-projects)