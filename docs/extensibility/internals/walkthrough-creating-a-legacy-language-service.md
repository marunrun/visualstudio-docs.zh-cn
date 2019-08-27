---
title: 演练：创建旧版语言服务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d5fdffa76f273bc8ff7b7bdf18ce9db99a9052e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323417"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>演练：创建旧版语言服务
使用托管的包框架 (MPF) 语言类实现中的语言服务[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]非常简单。 所需的 VSPackage，托管语言服务、 语言服务本身和你的语言分析器。

## <a name="prerequisites"></a>系统必备
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../../extensibility/visual-studio-sdk.md)。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio 包项目模板的位置
 可以在中的三个不同的模板位置找到 Visual Studio 包项目模板**新的项目**对话框：

1. 在“Visual Basic 扩展性”之下。 项目的默认语言为 Visual Basic。

2. 在“C# 扩展性”之下。 项目的默认语言为 C#。

3. 在“其他项目类型扩展性”之下。 项目的默认语言为 C++。

### <a name="create-a-vspackage"></a>创建 VSPackage

1. 使用 Visual Studio 包项目模板创建新的 VSPackage。

    如果要添加到现有的 VSPackage 的语言服务，跳过以下步骤，直接转到"创建语言服务类"过程。

2. MyLanguagePackage 输入项目的名称，再单击**确定**。

    可以使用所需的任何名称。 此处详细介绍这些过程假设 MyLanguagePackage 作为名称。

3. 选择[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]作为语言和用于生成新的密钥文件的选项。 单击 **“下一步”** 。

4. 输入相应的公司和包信息。 单击 **“下一步”** 。

5. 选择**菜单命令**。 单击 **“下一步”** 。

    如果不想支持代码段，您可以只需单击完成并忽略下一步。

6. 输入**插入代码片段**作为**命令名**并`cmdidInsertSnippet`有关**命令 ID**。 单击 **“完成”** 。

    **命令名称**并**命令 ID**可以是任何所需内容，这些是只是示例。

### <a name="create-the-language-service-class"></a>创建语言服务类

1. 在中**解决方案资源管理器**，右键单击 MyLanguagePackage 项目，选择**添加**，**引用**，然后选择**添加新引用**按钮。

2. 在中**添加引用**对话框中，选择**Microsoft.VisualStudio.Package.LanguageService**中 **.NET**选项卡并单击**确定**。

     这需要进行一次的语言包项目。

3. 在中**解决方案资源管理器**，右键单击 VSPackage 项目并选择**添加**，**类**。

4. 请确保**类**模板列表中选择。

5. 输入**MyLanguageService.cs**名称的类文件，并单击**添加**。

     可以使用所需的任何名称。 此处详细介绍这些过程假设`MyLanguageService`作为名称。

6. 在 MyLanguageService.cs 文件中，添加以下`using`语句。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_1.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_1.vb)]

7. 修改`MyLanguageService`类进行派生<xref:Microsoft.VisualStudio.Package.LanguageService>类：

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_2.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_2.vb)]

8. 将光标置于"LanguageService"上来回**编辑**， **IntelliSense**菜单中，选择**实现抽象类**。 这会添加最小必需的方法来实现的语言服务类。

9. 实现抽象方法，如中所述[实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)。

### <a name="register-the-language-service"></a>注册语言服务

1. 打开 MyLanguagePackagePackage.cs 文件并添加以下`using`语句：

     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_3.vb)]
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_3.cs)]

2. 注册您的语言服务类，如中所述[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。 这包括 ProvideXX 属性和"Proffering 语言服务"部分。 使用本主题使用 TestLanguageService 其中 MyLanguageService。

### <a name="the-parser-and-scanner"></a>分析器和扫描程序

1. 实现分析器和扫描程序针对你的语言，如中所述[旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。

     分析器和扫描程序的实现方式完全取决于您并不在本主题的范围。

## <a name="language-service-features"></a>语言服务功能
 语言服务中实现每项功能，您通常从相应的 MPF 语言服务类派生一个类、 在必要时，实现任何抽象方法和重写适当的方法。 你想要支持哪些类创建和/或派生自所依赖的功能。 中详细地讨论这些功能[旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)。 下面的过程是从 MPF 类派生类到常规的方法。

#### <a name="deriving-from-an-mpf-class"></a>从 MPF 类派生

1. 在中**解决方案资源管理器**，右键单击 VSPackage 项目并选择**添加**，**类**。

2. 请确保**类**模板列表中选择。

     输入类文件的合适名称，然后单击**添加**。

3. 在新类文件中，添加以下`using`语句。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_4.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_4.vb)]

4. 修改要从所需的 MPF 类派生的类。

5. 添加至少需要与基类的构造函数相同的参数的类构造函数并传递到基类构造函数的构造函数参数。

     例如，一个类的构造函数派生自<xref:Microsoft.VisualStudio.Package.Source>类可能如下所示：

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_5.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_5.vb)]

6. 从**编辑**， **IntelliSense**菜单中，选择**实现抽象类**如果基类不包含任何必须实现的抽象方法。

7. 否则为放置在类中插入符号并输入要重写的方法。

     例如，键入`public override`若要查看所有可以在此类中重写的方法的列表。

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)