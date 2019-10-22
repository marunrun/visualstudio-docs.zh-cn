---
title: “选项”对话框 ->“项目”->“Visual Basic 默认值” | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.VBDefaults
helpviewer_keywords:
- Option Explicit statement, setting in the IDE
- Option Compare statement, setting in the IDE
- Option Strict statement, setting in the IDE
ms.assetid: 2465cd9d-18b6-4c4a-b1ea-86dbab23fc79
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f08cc817fab6e81ae1160462c9b6d1221ca41160
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657876"
---
# <a name="visual-basic-defaults-projects-options-dialog-box"></a>“选项”对话框 ->“项目”->“Visual Basic 默认值”
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定 Visual Basic 项目选项的默认设置。 创建新项目时，指定选项语句会添加到代码编辑器的项目标头中。 选项应用于所有 Visual Basic 项目。

 若要访问此对话框，在“工具”菜单上，单击“选项”，展开“项目和解决方案”文件夹，单击“VB 默认值”     。

 **Option Explicit**设置编译器默认值，以便需要显式声明变量。 默认情况下，“Option Explicit”设置为“On”   。 有关详细信息，请参阅 [/optionexplicit](https://msdn.microsoft.com/library/5d296ab3-bafe-4c4d-9887-78f162ed86c7)。

 **Option Strict**设置编译器默认值，以便需要显式收缩转换，并且不允许后期绑定。 默认情况下，“Option Strict”设置为“Off”   。 有关详细信息，请参见 [/optionstrict](https://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da)。

 **选项比较**为字符串比较设置编译器默认值：二进制（区分大小写）或文本（不区分大小写）。默认情况下，“Option Compare”设置为“二进制”  。 有关详细信息，请参阅 [/optioncompare](https://msdn.microsoft.com/library/7237b766-b44d-4cc5-9a3c-885348a7d9e4)。

 **选项推断**设置本地类型推理的编译器默认值。 默认情况下，新创建的项目的“Option Infer”设置为“On”，在 Visual Basic 以前版本中创建的迁移项目的“Option Infer”设置为“Off”    。 有关详细信息，请参阅 [/optioninfer](https://msdn.microsoft.com/library/f6c09db1-0553-464a-abe3-d4510c61d6ed)。

## <a name="see-also"></a>另请参阅
 [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)
