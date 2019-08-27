---
title: 如何：面向 Office 多语言用户界面
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], user interface targeting
- MUI [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], localization
- Multilingual User Interface [Office development in Visual Studio]
- localization [Office development in Visual Studio], user interface targeting
- Office applications [Office development in Visual Studio], globalization
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c495f8a83b58c53404056befd2227b295c3324d5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961134"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>如何：面向 Office 多语言用户界面
  多语言用户界面 (MUI) 是 Microsoft Office 功能，使最终用户能够更改用户界面 (UI) 的语言。 例如，最终用户使用英语 UI，可以将 UI 的语言更改为西班牙语。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 如果你的应用程序将由使用的 Office 的许多语言的用户，可以添加代码以自动更改 UI 字符串以匹配 Office 所使用的用户的计算机上 （如果用户具有安装了正确的资源） 的语言的语言。

## <a name="to-check-the-current-office-ui-setting"></a>若要检查当前的 Office 用户界面设置

1. 使用<xref:System.Threading.Thread.CurrentUICulture%2A>当前线程的属性。 UI 字符串的当前用户的计算机运行的 Office 版本所用语言相匹配的语言设置。

     [!code-vb[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#10)]
     [!code-csharp[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#10)]

## <a name="see-also"></a>请参阅
- [如何：通过主互操作程序集的目标 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [在 Office 解决方案中的后期绑定](../vsto/late-binding-in-office-solutions.md)
