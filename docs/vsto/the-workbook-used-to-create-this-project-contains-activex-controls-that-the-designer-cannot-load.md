---
title: 用于创建此项目的工作簿包含设计器无法加载的 ActiveX 控件
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.SelectDocWizard.ContainsActiveXControls
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 27feb1c6a85740d8a9287ce3a2a47800595e178a
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253775"
---
# <a name="the-workbook-used-to-create-this-project-contains-activex-controls-that-the-designer-cannot-load"></a>用于创建此项目的工作簿包含设计器无法加载的 ActiveX 控件
  以编程方式向 Word 文档或 Excel 工作表添加控件时出现此错误，请保存文档或工作簿，然后基于文档或工作簿创建新的文档级解决方案。

 介绍控件托管类型的信息不会随文档或工作簿一起保存。 基于该文档或工作簿创建新的解决方案时，Visual Studio 没有足够的信息来加载主机项设计器中的控件。

## <a name="to-correct-this-error"></a>更正此错误

1. 打开文档或工作簿。

2. 删除在运行时添加的控件。 为此，可以在文档或工作簿中选择它们并按**Delete**键。

3. 基于文档或工作簿创建文档级解决方案。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
