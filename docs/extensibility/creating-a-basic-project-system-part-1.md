---
title: 创建基本项目系统，第 1 部分 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 19c73e47e8c07ebcf7c1124e6e59d80f76101458
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341655"
---
# <a name="create-a-basic-project-system-part-1"></a>创建基本项目系统，第 1 部分
在 Visual Studio 中，项目是开发人员用于组织源代码文件和其他资产的容器。 项目显示为解决方案中的子级**解决方案资源管理器**。 项目可组织、 生成、 调试和部署的源代码和创建对 Web 服务、 数据库和其他资源的引用。

 项目文件中定义项目，例如 *.csproj* Visual C# 项目文件。 可以创建自己的项目类型具有自己的项目文件扩展名。 有关项目类型的详细信息，请参阅[项目类型](../extensibility/internals/project-types.md)。

> [!NOTE]
> 如果你需要使用自定义项目类型来扩展 Visual Studio，我们强烈建议利用[Visual Studio 项目系统](https://github.com/Microsoft/VSProjectSystem)(VSP) 具有一系列通过生成一个从零开始的项目系统的优势：
>
> - 更轻松的载入。  基本项目系统需要成千上万行代码。  利用 VSP 可以载入成本减少到几次单击之前已准备好你的需求进行自定义。
> - 更便于维护。  通过利用 VSP，只需维护自己的方案。  我们处理所有项目系统基础结构在其的执行。
>
>   如果需要面向版本早于 Visual Studio 2013 的 Visual Studio，你将不能在 Visual Studio 扩展中利用 VSP。  如果是这种情况，本演练是入门的好时机。

 本演练演示如何创建具有项目文件扩展名的项目类型 *.myproj*。 本演练中利用的现有的 Visual C# 项目系统。

> [!NOTE]
> 扩展项目的更多示例，请参阅[VSSDK 示例](https://aka.ms/vs2015sdksamples)。

 本演练介绍了如何完成这些任务：

- 创建基本项目类型。

- 创建基本项目模板。

- 注册 Visual Studio 项目模板。

- 创建一个项目实例，方法是打开**新的项目**对话框，然后使用你的模板。

- 创建你的项目系统的项目工厂。

- 创建你的项目系统的项目节点。

- 添加对项目系统的自定义图标。

- 实现基本的模板参数替换。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

 您还必须下载的源代码[项目的托管包框架](https://github.com/tunnelvisionlabs/MPFProj10)。 将文件提取到要创建的解决方案可以访问的位置。

## <a name="create-a-basic-project-type"></a>创建基本项目类型
 创建一个名为 C# VSIX 项目**SimpleProject**。 (**文件** > **新** > **项目**，然后**Visual C#**  >  **可扩展性** > **VSIX 项目**)。 Visual Studio 包项目项模板添加 (上**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**，然后转到**扩展性** > **Visual Studio 包**)。 将文件命名*SimpleProjectPackage*。

## <a name="creating-a-basic-project-template"></a>创建基本项目模板
 现在，可以修改此基本 VSPackage 实现的新 *.myproj*项目类型。 若要创建基于项目 *.myproj*项目类型，Visual Studio 必须知道哪些文件、 资源和要添加到新项目的引用。 若要提供此信息，请将项目文件置于项目模板文件夹。 当用户使用 *.myproj*项目创建的项目中，将文件复制到新的项目。

### <a name="to-create-a-basic-project-template"></a>若要创建基本项目模板

1. 添加到项目中，一个在其他三个文件夹：*Templates\Projects\SimpleProject*. (在**解决方案资源管理器**，右键单击**SimpleProject**项目节点，指向**添加**，然后单击**新文件夹**。 将文件夹命名为*模板*。 在中*模板*文件夹中，添加名为的文件夹*项目*。 在*项目*文件夹中，添加名为的文件夹*SimpleProject*。)

2. 在中*Templates\Projects\SimpleProject*文件夹中，添加要用作名为的图标的位图图像文件*SimpleProject.ico*。 当您单击**添加**，打开图标编辑器。

3. 使图标不同。 此图标将出现在**新的项目**稍后的演练中的对话框。

    ![简单项目图标](../extensibility/media/simpleprojicon.png "SimpleProjIcon")

4. 将图标保存并关闭图标编辑器中。

5. 在中*Templates\Projects\SimpleProject*文件夹中，添加**类**项名为*Program.cs*。

6. 现有代码替换为以下行。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Text;

   namespace $nameSpace$
   {
       public class $className$
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

   > [!IMPORTANT]
   > 这不是最终的窗体*Program.cs*代码; 参数将在后面的步骤处理的替换。 你可能会看到编译错误，但只要文件的**BuildAction**是**内容**，您应该能够生成并照常运行项目。

7. 保存该文件。

8. 复制*AssemblyInfo.cs*文件从*属性*文件夹*Projects\SimpleProject*文件夹。

9. 在中*Projects\SimpleProject*文件夹中添加名为 XML 文件*SimpleProject.myproj*。

   > [!NOTE]
   > 此类型的所有项目的文件扩展名是 *.myproj*。 如果你想要对其进行更改，必须在本演练中提到的所有位置更改。

10. 现有内容替换为以下行。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid></ProjectGuid>
        <OutputType>Exe</OutputType>
        <RootNamespace>MyRootNamespace</RootNamespace>
        <AssemblyName>MyAssemblyName</AssemblyName>
        <EnableUnmanagedDebugging>false</EnableUnmanagedDebugging>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        <DebugSymbols>true</DebugSymbols>
        <OutputPath>bin\Debug\</OutputPath>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
        <DebugSymbols>false</DebugSymbols>
        <OutputPath>bin\Release\</OutputPath>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="mscorlib" />
        <Reference Include="System" />
        <Reference Include="System.Data" />
        <Reference Include="System.Xml" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="AssemblyInfo.cs">
          <SubType>Code</SubType>
        </Compile>
        <Compile Include="Program.cs">
          <SubType>Code</SubType>
        </Compile>
      </ItemGroup>
      <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
    </Project>
    ```

11. 保存该文件。

12. 在中**属性**窗口中，将**生成操作**的*AssemblyInfo.cs*， *Program.cs*， *SimpleProject.ico*，并*SimpleProject.myproj*到**内容**，并设置其**包含在 VSIX**属性设置为**True**.

    此项目模板介绍基本 Visual C# 项目的调试配置和发布配置。 该项目包括两个源文件*AssemblyInfo.cs*并*Program.cs*，和多个程序集引用。 从模板创建项目，ProjectGuid 值是自动替换为新的 GUID。

    在中**解决方案资源管理器**，展开**模板**文件夹应出现，如下所示：

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>创建基本项目工厂
 必须告知 Visual Studio 项目模板文件夹的位置。 若要执行此操作，请将属性添加到 VSPackage 类，该类实现项目工厂，以便生成 VSPackage 时，模板位置写入到系统注册表。 首先创建一个基本项目工厂，它由项目工厂 GUID 标识。 使用<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>属性来连接到的项目工厂`SimpleProjectPackage`类。

### <a name="to-create-a-basic-project-factory"></a>若要创建基本项目工厂

1. 为项目工厂创建 Guid (上**工具**菜单上，单击**创建 GUID**)，或使用下面的示例所示。 添加到 Guid`SimpleProjectPackage`附近与已定义的部分类`PackageGuidString`。 Guid 必须为 GUID 格式和字符串格式。 生成的代码应类似于下面的示例。

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. 将一个类添加到顶部*SimpleProject*名为文件夹*SimpleProjectFactory.cs*。

3. 添加以下 using 语句：

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. 添加到 GUID 属性`SimpleProjectFactory`类。 属性的值是新项目工厂的 GUID。

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   现在可以注册你的项目模板。

### <a name="to-register-the-project-template"></a>若要注册的项目模板

1. 在中*SimpleProjectPackage.cs*，添加<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>属性为`SimpleProjectPackage`类，如下所示。

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. 重新生成解决方案并验证正确生成。

    重新生成注册项目模板。

   参数`defaultProjectExtension`并`possibleProjectExtensions`设置为项目文件扩展名 ( *.myproj*)。 `projectTemplatesDirectory`参数设置为的相对路径*模板*文件夹。 在生成过程将转换为完整生成并添加到注册表注册项目系统中此路径。

## <a name="test-the-template-registration"></a>测试模板注册
 模板注册会告知 Visual Studio 项目模板文件夹的位置，以使 Visual Studio 可以显示的模板名称和图标**新的项目**对话框。

### <a name="to-test-the-template-registration"></a>若要测试模板注册

1. 按**F5**开始调试 Visual Studio 的实验实例。

2. 在实验实例中，创建一个新创建的项目类型的新项目。 在中**新的项目**对话框中，你应看到**SimpleProject**下**已安装的模板**。

   现在你已注册的项目工厂。 但是，它尚不能创建一个项目。 项目包和项目工厂协同工作来创建和初始化一个项目。

## <a name="add-the-managed-package-framework-code"></a>添加托管包框架代码
 实现项目包和项目工厂之间的连接。

- 为托管包框架导入的源代码文件。

    1. 卸载 SimpleProject 项目 (在**解决方案资源管理器**，选择项目节点，然后在上下文菜单上单击**卸载项目**。) 和 XML 编辑器中打开项目文件。

    2. 将以下块添加到项目文件 (正上方\<导入 > 块)。 设置`ProjectBasePath`到的位置*ProjectBase.files*刚下载的托管包框架代码中的文件。 您可能需要添加一个反斜杠到路径名。 如果不这样做，项目可能无法找到托管包框架的源代码。

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > 请不要忘记在路径末尾的反斜杠。

    3. 重新加载项目。

    4. 添加对下列程序集的引用：

        - `Microsoft.VisualStudio.Designer.Interfaces` (in *\<VSSDK install>\VisualStudioIntegration\Common\Assemblies\v2.0*)

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>若要初始化项目工厂

1. 在中*SimpleProjectPackage.cs*文件中，添加以下`using`语句。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. 派生`SimpleProjectPackage`类从`Microsoft.VisualStudio.Package.ProjectPackage`。

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. 注册项目工厂。 添加下面的代码行`SimpleProjectPackage.Initialize`方法，之后`base.Initialize`。

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. 实现抽象属性`ProductUserContext`:

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. 在中*SimpleProjectFactory.cs*，添加以下`using`后的现有语句`using`语句。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. 派生`SimpleProjectFactory`类从`ProjectFactory`。

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. 添加到以下虚拟方法`SimpleProjectFactory`类。 将在后面的部分实现此方法。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. 添加以下字段和构造函数`SimpleProjectFactory`类。 这`SimpleProjectPackage`引用缓存在私有字段，以便可在设置服务提供者站点。

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. 重新生成解决方案并验证正确生成。

## <a name="test-the-project-factory-implementation"></a>测试项目工厂实现
 测试是否调用项目工厂实现的构造函数。

### <a name="to-test-the-project-factory-implementation"></a>若要测试的项目工厂实现

1. 在中*SimpleProjectFactory.cs*文件中中的以下行上设置断点`SimpleProjectFactory`构造函数。

    ```csharp
    this.package = package;
    ```

2. 按**F5**启动 Visual Studio 的实验实例。

3. 在实验实例中，开始创建新的项目。 在中**新的项目**对话框中，选择**SimpleProject**项目类型，然后单击**确定**。 执行在断点处停止。

4. 清除断点和停止调试。 由于我们具有尚未创建的项目节点，项目创建代码仍将引发异常。

## <a name="extend-the-projectnode-class"></a>扩展 ProjectNode 类
 现在可以实现`SimpleProjectNode`类，该类派生自`ProjectNode`类。 `ProjectNode`基类处理项目创建的以下任务：

- 将项目模板文件，复制*SimpleProject.myproj*，为新的项目文件夹。 根据输入中的名称重命名该副本**新的项目**对话框。 `ProjectGuid`属性值替换为新的 GUID。

- 遍历的项目模板文件中，MSBuild 元素*SimpleProject.myproj*，并查找`Compile`元素。 每个`Compile`目标文件，将文件复制到新的项目文件夹。

  派生`SimpleProjectNode`类处理这些任务：

- 使项目和文件中的节点的图标**解决方案资源管理器**要创建或选择。

- 使指定的其他项目模板参数替换。

### <a name="to-extend-the-projectnode-class"></a>若要扩展 ProjectNode 类

1. 添加一个名为类`SimpleProjectNode.cs`。

2. 用下面的代码替换现有代码。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Project;

   namespace SimpleProject
   {
       public class SimpleProjectNode : ProjectNode
       {
           private SimpleProjectPackage package;

           public SimpleProjectNode(SimpleProjectPackage package)
           {
               this.package = package;
           }
           public override Guid ProjectGuid
           {
               get { return SimpleProjectPackage.guidSimpleProjectFactory; }
           }
           public override string ProjectType
           {
               get { return "SimpleProjectType"; }
           }

           public override void AddFileFromTemplate(
               string source, string target)
           {
               this.FileTemplateProcessor.UntokenFile(source, target);
               this.FileTemplateProcessor.Reset();
           }
       }
   }
   ```

   这`SimpleProjectNode`类实现了这些重写的方法：

- `ProjectGuid`它返回项目工厂的 GUID。

- `ProjectType`它返回的项目类型的本地化的名称。

- `AddFileFromTemplate`其中模板文件夹中将选定的文件复制到目标项目。 在后面的部分中进一步实现此方法。

  `SimpleProjectNode`构造函数，如`SimpleProjectFactory`构造函数中，缓存`SimpleProjectPackage`中以供将来使用的私有字段的引用。

  若要连接`SimpleProjectFactory`类来`SimpleProjectNode`类，您必须实例化一个新`SimpleProjectNode`中`SimpleProjectFactory.CreateProject`方法并将其缓存以供将来使用的私有字段中。

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>若要连接的项目工厂类和节点类

1. 在中*SimpleProjectFactory.cs*文件中，添加以下`using`语句：

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. 替换为`SimpleProjectFactory.CreateProject`方法通过使用下面的代码。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. 重新生成解决方案并验证正确生成。

## <a name="test-the-projectnode-class"></a>测试 ProjectNode 类
 测试您的项目工厂以查看它是否创建项目层次结构。

### <a name="to-test-the-projectnode-class"></a>若要测试 ProjectNode 类

1. 按 **F5** 启动调试。 在实验实例中，将创建新 SimpleProject。

2. Visual Studio 应调用你的项目工厂创建的项目。

3. 关闭 Visual Studio 的实验实例。

## <a name="add-a-custom-project-node-icon"></a>添加自定义项目节点图标
 前面部分中的项目节点图标是一个默认图标。 可以将其更改为自定义图标。

### <a name="to-add-a-custom-project-node-icon"></a>若要添加自定义项目节点图标

1. 在中**资源**文件夹中，添加名为的位图文件*SimpleProjectNode.bmp*。

2. 在中**属性**windows，减至 16 × 16 像素的位图。 请以不同的位图。

    ![Simple Project Comm](../extensibility/media/simpleprojprojectcomm.png "SimpleProjProjectComm")

3. 在中**属性**窗口中，更改**生成操作**的位图**嵌入的资源**。

4. 在中*SimpleProjectNode.cs*，添加以下`using`语句：

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. 添加以下静态字段和构造函数`SimpleProjectNode`类。

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. 将以下属性添加到开头`SimpleProjectNode`类。

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. 实例构造函数替换为以下代码。

   ```csharp
   public SimpleProjectNode(SimpleProjectPackage package)
   {
       this.package = package;

       imageIndex = this.ImageHandler.ImageList.Images.Count;

       foreach (Image img in imageList.Images)
       {
           this.ImageHandler.AddImage(img);
       }
   }
   ```

   在静态构造期间`SimpleProjectNode`从程序集清单资源中检索项目节点位图，并将其缓存以供将来使用的私有字段中。 请注意语法的<xref:System.Reflection.Assembly.GetManifestResourceStream%2A>映像路径。 若要查看嵌入程序集中的清单资源的名称，请使用<xref:System.Reflection.Assembly.GetManifestResourceNames%2A>方法。 当此方法应用于`SimpleProject`程序集，结果应按如下所示：

- *SimpleProject.Resources.resources*

- *VisualStudio.Project.resources*

- *SimpleProject.VSPackage.resources*

- *Resources.imagelis.bmp*

- *Microsoft.VisualStudio.Project.DontShowAgainDialog.resources*

- *Microsoft.VisualStudio.Project.SecurityWarningDialog.resources*

- *SimpleProject.Resources.SimpleProjectNode.bmp*

  在实例构造期间`ProjectNode`基础类加载*Resources.imagelis.bmp*，在其中嵌入通常使用从 16 × 16 位图*Resources\imagelis.bmp*。 此位图列表将提供给`SimpleProjectNode`作为`ImageHandler.ImageList`。 `SimpleProjectNode` 将项目节点位图追加到列表。 项目节点位图图像列表中的偏移量进行缓存以供将来使用的公共值`ImageIndex`属性。 Visual Studio 使用此属性来确定要显示为项目节点图标的位图。

## <a name="test-the-custom-project-node-icon"></a>测试节点自定义项目图标
 测试您的项目工厂以查看它是否创建具有自定义项目节点图标的项目层次结构。

### <a name="to-test-the-custom-project-node-icon"></a>若要测试自定义项目节点图标

1. 开始调试，并在实验实例中创建新 SimpleProject。

2. 在新建的项目中，注意*SimpleProjectNode.bmp*用作项目节点图标。

     ![简单项目新建项目节点](../extensibility/media/simpleprojnewprojectnode.png "SimpleProjNewProjectNode")

3. 打开*Program.cs*代码编辑器中。 您应看到类似于下面的代码的源代码。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace $nameSpace$
    {
        public class $className$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

     请注意，模板参数 $nameSpace$ 和 $ $className$ 没有新值。 您将学习如何实现下一节中的模板参数替换。

## <a name="substitute-template-parameters"></a>替换模板参数
 在前面部分中，你的项目模板与 Visual Studio 使用注册`ProvideProjectFactory`属性。 以这种方式注册的模板文件夹的路径，你可以通过重写并扩展让基本模板参数替换`ProjectNode.AddFileFromTemplate`类。 有关详细信息，请参阅[生成新项目：实质上，第二部分](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 现在，添加到替代代码`AddFileFromTemplate`类。

### <a name="to-substitute-template-parameters"></a>若要替换模板参数

1. 在中*SimpleProjectNode.cs*文件中，添加以下`using`语句。

   ```csharp
   using System.IO;
   ```

2. 替换为`AddFileFromTemplate`方法通过使用下面的代码。

   ```csharp
   public override void AddFileFromTemplate(
       string source, string target)
   {
       string nameSpace =
           this.FileTemplateProcessor.GetFileNamespace(target, this);
       string className = Path.GetFileNameWithoutExtension(target);

       this.FileTemplateProcessor.AddReplace("$nameSpace$", nameSpace);
       this.FileTemplateProcessor.AddReplace("$className$", className);

       this.FileTemplateProcessor.UntokenFile(source, target);
       this.FileTemplateProcessor.Reset();
   }
   ```

3. 设置断点在方法中，紧靠`className`赋值语句。

   赋值语句确定命名空间和新的类名称的合理值。 这两个`ProjectNode.FileTemplateProcessor.AddReplace`方法调用通过使用这些新值来替换相应的模板参数值。

## <a name="test-the-template-parameter-substitution"></a>测试模板参数替换
 现在，你可以测试模板参数替换。

### <a name="to-test-the-template-parameter-substitution"></a>若要测试模板参数替换

1. 开始调试，并在实验实例中创建新 SimpleProject。

2. 中的断点处停止执行`AddFileFromTemplate`方法。

3. 检查有关值`nameSpace`和`className`参数。

   - `nameSpace` 给定的值\<根命名空间 > 元素中的 *\Templates\Projects\SimpleProject\SimpleProject.myproj*项目模板文件。 在本例中，该值为 `MyRootNamespace`。

   - `className` 都提供了此类源的文件名称，不带文件扩展名值。 在这种情况下，要复制到目标文件夹中的第一个文件是*AssemblyInfo.cs*; 因此，类名的值是`AssemblyInfo`。

4. 删除该断点并按**F5**继续执行。

    Visual Studio 应会完成创建项目。

5. 打开*Program.cs*代码编辑器中。 您应看到类似于下面的代码的源代码。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;

   namespace MyRootNamespace
   {
       public class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

    请注意，现已在命名空间`MyRootNamespace`和类名称现在是`Program`。

6. 开始调试项目。 新的项目应编译、 运行和显示"Hello VSX!!!" 显示文本字符串“Hello World!”。

    ![简单项目命令](../extensibility/media/simpleprojcommand.png "SimpleProjCommand")

   祝贺你！ 您已实现的基本托管的项目系统。