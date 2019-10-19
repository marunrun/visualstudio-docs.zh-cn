---
title: 如何：更改域特定语言的命名空间 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, namespace
ms.assetid: f20c47e5-230d-4f0e-812f-5c6edb86866c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8b61b248876f701e9d5286063f28b4f71d73e18b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671724"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>如何：更改域特定语言的命名空间
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以更改域特定语言的命名空间。 必须在**Dsl 资源管理器**、dsl 包项目的属性和程序集信息中进行更改。

### <a name="to-change-the-namespace-of-a-domain-specific-language"></a>更改域特定语言的命名空间

1. 在**Dsl 资源管理器**中，单击**dsl**节点。

2. 在 "**属性**" 窗口中，更改**命名空间**属性。

3. 保存解决方案并转换模板。

4. 在 "**项目**" 菜单上，单击 " **Dsl 属性**"。

     将显示项目的属性。

5. 单击“应用程序” 选项卡。

6. 将 "**默认命名空间**" 属性更改为新的命名空间名称。

7. 如果还想要更改程序集的名称，请更改**程序集名称属性。**

8. 如果更改了程序集名称，请打开 DslPackage\Package.tt 并更新此行：

     `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. 如果已编写任何自定义代码，请确保在代码文件中更改命名空间和类引用。

10. 重置 Visual Studio 实验实例。

    1. 删除 **\Users \\** _{name}_ **\AppData\Local\Microsoft\VisualStudio \\ \*Exp**

    2. 在 Windows "**开始**" 菜单上，选择 "**所有程序**"、 **Microsoft Visual Studio 2010 SDK**、**工具**、"**重置实验实例"** 。

11. 在 "**生成**" 菜单上，选择 "**重新生成解决方案**"。

## <a name="see-also"></a>请参阅
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
