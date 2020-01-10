---
title: 如何：创建域特定语言解决方案 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
ms.assetid: e585b63b-34d2-405a-8d81-39ea22317975
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f4c5bd99c47517156f1ec89de9da1a163223b99a
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850432"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>如何：创建域特定语言解决方案
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用专用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案创建域特定语言（DSL）。

## <a name="prerequisites"></a>先决条件
 在开始此过程之前，必须先安装这些组件：

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185579](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185580](https://docs.microsoft.com/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|Visual Studio 可视化和建模 SDK|[http://go.microsoft.com/fwlink/?LinkID=185581](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)|

## <a name="creating-a-domain-specific-language-solution"></a>创建域特定语言解决方案

#### <a name="to-create-a-domain-specific-language-solution"></a>创建域特定语言解决方案

1. 启动 DSL 向导。

   1. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

   2. 此时将出现 **“新建项目”** 对话框。

   3. 在 "**项目类型**" 下，展开 "**其他项目类型**" 节点，然后单击 "**扩展性**"。

   4. 单击 "**特定于域的语言设计器**"。

   5. 在 "**名称**" 框中，键入解决方案的名称。 单击" **确定**"。

       此时将显示**特定于域的语言设计器向导**。

      > [!NOTE]
      > 最好键入的名称应为有效的视觉C#标识符，因为它可能用于生成代码。

      ![创建 DSL 对话](../modeling/media/create-dsldialog.png "Create_DSLDialog")

2. 选择 DSL 模板。

    在 "**选择域特定语言选项**" 页面上，选择一个解决方案模板（例如**最小语言**）。 选择类似于要创建的 DSL 的模板。

    有关解决方案模板的详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

3. 在 "**文件扩展名**" 页上输入文件扩展名。 它在您的计算机以及您想要安装 DSL 的任何计算机中都应该是唯一的。 应会看到消息 "**无应用程序或 Visual Studio 编辑器使用此扩展名**"。

   - 如果在以前的实验性 Dsl 中使用了尚未完全安装的文件扩展名，则可以通过使用 "**重置实验实例**" 工具将其清除，可在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK "菜单中找到该工具。

   - 如果计算机上已完全安装了使用此文件扩展名的其他 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展，请考虑将其卸载。 在 "**工具**" 菜单上，单击 "**扩展管理器**"。

4. 检查并根据需要调整向导剩余页面中的字段。 如果对设置感到满意，请单击 "**完成**"。 有关设置的详细信息，请参阅[DSL 设计器向导页面](#settings)。

    向导将创建一个包含两个项目的解决方案，分别名为**Dsl**和**DslPackage**。

   > [!NOTE]
   > 如果你看到一条消息，提示你不从不受信任的源运行文本模板，请单击 **"确定"** 。 您可以将此消息设置为不会再次显示。

## <a name="settings"></a>DSL 设计器向导页
 您可以保留多个字段的默认值不变。 但是，请确保设置了 "文件扩展名" 字段。

### <a name="solution-settings-page"></a>"解决方案设置" 页
 **你要将哪个模板基于域特定语言？**
选择类似于要创建的 DSL 的模板。 不同的模板提供便利的起点。 选择解决方案模板时，向导会显示说明。 有关解决方案模板的详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

 **要如何命名域特定语言？**
默认为解决方案名称。 此值生成代码。 它必须是有效的C#类名。

### <a name="file-extension-page"></a>文件扩展名页
 **使用哪种扩展来建模文件？**
键入新的文件扩展名。

 验证此文件扩展名是否尚未注册以便在此计算机中使用，如下所示：

 查看**已注册的其他工具和应用程序以处理此扩展**。 如果你看到消息 "**无应用程序或 Visual Studio 编辑器使用此扩展**"，则可以使用此文件扩展名。

 如果看到工具或包的列表，应执行以下操作之一：

- 键入不同的文件扩展名。

     \- 或 -

- 重置 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实验实例。 这会取消注册以前生成的所有 Dsl。 在 "**开始**" 菜单上，依次单击 "**所有程序**"、 **Microsoft Visual Studio 2010 SDK**和**工具**"，然后**重置 Microsoft Visual Studio 2010 实验实例**。 你可以重新生成任何其他你想要使用的 Dsl。

     \- 或 -

- 如果计算机上已完全安装了使用此文件扩展名的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展，请将其卸载。 在 "**工具**" 菜单上，单击 "**扩展管理器**"。

### <a name="product-settings-page"></a>"产品设置" 页
 **新的特定于域的语言所属的产品的名称是什么？**
默认为 DSL 名称。

 此值在 Windows 资源管理器（或文件资源管理器）中用于描述具有此文件扩展名的文件。

 **产品所属的公司的名称是什么？**
公司名称。

 此值将合并到 DSL 包的 AssemblyInfo 属性中。

 **此解决方案中项目的根命名空间是什么？**
此名称默认为由公司和产品名称组成的名称。

### <a name="signing-page"></a>签名页
 **创建强名称密钥文件**默认选项是创建新密钥以对 DSL 程序集进行签名。

 **使用现有的强名称密钥**如果要将 DSL 与其他程序集集成，请使用此选项。

 有关强命名的详细信息，请参阅[创建和使用具有强名称的程序集](https://docs.microsoft.com/dotnet/standard/assembly/create-use-strong-named?redirectedfrom=MSDN)。

## <a name="see-also"></a>请参阅
 [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)[特定于域的语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
