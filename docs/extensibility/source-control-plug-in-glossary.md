---
title: 源代码管理插件词汇表 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 47488621fe3e5167e00442e1ca971ef923d9b25c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331899"
---
# <a name="source-control-plug-in-glossary"></a>源代码管理插件词汇表
以下有用的术语和定义适用于源控制插件 SDK 文档。

## <a name="definitions"></a>定义
 签入到工作副本的用户进行更改时，用户必须将更改从发送到中央源控件存储库的工作副本。 这会创建可供其他用户的文件的新版本。 此过程称为一个签入。

 签出工作副本请求从存储库，告知你的意图进行修改的存储库的操作。 工作副本将反映截至目前已签出项目的状态。

 使用源代码管理系统的客户端的程序。 在本文档中，它是 Visual Studio IDE。

 描述执行源代码管理操作时用户可以将附加到某个修订版本的更改的注释的消息。

 冲突的情况下，当两个用户尝试签入更改到同一文件的同一区域。 通常情况下，必须执行合并。

 目录的客户端的本地文件夹称为一个目录。 这是用户实际进行更改的副本。 可以有多个工作副本的给定项目;通常每个开发人员都有其自己的副本。

 获取一个 get 操作会使用户的工作副本保持最新的存储库副本。 与不同的签出，用户只是需要的最新副本，但想要不进行任何更改时执行 get。

 历史记录它通常是所有签出、 签入、 更新、 标记和版本在源控件存储库中完成的摘要。

 IDE 通常是指在 Visual Studio 集成开发环境。 但是，它还可能引用到其他客户端环境，识别源控制插件 API。

 合并两个或多个源代码文件合并以形成新的文件，其中包含从以前的文件的所有功能的过程。 这一概念是在版本控制中至关重要的其中两个或多个开发人员在文件上同时处理。

 项目的源代码管理文件夹通常称为项目。 这在 Visual Studio 中没有与项目或解决方案的任何关系。

 通过实现源控件插件 API 提供的源代码管理功能的插件的 DLL。

 源代码管理系统存储项目的完整修订版本历史记录的位置存储库的主副本。 每个项目有且只有一个存储库。

 修订的提交中的文件历史记录或一组文件的行为更改。 修订版本是一个不断更改的项目中的快照。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)