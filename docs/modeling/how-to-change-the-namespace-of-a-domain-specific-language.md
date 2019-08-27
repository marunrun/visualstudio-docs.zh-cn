---
title: 如何：更改域特定语言的命名空间
ms.date: 10/31/2018
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, namespace
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 16fec4cf6150fe0711812d9fabe57fc667e36eef
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993493"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>如何：更改域特定语言的命名空间

您可以更改域特定语言的命名空间。 进行中的更改**DSL 资源管理器**、 Dsl 包项目的属性和程序集信息。

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>若要更改域特定语言的命名空间

1. 在中**DSL 资源管理器**，选择**Dsl**节点。

2. 在中**属性**窗口中，更改**Namespace**属性。

3. 保存解决方案和转换模板。

4. 上**项目**菜单中，选择**Dsl 属性**。

   为你的项目属性将显示。

5. 选择**应用程序**选项卡。

6. 更改**默认命名空间**属性设置为新的命名空间名称。

7. 如果还想要更改的程序集名称，更改**程序集名称属性。**

8. 如果已更改的程序集名称，打开 DslPackage\Package.tt 并更新此行：

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. 如果您编写任何自定义代码，请确保更改在代码文件中引用的命名空间和类。

10. 重置 Visual Studio 实验实例。

    1. 删除 **\Users\\** _{名称}_ **\AppData\Local\Microsoft\VisualStudio\\\*Exp** 。

    2. 在 Windows 上**启动**菜单中，选择**所有程序** > **Microsoft Visual Studio 2010 SDK** > **工具**  > **重置实验实例**。

11. 上**构建**菜单中，选择**重新生成解决方案**。

## <a name="see-also"></a>请参阅

[域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)