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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: eae08b771f3bd5748485f9029f7f12725df6f28f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698126"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>如何：创建域特定语言解决方案
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用一个专用创建域特定语言 (DSL)[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]解决方案。  
  
## <a name="prerequisites"></a>系统必备  
 在开始此过程之前，必须首先安装这些组件：  
  
|||  
|-|-|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185579](http://go.microsoft.com/fwlink/?LinkID=185579)|  
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185580](http://go.microsoft.com/fwlink/?LinkID=185580)|  
|Visual Studio 可视化和建模 SDK|[http://go.microsoft.com/fwlink/?LinkID=185581](http://go.microsoft.com/fwlink/?LinkID=185581)|  
  
## <a name="creating-a-domain-specific-language-solution"></a>创建域特定语言解决方案  
  
#### <a name="to-create-a-domain-specific-language-solution"></a>若要创建域特定语言解决方案  
  
1. 启动 DSL 向导。  
  
   1. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
   2. 此时将出现“新建项目”对话框。  
  
   3. 下**项目类型**，展开**其他项目类型**节点，然后单击**扩展性**。  
  
   4. 单击**域特定语言设计器**。  
  
   5. 在中**名称**框中，键入解决方案的名称。 单击 **“确定”**。  
  
       **域特定语言设计器向导**出现。  
  
      > [!NOTE]
      > 最好是您键入的名称应是有效的 Visual C# 标识符，因为它可能用于生成代码。  
  
      ![创建 DSL 对话框](../modeling/media/create-dsldialog.png "Create_DSLDialog")  
  
2. 选择一个 DSL 模板。  
  
    上**选择特定于域的语言选项**页上，选择其中一个解决方案模板例如**最小语言**。 选择模板类似于你想要创建 DSL。  
  
    有关解决方案模板的详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。  
  
3. 输入文件扩展名**文件扩展名**页。 它应该是唯一在您的计算机，并想要安装 DSL 在其上的任何计算机。 你应看到消息**没有应用程序或 Visual Studio 编辑器使用此扩展**。  
  
   - 如果您曾经用尚未完全安装的上一个实验性 Dsl 的文件扩展名，则可以清除它们出通过使用**重置实验实例**工具，可在[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]SDK 菜单。  
  
   - 如果另一个[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展使用此文件扩展名的完全安装在计算机上，请考虑卸载它。 上**工具**菜单上，单击**扩展管理器**。  
  
4. 检查，并根据需要调整，其余向导页中的字段。 设置感到满意，单击**完成**。 有关设置的详细信息，请参阅[DSL 设计器向导页](#settings)。  
  
    该向导创建的解决方案，有两个项目，分别名为**Dsl**并**DslPackage**。  
  
   > [!NOTE]
   > 如果你看到一条消息，提醒你不运行来自不受信任源的文本模板中，单击**确定**。 您可以设置不会再次出现此消息。  
  
## <a name="settings"></a> DSL 设计器向导页  
 可将多个字段从其默认值保持不变。 但是，请确保将文件扩展名字段设置。  
  
### <a name="solution-settings-page"></a>解决方案设置页  
 **要使你的域特定语言基于哪个模板？**  
 选择模板类似于你想要创建 DSL。 不同的模板提供方便的起点。 当你选择的解决方案模板时，向导将显示说明。 有关解决方案模板的详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。  
  
 **你想要命名特定于域的语言？**  
 默认值为解决方案名称。 此值中生成代码。 它必须是作为 C# 类名无效。  
  
### <a name="file-extension-page"></a>文件扩展名页  
 **哪些扩展应模型文件使用？**  
 键入新的文件扩展名。  
  
 验证，此文件扩展名不已注册以便在此计算机中使用，如下所示：  
  
 下查找**其他工具和应用程序注册为处理此扩展名**。 如果您看到的消息**没有应用程序或 Visual Studio 编辑器使用此扩展**，则可以使用此文件扩展名。  
  
 如果看到一系列工具或包，应执行下列任一操作：  
  
- 键入不同的文件扩展名。  
  
     \- 或 -  
  
- 重置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]实验实例。 这将取消注册所有以前生成的 Dsl。 上**启动**菜单上，单击**所有程序**， **Microsoft Visual Studio 2010 SDK**，**工具**，，然后**重置Microsoft Visual Studio 2010 实验实例**。 您可以重新生成任何其他你想要再次使用的 Dsl。  
  
     \- 或 -  
  
- 如果[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展使用此文件扩展名的完全安装在计算机上，卸载它。 上**工具**菜单上，单击**扩展管理器**。  
  
### <a name="product-settings-page"></a>产品设置页  
 **新的特定于域的语言所属的产品名称是什么？**  
 默认值为 DSL 名称。  
  
 在 Windows 资源管理器 （或文件资源管理器） 来描述此文件扩展名的文件中使用此值。  
  
 **产品所属的公司名称是什么？**  
 你的公司名称。  
  
 此值将合并到在 DSL 程序包的程序集信息属性。  
  
 **什么是此解决方案中项目的根命名空间？**  
 此值默认为创建从你的公司的名称和产品名称。  
  
### <a name="signing-page"></a>签名页  
 **创建强名称密钥文件**  
 默认选项是创建新 DSL 程序集进行签名的密钥。  
  
 **使用现有的强名称密钥**  
 如果你想要将你的 DSL 集成与另一个程序集，请使用此选项。  
  
 有关强命名的详细信息，请参阅[创建和使用具有强名称程序集](http://go.microsoft.com/fwlink/?LinkId=186073)。  
  
## <a name="see-also"></a>请参阅  
 [如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)   
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
