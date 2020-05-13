---
title: 创建基本项目系统，第 2 部分 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: aee48fc6-a15f-4fd5-8420-7f18824de220
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7823dc949e78cc6d22514a1ba93476fd5f42d076
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739709"
---
# <a name="create-a-basic-project-system-part-2"></a>创建基本项目系统，第 2 部分
本系列的第一个演练"[创建基本项目系统"第 1 部分](../extensibility/creating-a-basic-project-system-part-1.md)演示如何创建基本项目系统。 本演练通过添加 Visual Studio 模板、属性页和其他功能构建基本项目系统。 在开始第一次演练之前，您必须完成第一次演练。

本演练将介绍如何创建具有项目文件名扩展名 *.myproj*的项目类型。 要完成演练，您不必创建自己的语言，因为演练借用了现有的 Visual C++ 项目系统。

本演练将介绍如何完成这些任务：

- 创建可视化工作室模板。

- 部署可视化工作室模板。

- 在 **"新项目"** 对话框中创建项目类型子节点。

- 在可视化工作室模板中启用参数替换。

- 创建项目属性页。

> [!NOTE]
> 本演练中的步骤基于 C# 项目。 但是，除了文件名扩展名和代码等细节外，您可以对 Visual Basic 项目使用相同的步骤。

## <a name="create-a-visual-studio-template"></a>创建可视化工作室模板
- [创建基本项目系统，第 1 部分](../extensibility/creating-a-basic-project-system-part-1.md)演示如何创建基本项目模板并将其添加到项目系统。 它还演示如何使用<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>属性向 Visual Studio 注册此模板，该属性在系统注册表中写入*\\模板_Project_SimpleProject\\*文件夹的完整路径。

通过使用 Visual Studio 模板 *（.vstemplate*文件） 而不是基本项目模板，可以控制模板在 **"新项目"** 对话框中的显示方式以及如何替换模板参数。 *.vstemplate*文件是一个 XML 文件，用于描述如何使用项目系统模板创建项目时如何包括源文件。 项目系统本身是通过收集 *.vstemplate*文件和 *.zip*文件中的源文件而构建的，并通过将 *.zip*文件复制到 Visual Studio 已知的位置进行部署。 此过程在本演练的后面部分进行了详细介绍。

1. 在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]中，打开通过以下[创建基本项目系统（第 1 部分](../extensibility/creating-a-basic-project-system-part-1.md)）创建的 SimpleProject 解决方案。

2. 在*SimpleProjectPackage.cs*文件中，查找"提供项目工厂"属性。 将第二个参数（项目名称）替换为 null，将第四个参数（项目模板文件夹的路径）替换为""。\\*NullPath"，如下所示。

    ```
    [ProvideProjectFactory(typeof(SimpleProjectFactory), null,
        "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
        ".\\NullPath",
    LanguageVsTemplate = "SimpleProject")]
    ```

3. 将名为*SimpleProject.vstemplate*的 XML 文件添加到*\\模板\项目_\\简单项目*文件夹。

4. 将*SimpleProject.vstemplate*的内容替换为以下代码。

    ```xml
    <VSTemplate Version="2.0.0" Type="Project"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
      <TemplateData>
        <Name>SimpleProject Application</Name>
        <Description>
          A project for creating a SimpleProject application
        </Description>
        <Icon>SimpleProject.ico</Icon>
        <ProjectType>SimpleProject</ProjectType>
      </TemplateData>
      <TemplateContent>
        <Project File="SimpleProject.myproj" ReplaceParameters="true">
          <ProjectItem ReplaceParameters="true" OpenInEditor="true">
            Program.cs
          </ProjectItem>
          <ProjectItem ReplaceParameters="true" OpenInEditor="false">
            AssemblyInfo.cs
          </ProjectItem>
        </Project>
      </TemplateContent>
    </VSTemplate>
    ```

