---
title: Visual Studio 打开文件夹扩展性概述 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 2bb74703f639848d643f536edf620e30b1836310
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806436"
---
# <a name="open-folder-extensibility"></a>打开文件夹可扩展性

[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)功能允许用户打开任何基本代码在 Visual Studio 中而无需项目或解决方案文件。 打开文件夹提供了功能用户期望从 Visual Studio 如：

* 解决方案资源管理器集成和搜索
* 编辑器颜色设置
* 转到导航
* 文件搜索中找到

与一起使用时的工作负荷此类与.NET 和C++开发，用户可获得：

* 丰富的 Intellisense
* 特定于语言的功能

使用打开的文件夹，扩展作者可以创建用于任何语言的丰富功能。 有 Api 针对用户中的任何文件的基本代码的支持构建、 调试和符号搜索。 当前的扩展程序可以更新其现有的 Visual Studio 功能，以了解代码而无需项目或解决方案的支持。

## <a name="an-api-without-project-systems"></a>API 而无需项目系统

从历史上看，Visual Studio 仅了解一种解决方案和项目使用项目系统中的文件。 项目系统负责加载的项目的功能和用户交互。 它知道哪些文件及其项目包含项目内容，在其他项目的依赖关系的可视表示形式，并且基础修改项目文件。 正是通过这些层次结构和其他组件代表用户执行工作的功能。 并非所有代码库中的项目和解决方案的结构很好的体现。 脚本编写语言和开放源代码代码编写的C++适用于 Linux 是很好示例。 打开文件夹时，Visual Studio 允许用户使用其源代码进行交互的新方法。

打开文件夹 Api 是下`Microsoft.VisualStudio.Workspace.*`命名空间和可用的扩展程序来生成和使用数据或周围打开文件夹中的文件的操作。 扩展可以使用这些 Api 提供了许多领域，包括功能：

- [工作区](workspaces.md)-启动点的打开文件夹扩展是在工作区和其 Api。
- [文件上下文和操作](workspace-file-contexts.md)-文件通过文件上下文提供的特定代码智能。
- [索引](workspace-indexing.md)-收集并保存有关工作区打开的文件夹的数据。
- [语言服务](workspace-language-services.md)-将语言服务集成到工作区打开的文件夹。
- [生成](workspace-build.md)-生成对打开的文件夹的工作区的支持。

使用以下类型的功能将需要采用新的 Api 来支持打开文件夹：

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>反馈、 意见问题

打开文件夹和`Microsoft.VisualStudio.Workspace.*`Api 是处于积极开发阶段。 如果您看到意外的行为，请参阅感兴趣的版本的已知的问题。 [开发人员社区](https://developercommunity.visualstudio.com)提出建议，以及创建的任何问题的建议位置。 有关每个反馈，我们强烈建议你的问题的详细的说明。 包括您在开发的 Visual Studio 版本、 使用 （已实现和与正在进行的交互） 的 Api、 的预期的结果和实际结果。 如果可能，包括 devenv.exe 进程的转储。 使用 GitHub 的问题跟踪有关对此提供反馈和相关文档。

## <a name="next-steps"></a>后续步骤

* [工作区](workspaces.md)-了解有关 API 的打开文件夹工作区的信息。