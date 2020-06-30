---
title: 如何：防止 Outlook 显示窗体区域
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], canceling display
- canceling form region display
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 90da255beb0a85a302158feb1f9d5cc4981437eb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520129"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>如何：防止 Outlook 显示窗体区域
  在某些情况下，您可能不希望 Microsoft Office Outlook 显示特定项的窗体区域。 例如，如果某一联系人项不包含业务地址，则可以阻止显示该业务在地图中的位置的窗体区域。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>阻止 Outlook 显示窗体区域

1. 打开要修改的窗体区域的代码文件。

2. 展开**窗体区域工厂**代码区域。

3. 向 `FormRegionInitializing` 事件处理程序添加代码，用于将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 类的属性设置 <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> 为**true**。

   在此示例中，如果联系人项不包含地址，则将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性设置为**true**，并且不会显示窗体区域。

## <a name="example"></a>示例
 [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
 [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

## <a name="see-also"></a>另请参阅
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
