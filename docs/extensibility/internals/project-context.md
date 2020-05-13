---
title: 项目上下文 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51e411f0bca361f96cdffcfd89498908fd21d441
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706589"
---
# <a name="project-context"></a>项目上下文
当用户添加或使用项目和项目项时，IDE 将使用项目上下文的概念来确定如何执行各种操作。

 通常，文件是用户通过选择 **"新项目"** 命令或通过在 **"文件**"菜单上选择 **"打开项目"** 命令而显式创建的标准项目对象。 在这些情况下，在项目的上下文中创建和打开文件，项目类型定义用于编辑文档的上下文。

 有些项目提供了非常丰富的上下文。 例如，项目管理用于数据绑定的项目范围、编程命名空间或项目范围数据库连接。 用户经常使用特定的项目对象（如解决方案资源管理器中显示的项目项）直接打开文件或数据库连接。

 在其他情况下，未显式指定项的项目上下文。 例如，当用户通过在 **"文件"** 菜单上选择 **"打开现有文件"** 命令、调试器对文件进行操作或在 **"查找和替换**"对话框中单击"**查找文件"** 命令来打开文件时，项的上下文不可用。 为了处理这些情况，IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>以管理查找打开文档的最佳项目的过程。

## <a name="see-also"></a>请参阅
- [项目优先级](../../extensibility/internals/project-priority.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
