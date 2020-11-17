---
title: XML 文本与 XML 架构资源管理器的集成
description: 了解如何在 Visual Studio 中使用 XML 架构资源管理器中的 XML 文本支持，将 XML 片段直接集成到 Visual Basic 代码中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 57a29998-c6e8-48ac-bdb0-5788e73f9164
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 059263f06421fee3c90f2471df4c8b2c7bf8fc86
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93398496"
---
# <a name="integration-of-xml-literals-with-xml-schema-explorer"></a>XML 文本与 XML 架构资源管理器的集成

Visual Basic 支持 XML 文本，这表示可以将 XML 代码片断直接合并到 Visual Basic 代码中。 有关详细信息，请参阅 [XML 文本概述](/dotnet/visual-basic/programming-guide/language-features/xml/xml-literals-overview)。

## <a name="how-to"></a>如何

如果 Visual Basic 项目中的 XSD 文件包括一个 XML 文本，则可以在 XML 架构资源管理器中查看 XML 架构集。 若要查看与 XML 文本关联的架构集，请右键单击 XML 文本或 XML 命名空间导入中的 XML 节点，然后选择“在架构资源管理器中显示”。

![Visual Basic 项目窗口的屏幕截图，显示 XML 节点上的上下文菜单，其中突出显示了“在架构资源管理器中显示”命令。](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer1.gif)

此操作将并排打开 XML 架构资源管理器和 Visual Basic 文件。

![Visual Basic 项目窗口的屏幕截图，显示 XML 架构资源管理器和解决方案资源管理器已在右窗格中打开 。](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer2.gif)

## <a name="see-also"></a>请参阅

- [如何：将 XML 架构设计器用于 XML 文本](../xml-tools/how-to-use-the-xml-schema-designer-with-xml-literals.md)
