---
title: 如何：禁止显示所生成代码的代码分析警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 52caadd7f4dd9349eccb80a366a1458212aba5ca
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646275"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>如何：禁止显示所生成代码的代码分析警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

托管代码编译器通常会生成添加到项目中的代码，以便快速进行代码开发。 此外，开发人员通常使用第三方工具来帮助快速开发应用程序。 这些工具还会生成添加到项目中的代码。

 你可能想要查看代码分析在生成的代码中发现的规则冲突。 但是，如果您无法查看和维护包含冲突的代码，则您可能不希望看到它们。

 通过项目的 "代码分析" 属性页上的 "**禁止显示生成代码的结果**" 复选框，您可以选择是否要查看第三方工具生成的代码的代码分析警告。

> [!NOTE]
> 当窗体和模板中出现错误和警告时，此选项不会禁止显示所生成代码的代码分析错误和警告。 可以查看和维护窗体或模板的源代码。

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>禁止显示项目中生成的代码的警告

1. 右键单击 "解决方案资源管理器中的项目，然后单击"**属性**"。

2. 单击 "**代码分析**"。

3. 选中 "**禁止显示生成的代码结果**" 复选框。
