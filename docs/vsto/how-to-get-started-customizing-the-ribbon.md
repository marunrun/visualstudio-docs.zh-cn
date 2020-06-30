---
title: 如何：开始自定义功能区
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, adding Ribbon to project
- Ribbon [Office development in Visual Studio], adding
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, adding Ribbon to project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: be311f87862f4447d903294508927735d3507b08
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520063"
---
# <a name="how-to-get-started-customizing-the-ribbon"></a>如何：开始自定义功能区
  若要自定义 Microsoft Office 应用程序的功能区，请向 Office 项目添加**功能区（可视化设计器）** 或**功能区（XML）** 项。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-ribbon-to-a-project"></a>向项目添加功能区

1. 在 "**项目**" 菜单上，单击 "**添加新项**"。

2. 在 "**添加新项**" 对话框中，选择 "**功能区（可视化设计器）** 或**功能区（XML）**"。 有关这些模板的详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

3. 在 "**名称**" 框中，键入功能区项的名称。

    名称不能包含下列字符：

   - 井号 (#)

   - 百分号 (%)

   - 与符号 (&)

   - 星号 (*)

   - 竖线 (|)

   - 反斜杠 (\\)

   - 冒号 (:)

   - 双引号 (")

   - 小于号 (\<)

   - 大于号 (>)

   - 问号 (?)

   - 正斜杠 (/)

   - 前导空格或尾随空格 (' ')

   - 为 Windows 或 DOS 保留的名称，如（"nul"、"aux"、"con"、"com1"、"lpt1" 等）

4. 单击“确定”。

   功能区项显示在**解决方案资源管理器**中。 有关后续步骤的信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

## <a name="see-also"></a>另请参阅
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
