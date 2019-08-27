---
title: 源代码管理插件词汇表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f5120a5c6678cac32ef65e08ef7dc34649364cf9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160607"
---
# <a name="source-control-plug-in-glossary"></a>源代码管理插件词汇表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下有用的术语和定义适用于源控制插件 SDK 文档。  
  
## <a name="definitions"></a>定义  
 签入  
 当用户对工作副本的更改时，用户必须将更改从发送到中央源控件存储库的工作副本。 这会创建可供其他用户的文件的新版本。 此过程称为一个签入。  
  
 签出  
 请求从存储库，告知你的意图进行修改的存储库的工作副本的行为。 工作副本将反映截至目前已签出项目的状态。  
  
 客户端  
 使用源代码管理系统的程序。 在本文档中，它是 Visual Studio IDE。  
  
 注释  
 描述执行源代码管理操作时用户可以将附加到某个修订版本的更改的消息。  
  
 冲突  
 如果两个用户尝试签入更改到同一文件的同一区域。 通常情况下，必须执行合并。  
  
 目录  
 客户端的本地文件夹称为一个目录。 这是用户实际进行更改的副本。 可以有多个工作副本的给定项目;通常每个开发人员都有其自己的副本。  
  
 获取  
 Get 操作会使用户的工作副本保持最新的存储库副本。 与不同的签出，用户只是需要的最新副本，但想要不进行任何更改时执行 get。  
  
 历史记录  
 它通常是所有签出、 签入、 更新、 标记和版本在源控件存储库中完成的摘要。  
  
 IDE  
 通常是指在 Visual Studio 集成开发环境。 但是，它还可能引用到其他客户端环境，识别源控制插件 API。  
  
 合并  
 过程期间的两个或多个源的代码文件合并以形成新的文件，其中包含从以前的文件的所有功能。 这一概念是在版本控制中至关重要的其中两个或多个开发人员在文件上同时处理。  
  
 项目  
 源代码管理文件夹通常称为项目。 这在 Visual Studio 中没有与项目或解决方案的任何关系。  
  
 插件  
 通过实现源控件插件 API 提供的源代码管理功能的 DLL。  
  
 存储库  
 其中一个源控制系统的主副本将存储项目的完整修订版本历史记录。 每个项目有且只有一个存储库。  
  
 Revision  
 文件历史记录或一组文件中的已提交的更改。 修订版本是一个不断更改的项目中的快照。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)