5. 在 **"属性"** 窗口中，选择*\\\\模板\项目_简单项目*文件夹中的所有五个文件，并将**生成操作**设置为**ZipProject**。

    ![简单项目文件夹](../extensibility/media/simpproj2.png "辛普普杰2")

    "\<模板数据>"部分确定 **"新项目"** 对话框中"简单项目项目类型"的位置和外观，如下所示：

- 名称\<>元素将项目模板命名为"简单项目应用程序"。

- "\<描述>元素包含选择项目模板时显示在 **"新项目"** 对话框中的说明。

- 图标\<>元素指定与简单项目项目类型一起显示的图标。

- "\<项目类型>元素在 **"新项目"** 对话框中命名项目类型。 此名称将替换"提供项目工厂"属性的项目名称参数。

  > [!NOTE]
  > ProjectType \<> 元素必须与`LanguageVsTemplate`SimpleProjectPackage.cs文件中`ProvideProjectFactory`的属性参数匹配。

  模板\<内容>部分介绍创建新项目时生成的这些文件：

- *简单项目.myproj*

- *Program.cs*

- *AssemblyInfo.cs*

  所有三个文件`ReplaceParameters`都设置为 true，从而启用参数替换。 *Program.cs*文件已`OpenInEditor`设置为 true，这将导致在创建项目时在代码编辑器中打开该文件。

  有关可视化工作室模板架构中的元素的详细信息，请参阅[可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)。

> [!NOTE]
> 如果项目有多个 Visual Studio 模板，则每个模板都在单独的文件夹中。 该文件夹中的每个文件都必须将**生成操作**设置为**ZipProject**。

## <a name="adding-a-minimal-vsct-file"></a>添加最小的 .vsct 文件
 可视化工作室必须在设置模式下运行，以识别新的或修改的可视化工作室模板。 设置模式需要存在 *.vsct*文件。 因此，您必须向项目添加最小的 *.vsct*文件。

1. 将名为*SimpleProject.vsct 的*XML 文件添加到简单项目项目中。

2. 将*SimpleProject.vsct*文件的内容替换为以下代码。

    ```
    <?xml version="1.0" encoding="utf-8" ?>
    <CommandTable
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
    </CommandTable>
    ```

3. 将此文件的**生成操作**设置为**VSCT 编译**。 只能在 *.csproj*文件中执行此操作，不能在 **"属性"** 窗口中执行此操作。 确保此时此文件的**生成操作**设置为 **"无**"。

    1. 右键单击简单项目节点，然后单击 **"编辑简单项目.csproj**"。

    2. 在 *.csproj*文件中，找到*SimpleProject.vsct*项。

        ```
        <None Include="SimpleProject.vsct" />
        ```

    3. 将生成操作更改为**VSCT 编译**。

        ```
        <VSCTCompile Include="SimpleProject.vsct" />
        ```

    4. 项目文件并关闭编辑器。

    5. 保存简单项目节点，然后在**解决方案资源管理器**中单击 **"重新加载项目**"。

## <a name="examine-the-visual-studio-template-build-steps"></a>检查可视化工作室模板生成步骤
 VSPackage 项目生成系统通常在设置模式下运行 Visual Studio，当 *.vstemplate*文件发生更改或包含 *.vstemplate*文件的项目被重建时。 通过设置 MSBuild 的详细程度级别或更高版本，可以遵循这一点。

1. 在“工具” **** 菜单上，单击“选项” ****。

2. 展开**项目和解决方案**节点，然后选择 **"生成"和"运行**"。

3. 将**MSBuild 项目生成输出详细性**设置为 **"正常**"。 单击“确定”。

4. 重建简单项目项目。

    创建 *.zip*项目文件的生成步骤应类似于以下示例。

```
ZipProjects:
1>  Zipping ProjectTemplates
1>  Zipping <path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip...
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "<%LOCALAPPDATA%>\Microsoft\VisualStudio\14.0Exp\ProjectTemplates\\\\SimpleProject.zip".
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "bin\Debug\\ProjectTemplates\\\\SimpleProject.zip".
1>  SimpleProject -> <path>\SimpleProject\SimpleProject\bin\Debug\ProjectTemplates\SimpleProject.zip
1>ZipItems:
1>  Zipping ItemTemplates
1>  SimpleProject ->
```

