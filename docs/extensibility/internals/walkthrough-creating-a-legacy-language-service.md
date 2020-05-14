---
title: 演练：创建传统语言服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59ec18ab0c97ec89422e06f5b33804adcc750d5a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703690"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>演练：创建旧版语言服务
使用托管包框架 （MPF） 语言类来实现 语言[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]服务非常简单。 您需要一个 VSPackage 来托管语言服务、语言服务本身以及语言的解析器。

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[可视化工作室 SDK](../../extensibility/visual-studio-sdk.md)。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio 包项目模板的位置
 "可视化工作室包项目模板"可在 **"新项目"** 对话框中的三个不同模板位置找到：

1. 在“Visual Basic 扩展性”之下。 项目的默认语言为 Visual Basic。

2. 在“C# 扩展性”之下。 项目的默认语言为 C#。

3. 在“其他项目类型扩展性”之下。 项目的默认语言为 C++。

### <a name="create-a-vspackage"></a>创建 VS 包

1. 使用可视化工作室包项目模板创建新的 VS 包。

    如果要将语言服务添加到现有 VSPackage，请跳过以下步骤，然后直接转到"创建语言服务类"过程。

2. 输入项目名称的"我的语言包"，然后单击 **"确定**"。

    您可以使用任何所需的名称。 此处详述的这些过程将"我的语言包"作为名称。

3. 选择[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]作为语言和生成新密钥文件的选项。 单击“下一步”。 

4. 输入相应的公司和包裹信息。 单击“下一步”。 

5. 选择**菜单命令**。 单击“下一步”。 

    如果您不打算支持代码段，只需单击"完成"并忽略下一步即可。

6. 输入 **"插入代码段**"作为**命令名称**`cmdidInsertSnippet`和**命令 ID**。 单击“完成”  。

    **命令名称**和**命令 ID**可以是所需的任何内容，这些只是示例。

### <a name="create-the-language-service-class"></a>创建语言服务类

1. 在**解决方案资源管理器**中，右键单击 My语言包项目，选择 **"添加**"**参考**，然后选择"**添加新参考"** 按钮。

2. 在 **"添加参考"** 对话框中，在 **.NET**选项卡中选择**Microsoft.VisualStudio.Package.语言服务**，然后单击"**确定**"。

     对于语言包项目，只需执行一次此操作。

3. 在**解决方案资源管理器**中，右键单击 VSPackage 项目并选择"**添加**"**类**。

4. 确保在模板列表中选择了**类**。

5. 输入**类文件名称MyLanguageService.cs，** 然后单击"**添加**"。

     您可以使用任何所需的名称。 此处详述的这些过程`MyLanguageService`假定为名称。

6. 在MyLanguageService.cs文件中，添加以下`using`指令。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_1.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_1.vb)]

7. 修改要`MyLanguageService`派生自类的<xref:Microsoft.VisualStudio.Package.LanguageService>类：

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_2.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_2.vb)]

8. 将光标放在"语言服务"和 **"编辑****、IntelliSense"** 菜单中，选择 **"实现抽象类**"。 这将添加实现语言服务类的最低必要方法。

9. 实现[实现旧语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)中所述的抽象方法。

### <a name="register-the-language-service"></a>注册语言服务

1. 打开MyLanguagePackagePackage.cs文件并添加以下`using`指令：

     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_3.vb)]
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_3.cs)]

2. 注册您的语言服务类，如[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)中所述。 这包括提供XX属性和"提供语言服务"部分。 使用"我的语言服务"，本主题使用测试语言服务。

### <a name="the-parser-and-scanner"></a>解析器和扫描仪

1. 实现您的语言的解析器和扫描仪，如[旧语言服务解析器和扫描仪](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)中所述。

     如何实现解析器和扫描仪完全取决于您，并且超出了本主题的范围。

## <a name="language-service-features"></a>语言服务功能
 要实现语言服务中的每个功能，通常从相应的 MPF 语言服务类派生一个类，根据需要实现任何抽象方法，并重写适当的方法。 您创建和/或派生的类取决于要支持的功能。 这些功能在[旧语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)中进行了详细讨论。 以下过程是从 MPF 类派生类的一般方法。

#### <a name="deriving-from-an-mpf-class"></a>从 MPF 类派生

1. 在**解决方案资源管理器**中，右键单击 VSPackage 项目并选择"**添加**"**类**。

2. 确保在模板列表中选择了**类**。

     输入类文件的合适名称，然后单击 **"添加**"。

3. 在新类文件中，添加以下`using`指令。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_4.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_4.vb)]

4. 修改类以从所需的 MPF 类派生。

5. 添加至少采用与基类构造函数相同的参数的类构造函数，并将构造函数参数传递给基类构造函数。

     例如，派生自类的<xref:Microsoft.VisualStudio.Package.Source>类的构造函数可能如下所示：

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_5.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_5.vb)]

6. 在 **"编辑****、IntelliSense"** 菜单中，如果基类具有必须实现的任何抽象方法，请选择 **"实现抽象类**"。

7. 否则，将 care 放置在类中，并输入要重写的方法。

     例如，键入`public override`以查看该类中可以重写的所有方法的列表。

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
