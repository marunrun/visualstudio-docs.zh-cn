---
title: 如何：防止 Outlook 显示窗体区域
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: ad17041650324e597fb76925f521bb7fc2e9ce93
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967652"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>如何：防止 Outlook 显示窗体区域
  可能有不希望 Microsoft Office Outlook 显示特定项的窗体区域的情况。 例如，如果联系人项目不包含业务地址，可以防止使其不显示地图中显示的业务位置的窗体区域。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>若要防止 Outlook 显示窗体区域

1. 打开你想要修改的窗体区域代码文件。

2. 展开**窗体区域工厂**代码区域。

3. 将代码添加到`FormRegionInitializing`事件处理程序设置<xref:System.ComponentModel.CancelEventArgs.Cancel%2A>的属性<xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs>类来**true**。

   在此示例中，如果联系人项目不包含地址<xref:System.ComponentModel.CancelEventArgs.Cancel%2A>属性设置为**true**，窗体区域没有显示。

## <a name="example"></a>示例
 [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
 [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

## <a name="see-also"></a>请参阅
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
