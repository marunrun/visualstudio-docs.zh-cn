---
title: 如何：面向 Office 多语言用户界面
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 5217f2d6cf67eced00c0c84b9bacda94573c5a09
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537496"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>如何：面向 Office 多语言用户界面
  多语言用户界面（MUI）是一项 Microsoft Office 功能，使最终用户能够更改用户界面（UI）的语言。 例如，使用英语 UI 的最终用户可将 UI 的语言更改为西班牙语。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 如果你的应用程序将由使用多种语言的 Office 的人员使用，则可以添加代码以自动更改 UI 字符串的语言，以匹配用户计算机上 Office 使用的语言（如果用户安装了正确的资源）。

## <a name="to-check-the-current-office-ui-setting"></a>检查当前 Office UI 设置

1. 使用 <xref:System.Threading.Thread.CurrentUICulture%2A> 当前线程的属性。 设置您的 UI 字符串的语言以与当前在用户计算机上运行的 Office 版本所使用的语言相匹配。

     [!code-vb[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#10)]
     [!code-csharp[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#10)]

## <a name="see-also"></a>请参阅
- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Office 解决方案中的后期绑定](../vsto/late-binding-in-office-solutions.md)
