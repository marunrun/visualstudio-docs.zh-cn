---
title: 源代码管理插件词汇表 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3835561eb63fa2a4a71174732c07ecd73f1df5d7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699909"
---
# <a name="source-control-plug-in-glossary"></a>源代码管理插件词汇表
以下有用的术语和定义与源代码管理插件 SDK 文档相关。

## <a name="definitions"></a>定义
 签入 当用户对工作副本进行更改时，用户必须将更改从工作副本发送到中央源代码管理存储库。 这将创建可供其他用户使用的文件的新修订版。 此过程称为签入。

 签出从存储库请求工作副本的行为，通知存储库您修改该副本的意图。 工作副本反映项目签出时的状态。

 客户端 使用源代码控制系统的程序。 对于本文档，它是可视化工作室 IDE。

 注释 描述执行源代码管理操作时用户可以附加到修订版更改的消息。

 冲突两个用户尝试签入对同一文件的同一区域的更改的情况。 通常，必须执行合并。

 目录 客户端本地文件夹称为目录。 这是用户实际进行更改的副本。 给定项目可以有许多工作副本;通常每个开发人员都有自己的副本。

 Get get 操作使用户的工作副本与存储库副本一起更新。 与结帐不同，当用户只需要最新副本但不打算进行任何更改时，将执行 get。

 历史记录 它通常是在源代码管理存储库中完成的所有签出、签入、更新、标记和版本的摘要。

 IDE 通常是指可视化工作室集成开发环境。 但是，它还可以引用其他客户端环境来识别源代码管理插件 API。

 合并将两个或多个源代码文件组合以形成包含以前文件的所有功能的新文件的过程。 在两个或多个开发人员同时处理文件的版本控制中，这个概念至关重要。

 项目 源控制文件夹通常称为项目。 这与 Visual Studio 中的项目或解决方案没有任何关系。

 插件 DLL 通过实现源代码管理插件 API 提供源代码管理功能。

 存储库 源控制系统存储项目的完整修订历史记录的主副本。 每个项目都有一个存储库。

 修订 文件或文件集的历史记录中已提交的更改。 修订是不断更改的项目中的一个快照。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
