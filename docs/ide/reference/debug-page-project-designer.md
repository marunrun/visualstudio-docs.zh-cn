---
title: “项目设计器”->“调试”页
ms.date: 06/27/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesDebug
helpviewer_keywords:
- Project Designer, Debug page
- Debug page in Project Designer
ms.assetid: ef11eae9-df96-4e20-aabd-2678ba317140
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 406b3ecdc0e4e3f0d45c22fc9201bd37c6031152
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418738"
---
# <a name="debug-page-project-designer"></a>“项目设计器”->“调试”页

使用项目设计器的“调试”页为 Visual Basic 或 C# 项目中的调试行为设置属性 。

要访问“调试”页，请在解决方案资源管理器中选择项目节点 。 在“项目”菜单上，选择“\<ProjectName> 属性” 。 当项目设计器出现时，请单击“调试”选项卡 。

> [!NOTE]
> 本主题不适用于 UWP 应用。 有关 UWP 应用，请参阅[启动调试会话 (VB、C#、C++ 和 XAML)](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)。

## <a name="configuration-and-platform"></a>配置和平台

通过以下选项，可选择要显示或修改的配置和平台。

**配置**

指定要显示或修改的配置设置。 设置可以为“调试”（默认）、“发布”或“所有配置”  。

**平台**

指定要显示或修改的平台设置。 这些选择包括“任何 CPU”（默认）、“x64”和“x86”  。

## <a name="start-action"></a>启动操作

“启动操作”指示应用程序调试时要启动的项：项目、自定义程序、URL 或不启动任何项。 默认情况下，此选项设置为“启动项目”。 “调试”页上的“启动操作”设置确定 `StartAction` 属性的值 。

**启动项目**

选择此选项可指定调试应用程序时应启动（适用于 Windows 应用程序和控制台应用程序项目的）可执行文件。 默认情况下选择此选项。

**启动外部程序**

选择此选项可指定调试应用程序时应启动特定程序。

**使用 URL 启动浏览器**

选择此选项可指定调试应用程序时应访问特定 URL。

## <a name="start-options"></a>启动选项

**命令行参数**

在此文本框中，输入用于调试的命令行参数。

**工作目录**

在此文本框中，输入将从其中启动项目的目录。 或单击“浏览”按钮 (...) 选择目录。

**使用远程计算机**

要从远程计算机调试应用程序，请选中此复选框，然后在文本框中输入该远程计算机的路径。

## <a name="debugger-engines"></a>调试程序引擎

**启用本机代码调试**

该选项指定是否支持本机代码调试。 如果正在调用 COM 对象或启动以调用项目的本机代码编写的自定义程序，请选中此复选框并且必须调试此本机代码。 清除此复选框可禁用非托管代码调试。 默认情况下清除此复选框。

**启用 SQL Server 调试**

选中或清除此复选框，从 Visual Basic 应用程序启用或禁用 SQL 过程调试。 默认情况下清除此复选框。

## <a name="see-also"></a>请参阅

- [初探调试器](../../debugger/debugger-feature-tour.md)
- [C# 调试配置的项目设置](../../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic 调试配置的项目设置](../../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [保护 ClickOnce 应用](../../deployment/securing-clickonce-applications.md)
- [如何：创建和编辑配置](../../ide/how-to-create-and-edit-configurations.md)
