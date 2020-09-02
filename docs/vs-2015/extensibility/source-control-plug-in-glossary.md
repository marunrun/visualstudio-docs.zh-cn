---
title: 源代码管理插件术语表 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160607"
---
# <a name="source-control-plug-in-glossary"></a>源代码管理插件词汇表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下有用的术语和定义适用于源代码管理插件 SDK 文档。  
  
## <a name="definitions"></a>定义  
 签入  
 当用户更改工作副本时，用户必须将工作副本中的更改发送到中央源代码管理存储库。 这会创建可供其他用户使用的文件的新修订版本。 此过程称为签入。  
  
 签出  
 从存储库请求工作副本的行为，通知存储库你的意图来修改它。 工作副本反映了项目在签出时的状态。  
  
 客户端  
 使用源代码管理系统的程序。 对于本文档，它是 Visual Studio IDE。  
  
 备注  
 描述用户在执行源代码管理操作时可以附加到修订版本的更改的消息。  
  
 冲突  
 当两个用户尝试将更改签入到同一文件的同一区域时，会出现这种情况。 通常，必须执行合并。  
  
 Directory  
 客户端本地文件夹称为目录。 这是用户实际进行更改的副本。 给定项目可以有许多工作副本;通常，每个开发人员都有自己的副本。  
  
 获取  
 Get 操作使用户的工作副本与存储库副本保持最新。 与结帐不同，当用户只需使用最新副本但不进行任何更改时，就会执行 get。  
  
 历史记录  
 它通常是在源代码管理存储库中完成的所有签出、签入、更新、标记和发布的汇总。  
  
 IDE  
 通常指 Visual Studio 集成开发环境。 不过，它也可以引用其他识别源代码管理插件 API 的客户端环境。  
  
 合并  
 在此过程中，将两个或多个源代码文件组合在一起形成一个新文件，该文件包含以前文件中的所有功能。 在两个或多个开发人员同时处理文件的版本控制中，此概念至关重要。  
  
 Project  
 源代码管理文件夹通常称为 "项目"。 这与 Visual Studio 中的项目或解决方案没有任何关系。  
  
 插件  
 一个 DLL，它通过实现源代码管理插件 API 提供源代码管理功能。  
  
 存储库  
 源代码管理系统存储项目完整修订历史记录的主副本。 每个项目都有一个存储库。  
  
 修订  
 文件或文件集的历史记录中的已提交更改。 修订是不断变化的项目中的一个快照。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)
