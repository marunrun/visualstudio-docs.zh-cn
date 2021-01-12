---
title: Visual Studio 打开文件夹扩展性概述 | Microsoft Docs
description: 了解“打开文件夹”功能的扩展性，通过此功能，用户可在 Visual Studio 中打开代码库，而无需项目或解决方案文件。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: overview
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 81ca62c834e09d542016ffce607abf3c32cf2a61
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863742"
---
# <a name="open-folder-extensibility"></a>打开文件夹扩展性

通过[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)功能，用户可在 Visual Studio 中打开任何代码库，而无需项目或解决方案文件。 打开文件夹提供用户期望从 Visual Studio 获得的功能，例如：

* “解决方案资源管理器”集成和搜索
* “编辑器”着色
* “转至”导航
* “在文件中查找”搜索

当与工作负载（如对于 .NET 和 C++ 开发）一起使用时，用户还会获得：

* 丰富的 IntelliSense
* 语言特定功能

使用打开文件夹功能，扩展插件作者可为任何语言创建丰富的功能。 支持使用 API 生成和调试用户代码库，并在代码库包含的任何文件中进行符号搜索。 当前扩展程序可以更新其现有的 Visual Studio 功能，以了解代码，而无需项目或解决方案的支持。

## <a name="an-api-without-project-systems"></a>无需项目系统的 API

过去，Visual Studio 仅通过项目系统了解解决方案及其项目中的文件。 项目系统负责加载项目的功能和用户交互。 它了解项目包含的文件、项目内容的直观表示、对其他项目的依赖以及基础项目文件的修改。 正是通过这些层次结构和功能，其他组件可代表用户工作。 并非所有代码库都可以在项目和解决方案结构中很好地表示。 通过适用于 Linux 的 C++ 编写的脚本语言和开放源代码就是很好的例子。 使用打开文件夹功能，Visual Studio 为用户提供了新的源代码交互方式。

打开文件夹 API 位于 `Microsoft.VisualStudio.Workspace.*` 命名空间下，可供扩展程序在打开文件夹的功能范围内围绕文件生成及使用数据或操作。 扩展可以使用这些 API 为许多领域提供功能，包括：

- [工作区](workspaces.md) - 打开文件夹扩展性的起点是工作区及其 API。
- [文件上下文和操作](workspace-file-contexts.md) - 通过文件上下文提供的文件特定代码智能。
- [索引](workspace-indexing.md) - 收集和保留有关打开文件夹工作区的数据。
- [语言服务](workspace-language-services.md) - 将语言服务集成到打开文件夹工作区中。
- [生成](workspace-build.md) - 生成对打开文件夹工作区的支持。

使用以下类型的功能将需要采用新的 API 来支持打开文件夹：

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>反馈、意见、问题

打开文件夹和 `Microsoft.VisualStudio.Workspace.*` API 处于积极开发阶段。 如果你发现意外行为，请查看相关版本的已知问题。 建议在[开发者社区](https://aka.ms/feedback/suggest?space=8)中进行投票和创建任何问题。 对于每个反馈，我们强烈建议你提供详细的问题描述。 包括你正在开发的 Visual Studio 版本、正在使用的 API（已实现的 API 和正在交互的 API）、预期结果和实际结果。 如果可能，请包括 devenv.exe 进程的转储。 使用 GitHub 的问题跟踪提供有关此文档和相关文档的反馈。

## <a name="next-steps"></a>后续步骤

* [工作区](workspaces.md) - 了解打开文件夹工作区 API。