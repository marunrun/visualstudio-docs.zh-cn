---
title: 源代码管理插件术语表 |Microsoft Docs
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
ms.openlocfilehash: 672a96c31137a52f3bd4a8c826cef1b19406790b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72719584"
---
# <a name="source-control-plug-in-glossary"></a>源代码管理插件词汇表
以下有用的术语和定义适用于源代码管理插件 SDK 文档。

## <a name="definitions"></a>定义
 签入用户更改工作副本后，用户必须从工作副本将更改发送到中央源代码管理存储库。 这会创建可供其他用户使用的文件的新修订版本。 此过程称为签入。

 从存储库中签出请求工作副本的行为，并通知存储库你打算修改它。 工作副本反映了项目在签出时的状态。

 使用源代码管理系统的客户端程序。 对于本文档，它是 Visual Studio IDE。

 注释一条消息，该消息描述当执行源代码管理操作时用户可以附加到修订版本的更改。

 当两个用户尝试将更改签入到同一文件的同一区域时，会发生冲突。 通常，必须执行合并。

 目录：客户端本地文件夹称为目录。 这是用户实际进行更改的副本。 给定项目可以有许多工作副本;通常，每个开发人员都有自己的副本。

 Get 操作使用户的工作副本与存储库副本保持最新。 与结帐不同，当用户只需使用最新副本但不进行任何更改时，就会执行 get。

 历史记录通常是在源代码管理存储库中完成的所有签出、签入、更新、标记和发布的汇总。

 IDE 通常是指 Visual Studio 集成开发环境。 不过，它也可以引用其他识别源代码管理插件 API 的客户端环境。

 合并两个或更多个源代码文件组合起来以形成一个新文件，该文件包含以前文件中的所有功能。 在两个或多个开发人员同时处理文件的版本控制中，此概念至关重要。

 项目一个源代码管理文件夹通常称为 "项目"。 这与 Visual Studio 中的项目或解决方案没有任何关系。

 插件通过实现源代码管理插件 API 提供源代码管理功能的 DLL。

 存储库：源代码管理系统用于存储项目完整修订历史记录的主副本。 每个项目都有一个存储库。

 修订一个文件或一组文件的历史记录中的已提交更改。 修订是不断变化的项目中的一个快照。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)