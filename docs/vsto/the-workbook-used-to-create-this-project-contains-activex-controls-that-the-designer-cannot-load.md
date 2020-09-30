---
title: 工作簿包含无法加载的 ActiveX 控件
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: error-reference
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
ms.openlocfilehash: 09182fb354ad3ae8937b66952a0acd376d54fe0a
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584446"
---
# <a name="the-workbook-contains-activex-controls-that-cannot-be-loaded"></a>工作簿包含无法加载的 ActiveX 控件

  当你以编程方式将控件添加到 Word 文档或 Excel 工作表时，将显示错误 "用于创建此项目的工作簿包含 ActiveX 控件"，保存文档或工作簿，然后根据文档或工作簿创建新的文档级解决方案。

 介绍控件托管类型的信息不会随文档或工作簿一起保存。 基于该文档或工作簿创建新的解决方案时，Visual Studio 没有足够的信息来加载主机项设计器中的控件。

## <a name="to-correct-this-error"></a>更正此错误

1. 打开文档或工作簿。

2. 删除在运行时添加的控件。 为此，可以在文档或工作簿中选择它们并按 **Delete** 键。

3. 基于文档或工作簿创建文档级解决方案。

## <a name="see-also"></a>另请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
