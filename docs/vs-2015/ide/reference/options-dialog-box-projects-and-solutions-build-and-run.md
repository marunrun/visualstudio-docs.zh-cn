---
title: “选项”对话框、项目和解决方案、生成和运行 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.Build_and_Run
- VS.ToolsOptionsPag.Projects.Build_and_Run
helpviewer_keywords:
- builds [Visual Studio], setting up
- run actions
- debugger, run options
ms.assetid: c884976e-c0df-4c6d-8e3a-856ea2bd547c
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9b7eb229c5938165607b797205b94a318e3303b3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655191"
---
# <a name="options-dialog-box--projects-and-solutions-build-and-run"></a>选项对话框，项目和解决方案，生成和运行
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在此对话框中，可以指定可同时生成的 Visual C++ 或 Visual C# 项目的最大数量、某些默认生成行为及一些生成日志设置。 若要打开“选项”对话框中，依次选择菜单栏上的“工具”、“选项”。 若要访问此组选项，请展开“项目和解决方案”，然后选择“生成并运行”。

## <a name="uielement-list"></a>UIElement 列表
 **最大并行项目生成数**指定可以同时生成的视觉C++对象和C#可视化项目的最大数量。 若要优化生成过程，最大并行项目生成数自动设置为你的计算机的 CPU 数量。 最大数量为 32。

 **仅在运行时生成启动项目和依赖项**如果在选择 F5 键时选中此复选框，则仅生成启动项目及其依赖项;在菜单栏上选择 "**调试**"、"**启动**";或选择菜单栏上的 "**生成**" 和 "**生成**"。 如果在选择 F5 键时清楚了此复选框，则将生成所有项目、依赖项和解决方案文件；依次选择菜单栏上的“调试”、“启动”；或者依次选择菜单栏上的“生成”、“生成”。 默认情况下清除此选项。

 **运行期间，当项目过期时**
 > [!NOTE]
> 此列表仅适用于 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 项目。

 默认情况下，如果在选择 F5 键或在菜单栏上依次选择“调试”、“启动”时，项目配置已过期，则将显示一条消息。 你可以指定是否仍要生成项目以及是否显示消息。 此选项用于指定是否将显示消息以及不显示消息时的生成行为。

 **始终生成**不会显示消息框，而是生成项目，而不考虑过期的配置。 于在消息中选择“不再显示此对话框”框，然后选择“是”按钮时，设置此选项。

 **从不生成**不显示消息框，并且不生成项目。 于在消息中选择“不再显示此对话框”框，然后选择“否”按钮时，设置此选项。

 **提示生成**每次项目配置过期时显示消息框。

 **在运行时，当发生生成或部署错误时**如果从 "**生成**" 菜单启动生成时出现生成错误，则会出现一条消息。 您可以指定是否要继续通过启动该应用程序和该消息将显示每次生成错误发生。 此选项用于指定是否将显示消息以及不显示消息时的行为。

> [!NOTE]
> 此选项仅适用于 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 项目。

 **提示启动**每次出现生成错误时显示一个消息框。

 不**启动**不会显示消息框，应用程序也不会启动。 于在消息框中选择“不再显示此对话框”复选框，然后选择“否”按钮时，设置此选项。

 **启动旧版本**不会显示消息框，并且不会启动新构建的应用程序版本。 于在消息框中选择“不再显示此对话框”复选框，然后选择“是”按钮时，设置此选项。

 **对于新解决方案，使用当前选定的项目作为启动项目**如果选中此复选框，则新解决方案将使用当前选定的项目作为启动项目。

 **MSBuild 项目生成输出详细级别**确定在生成的 "**输出**" 窗口中显示的信息量。

 **MSBuild 项目生成日志文件详细信息**
 > [!NOTE]
> 此选项仅适用于 Visual C++ 项目。

 确定写入到生成日志文件中的信息数，该文件位于 \\...\\ProjectName\Debug\\ProjectName.log。

## <a name="see-also"></a>请参阅
 [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)
