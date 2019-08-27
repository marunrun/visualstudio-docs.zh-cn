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
ms.openlocfilehash: 0087841e7f37d49da40817e1487b8529af1f87df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978922"
---
# <a name="the-workbook-used-to-create-this-project-contains-activex-controls-that-the-designer-cannot-load"></a>用于创建此项目的工作簿包含设计器无法加载的 ActiveX 控件
  以编程方式向 Word 文档或 Excel 工作表添加控件时出现此错误，请保存文档或工作簿，然后基于文档或工作簿创建新的文档级解决方案。

 介绍控件托管类型的信息不会随文档或工作簿一起保存。 基于该文档或工作簿创建新的解决方案时，Visual Studio 没有足够的信息来加载主机项设计器中的控件。

## <a name="to-correct-this-error"></a>更正此错误

1. 打开文档或工作簿。

2. 删除已在运行时添加的控件。 您可以执行此操作通过在文档或工作簿以及按将其选中**删除**密钥。

3. 基于文档或工作簿创建文档级解决方案。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