## <a name="deploy-a-visual-studio-template"></a>部署可视化工作室模板
可视化工作室模板不包含路径信息。 因此，模板 *.zip*文件必须部署到 Visual Studio 已知的位置。 ProjectTemplates 文件夹的位置通常 *<%LOCALAPPDATA%>\微软_VisualStudio_14.0Exp_ProjectTemplates。*

要部署项目工厂，安装程序必须具有管理员权限。 它在可视化工作室安装节点下部署模板： *.\微软可视化工作室 14.0\Common7_IDE_ProjectTemplates*。

## <a name="test-a-visual-studio-template"></a>测试可视化工作室模板
测试项目工厂以查看它是否使用 Visual Studio 模板创建项目层次结构。

1. 重置可视化工作室 SDK 实验实例。

    在[!INCLUDE[win7](../debugger/includes/win7_md.md)]：在 **"开始"** 菜单上，查找**微软视觉工作室/微软视觉工作室 SDK/Tools**文件夹，然后选择 **"重置 Microsoft 视觉工作室实验实例**"。

    在更高版本的 Windows 上：在 **"开始"** 屏幕上，键入 **"重置\<Microsoft 可视化工作室"版本>实验实例**。

2. 将显示命令提示窗口。 当您看到单词 **"按任意键继续"时**，单击**ENTER**。 窗口关闭后，打开视觉工作室。

3. 重建简单项目并开始调试。 出现实验实例。

4. 在实验实例中，创建一个简单的项目项目。 在 **"新项目"** 对话框中，选择 **"简单项目**"。

