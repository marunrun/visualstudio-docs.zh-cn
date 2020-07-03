---
title: Visual Studio 打开文件夹扩展性概述 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: overview
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: d213a7add358c46f7088f504d8c54352cda44a1c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905970"
---
# <a name="open-folder-extensibility"></a>打开文件夹扩展性

通过 "[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)" 功能，用户可在 Visual Studio 中打开任何基本代码，而无需项目或解决方案文件。 "打开文件夹" 提供用户期望的 Visual Studio 功能，例如：

* 解决方案资源管理器集成和搜索
* 编辑器着色
* 定位到导航
* 在文件中查找搜索

当用于 .NET 和 c + + 开发等工作负荷时，用户还会获得：

* 丰富的 Intellisense
* 语言特定的功能

对于 "打开文件夹"，扩展创作者可以为任何语言创建丰富的功能。 存在 Api，可支持对用户的基本代码中的任何文件进行生成、调试和符号搜索。 当前扩展器可以更新其现有的 Visual Studio 功能，以了解不支持项目或解决方案的代码。

## <a name="an-api-without-project-systems"></a>无项目系统的 API

从历史上看，Visual Studio 只使用项目系统来理解解决方案及其项目中的文件。 项目系统负责加载的项目的功能和用户交互。 它了解项目包含的文件、项目内容的可视化表示形式、其他项目的依赖项以及基础项目文件的修改。 它通过这些层次结构和功能，其他组件可代表用户进行操作。 并非所有基本代码在项目和解决方案结构中都有很好的表示形式。 用 c + + 编写的脚本语言和开源代码都是很好的例子。 使用打开的文件夹，Visual Studio 为用户提供了与其源代码交互的新方式。

打开的文件夹 Api 位于 `Microsoft.VisualStudio.Workspace.*` 命名空间下，并且可供扩展程序在打开的文件夹中生成和使用有关文件的数据或操作。 扩展可以使用这些 Api 为多个领域提供功能，包括：

- [工作区](workspaces.md)-打开文件夹扩展性的起点是工作区及其 api。
- [文件上下文和操作](workspace-file-contexts.md)-文件上下文中提供的特定于文件的代码智能。
- [索引](workspace-indexing.md)-收集和保存有关打开的文件夹工作区的数据。
- [语言服务](workspace-language-services.md)-将语言服务集成到打开的文件夹工作区中。
- 对打开文件夹工作区的[生成](workspace-build.md)-生成支持。

使用以下类型的功能需要采用新的 Api 来支持打开文件夹：

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>反馈、评论、问题

打开文件夹， `Microsoft.VisualStudio.Workspace.*` api 处于积极开发阶段。 如果出现意外行为，请查看相关发行版的已知问题。 建议使用[开发人员社区](https://developercommunity.visualstudio.com)来投票和创建任何问题。 对于每个反馈，我们强烈建议您对问题进行详细说明。 包括你开发的 Visual Studio 版本、所使用的 Api （既是实现的，也包括你要与之交互的内容）、预期结果和实际结果。 如果可能，请包含 devenv.exe 进程的转储。 使用 GitHub 的问题跟踪提供有关此文档和相关文档的反馈。

## <a name="next-steps"></a>后续步骤

* [工作区](workspaces.md)-了解打开文件夹工作区 API。