5. 您应该会看到一个新实例的简单项目。

    ![简单项目新实例](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")

    ![我的项目新实例](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")

## <a name="create-a-project-type-child-node"></a>创建项目类型子节点
您可以在 **"新项目"** 对话框中将子节点添加到项目类型节点。 例如，对于 SimpleProject 项目类型，可以具有控制台应用程序、窗口应用程序、Web 应用程序等的子节点。

子节点是通过更改项目文件和将输出子路径>\<子节点添加到\<ZipProject>元素来创建的。 在生成或部署期间复制模板时，每个子节点将成为项目模板文件夹的子文件夹。

本节演示如何为简单项目项目类型创建控制台子节点。

1. 将*\\模板\项目\简单项目\\*文件夹重命名为*\\模板\项目\控制台应用程序\\*。

2. 在 **"属性"** 窗口中，选择*\\\\模板\项目\控制台应用*文件夹中的所有五个文件，并确保**生成操作**设置为**ZipProject**。

3. 在 SimpleProject.vstemplate 文件中，在结束标记之前的\<模板数据>部分的末尾添加以下行。

    ```
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    ```

    这将导致控制台应用程序模板同时出现在控制台子节点和 SimpleProject 父节点中，该节点位于子节点上方一个级别。

4. 保存*简单项目.vstemplate*文件。

5. 在 *.csproj*文件中，\<将输出子路径>添加到每个 ZipProject 元素。 与以前一样卸载项目并编辑项目文件。

6. 找到\<ZipProject>元素。 到每个\<ZipProject>元素，\<添加一个输出子路径>元素，并给它值控制台。 邮编项目

    ```
    <ZipProject Include="Templates\Projects\ConsoleApp\AssemblyInfo.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\Program.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.myproj">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.vstemplate">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.ico">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    ```

7. 将此属性\<组>添加到项目文件中：

    ```
    <PropertyGroup>
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>
    </PropertyGroup>
    ```

8. 保存项目文件并重新加载项目。

## <a name="test-the-project-type-child-node"></a>测试项目类型子节点
测试修改后的项目文件，以查看**控制台**子节点是否显示在 **"新项目**"对话框中。

1. 运行**重置 Microsoft 视觉工作室实验实例**工具。

2. 重建简单项目并开始调试。 应出现实验实例

3. 在 **"新项目"** 对话框中，单击 **"简单项目**"节点。 **控制台应用程序**模板应显示在 **"模板"窗格中**。

4. 展开**简单项目**节点。 应显示**控制台**子节点。 **简单项目应用程序**模板继续显示在 **"模板"** 窗格中。

5. 单击 **"取消并**停止调试"。

    ![简单的项目汇总](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")

    ![简单的项目控制台节点](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")

## <a name="substitute-project-template-parameters"></a>替换项目模板参数
- [创建基本项目系统，第1部分](../extensibility/creating-a-basic-project-system-part-1.md)展示了如何覆盖`ProjectNode.AddFileFromTemplate`方法，以进行一种基本的模板参数替换。 本节介绍如何使用更复杂的 Visual Studio 模板参数。

在 **"新建项目**"对话框中使用 Visual Studio 模板创建项目时，模板参数将替换为字符串以自定义项目。 模板参数是一个特殊的令牌，以美元符号开始和结束，例如，$time$。 以下两个参数对于在基于模板的项目中启用自定义特别有用：

- $GUID[1-10]$被新的Guid取代。 您最多可以指定 10 个唯一 GUID，例如，$guid1 美元。

- $safeprojectname$是用户在 **"新项目"** 对话框中提供的名称，已修改以删除所有不安全的字符和空格。

  有关模板参数的完整列表，请参阅[模板参数](../ide/template-parameters.md)。

### <a name="to-substitute-project-template-parameters"></a>替换项目模板参数

1. 在*SimpleProjectNode.cs*文件中，删除 方法`AddFileFromTemplate`。

2. 在*\\模板\项目\ConsoleApp_SimpleProject.myproj*文件中，找到\<根命名空间>属性并将其值更改为 $safeprojectname$。

    ```
    <RootNamespace>$safeprojectname$</RootNamespace>
    ```

3. 在*\\模板_项目_简单项目_程序.cs*文件中，用以下代码替换文件的内容：

    ```
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace $safeprojectname$
    {
        [Guid("$guid1$")]
        public class $safeprojectname$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

4. 重建简单项目并开始调试。 应出现实验实例。

5. 创建新的 SimpleProject 控制台应用程序。 （在 **"项目类型"** 窗格中，选择 **"简单项目**"。 在**可视化工作室安装的模板**下，选择**控制台应用程序**。

6. 在新创建的项目中，打开*Program.cs*。 它的外观应如下所示（文件中的 GUID 值会有所不同。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace Console_Application1
    {
        [Guid("00000000-0000-0000-00000000-00000000)"]
        public class Console_Application1
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

## <a name="create-a-project-property-page"></a>创建项目属性页
可以为项目类型创建属性页，以便用户可以查看和更改基于模板的项目中的属性。 本节介绍如何创建与配置无关的属性页。 此基本属性页使用属性网格来显示您在属性页类中公开的公共属性。

从`SettingsPage`基类派生属性页类。 `SettingsPage`类提供的属性网格知道大多数原始数据类型，并知道如何显示它们。 此外，该`SettingsPage`类知道如何将属性值保存到项目文件。

通过在此部分创建的属性页，您可以更改和保存以下项目属性：

- AssemblyName

- OutputType

- 根命名空间。

1. 在*SimpleProjectPackage.cs*文件中，将此属性`ProvideObject`添加到`SimpleProjectPackage`类：

    ```
    [ProvideObject(typeof(GeneralPropertyPage))]
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

    这将属性页类`GeneralPropertyPage`与 COM 注册。

2. 在*SimpleProjectNode.cs*文件中，将这两个重写方法添加到`SimpleProjectNode`类：

    ```csharp
    protected override Guid[] GetConfigurationIndependentPropertyPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    protected override Guid[] GetPriorityProjectDesignerPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    ```

    这两种方法都返回属性页 GUID 的数组。 属性页 GUID 是数组中的唯一元素，因此 **"属性页"** 对话框将仅显示一个页面。

3. 将名为*GeneralPropertyPage.cs*的类文件添加到 SimpleProject 项目中。

4. 使用以下代码替换此文件的内容：

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Project;
    using System.ComponentModel;

    namespace SimpleProject
    {
        [ComVisible(true)]
        [Guid("6BC7046B-B110-40d8-9F23-34263D8D2936")]
        public class GeneralPropertyPage : SettingsPage
        {
            private string assemblyName;
            private OutputType outputType;
            private string defaultNamespace;

            public GeneralPropertyPage()
            {
                this.Name = "General";
            }

            [Category("AssemblyName")]
            [DisplayName("AssemblyName")]
            [Description("The output file holding assembly metadata.")]
            public string AssemblyName
            {
                get { return this.assemblyName; }
            }
            [Category("Application")]
            [DisplayName("OutputType")]
            [Description("The type of application to build.")]
            public OutputType OutputType
            {
                get { return this.outputType; }
                set { this.outputType = value; this.IsDirty = true; }
            }
            [Category("Application")]
            [DisplayName("DefaultNamespace")]
            [Description("Specifies the default namespace for added items.")]
            public string DefaultNamespace
            {
                get { return this.defaultNamespace; }
                set { this.defaultNamespace = value; this.IsDirty = true; }
            }

            protected override void BindProperties()
            {
                this.assemblyName = this.ProjectMgr.GetProjectProperty("AssemblyName", true);
                this.defaultNamespace = this.ProjectMgr.GetProjectProperty("RootNamespace", false);

                string outputType = this.ProjectMgr.GetProjectProperty("OutputType", false);
                this.outputType = (OutputType)Enum.Parse(typeof(OutputType), outputType);
            }

            protected override int ApplyChanges()
            {
                this.ProjectMgr.SetProjectProperty("AssemblyName", this.assemblyName);
                this.ProjectMgr.SetProjectProperty("OutputType", this.outputType.ToString());
                this.ProjectMgr.SetProjectProperty("RootNamespace", this.defaultNamespace);
                this.IsDirty = false;

                return VSConstants.S_OK;
            }
        }
    }
    ```

    该`GeneralPropertyPage`类公开三个公共属性"程序集名称"、输出类型和根命名空间。 由于 AssemblyName 没有设置方法，因此它显示为只读属性。 输出类型是枚举常量，因此显示为下拉列表。

    基`SettingsPage`类提供`ProjectMgr`以保留属性。 该方法`BindProperties`用于`ProjectMgr`检索持久化属性值并设置相应的属性。 该方法`ApplyChanges`用于`ProjectMgr`获取属性的值并将其保存到项目文件中。 属性集方法设置为`IsDirty`true 以指示必须保留属性。 保存项目或解决方案时会发生持久性。

5. 重建简单项目解决方案并开始调试。 应出现实验实例。

6. 在实验实例中，创建新的 SimpleProject 应用程序。

7. Visual Studio 调用项目工厂，使用 Visual Studio 模板创建项目。 新的*Program.cs*文件在代码编辑器中打开。

8. 右键单击**解决方案资源管理器**中的项目节点，**然后单击属性**。 **属性页** ”对话框。

    ![简单的项目属性页面](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")

## <a name="test-the-project-property-page"></a>测试项目属性页
现在，您可以测试是否可以修改和更改属性值。

1. 在**MyConsole 应用程序属性页**对话框中，将**默认命名空间**更改为 **"我的应用程序**"。

2. 选择 **"输出类型"** 属性，然后选择**类库**。

3. 单击“应用”****，然后单击“确定”****。

4. 重新打开 **"属性页"** 对话框，并验证所做的更改是否已保留。

5. 关闭 Visual Studio 的实验实例。

6. 重新打开实验实例。

7. 重新打开 **"属性页"** 对话框，并验证所做的更改是否已保留。

8. 关闭 Visual Studio 的实验实例。
    ![关闭实验实例](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")
