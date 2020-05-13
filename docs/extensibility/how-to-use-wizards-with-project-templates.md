---
title: 如何：使用向导来处理项目模板
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- project templates [Visual Studio], wizards
- Visual Studio templates, wizards
- wizards [Visual Studio], project templates
- templates [Visual Studio], wizards
- IWizard interface
ms.assetid: 47ee26cf-67b7-4ff1-8a9d-ab11a725405c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4d2dc057dfa518bb52c6ba4d30cd0f3e0a822cfd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710535"
---
# <a name="how-to-use-wizards-with-project-templates"></a>如何：将向导与项目模板一起使用

Visual Studio 提供了 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，可实现该接口来在用户从模板创建项目时运行自定义代码。

项目模板自定义可用于显示自定义 UI，用于收集用户输入以自定义模板、向模板添加其他文件或项目上允许的任何其他操作。

在<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>创建项目时，在不同时间调用接口方法，从用户单击 **"新项目**"对话框上的 **"确定"** 开始。 命名接口的每个方法来描述调用它的点。 例如，Visual Studio<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A>在开始创建项目时立即调用，使其成为编写自定义代码以收集用户输入的良好位置。

## <a name="create-a-project-template-project-with-a-vsix-project"></a>使用 VSIX 项目创建项目模板项目

开始使用项目模板项目创建自定义模板，该项目是可视化工作室 SDK 的一部分。 在此过程中，我们将使用 C# 项目模板项目，但也有 Visual Basic 项目模板项目。 然后，将 VSIX 项目添加到包含项目模板项目的解决方案。

1. 创建 C# 项目模板项目（在可视化工作室中，选择 **"文件** > **新项目** > **"并**搜索"项目模板"）。 将其命名为 **"我的项目模板**"。

   > [!NOTE]
   > 系统可能会要求您安装可视化工作室 SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

2. 在项目模板项目相同的解决方案中添加新的 VSIX 项目（在**解决方案资源管理器**中，选择解决方案节点，右键单击，然后选择 **"添加新** > **项目**"并搜索"vsix"）。 将其命名为 **"我的项目向导"。**

3. 将 VSIX 项目设置为启动项目。 在**解决方案资源管理器**中，选择 VSIX 项目节点，右键单击，然后选择"**设置为启动项目**"。

4. 将模板项目添加为 VSIX 项目的资产。 在**解决方案资源管理器**中，在 VSIX 项目节点下，查找*源.扩展.vsixmanifest*文件。 双击它以在清单编辑器中打开它。

5. 在清单编辑器中，选择窗口左侧的"**资产**"选项卡。

6. 在"**资产**"选项卡中，选择 **"新建**"。 在"**添加新资产**"窗口中，对于"类型"字段，选择**Microsoft.VisualStudio.ProjectTemplate**。 在 **"源"** 字段中，选择**当前解决方案中的项目**。 在 **"项目"** 字段中，选择 **"我的项目模板**"。 然后单击“确定”****。

7. 生成解决方案并启动调试。 将出现 Visual Studio 的第二个实例。 （这可能需要几分钟的时间。）

8. 在 Visual Studio 的第二个实例中，尝试使用新模板创建新**项目**（**文件** > **新项目** > ，搜索"我的项目"）。 新项目应与名为**Class1**的类一起出现。 您现在已创建自定义项目模板！ 现在停止调试。

## <a name="create-a-custom-template-wizard"></a>创建自定义模板向导

此过程演示如何创建在创建项目之前打开 Windows 窗体的自定义向导。 该窗体允许用户添加在项目创建期间添加到源代码的自定义参数值。

1. 设置 VSIX 项目以允许它创建程序集。

2. 在**解决方案资源管理器中**，选择 VSIX 项目节点。 在**解决方案资源管理器**下方 ，应看到 **"属性"** 窗口。 否则，请选择 **"查看** > **属性窗口**"或按**F4**。 在 **"属性"** 窗口中，选择以下字段以`true`：

   - **在 VSIX 容器中包括程序集**

   - **在 VSIX 容器中包括调试符号**

   - **在本地 VSIX 部署中包括调试符号**

3. 将程序集作为资产添加到 VSIX 项目中。 打开*源.扩展.vsixmanifest*文件并选择"**资产**"选项卡。在 **"添加新资产**"窗口中，对于**类型**，请选择**Microsoft.VisualStudio.Assembly**，对于**源**选择**当前解决方案中的项目**，并且对于**项目**选择 **"我的项目向导**"。

4. 添加以下对 VSIX 项目的引用。 （在 **"解决方案资源管理器**"中，在 VSIX 项目节点下，选择 **"引用**"，右键单击，然后选择 **"添加参考**"。"在"**添加参考**"对话框中，在 **"框架"** 选项卡中，查找**System.Windows 窗体**程序集并选择它。 还要查找并选择**系统和****系统.绘图**程序集。 现在选择 **"扩展"** 选项卡。找到**EnvDTE**程序集并选择它。 还可以找到**Microsoft.VisualStudio.模板向导界面**程序集并选择它。 单击“确定”。

5. 向 VSIX 项目添加向导实现的类。 （在**解决方案资源管理器**中，右键单击 VSIX 项目节点，然后选择 **"添加**"，然后选择 **"新建项目**"，然后选择**类**。）命名类**向导实现**。

6. 将*WizardImplementationClass.cs*文件中的代码替换为以下代码：

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.TemplateWizard;
   using System.Windows.Forms;
   using EnvDTE;

   namespace MyProjectWizard
   {
       public class WizardImplementation:IWizard
       {
           private UserInputForm inputForm;
           private string customMessage;

           // This method is called before opening any item that
           // has the OpenInEditor attribute.
           public void BeforeOpeningFile(ProjectItem projectItem)
           {
           }

           public void ProjectFinishedGenerating(Project project)
           {
           }

           // This method is only called for item templates,
           // not for project templates.
           public void ProjectItemFinishedGenerating(ProjectItem
               projectItem)
           {
           }

           // This method is called after the project is created.
           public void RunFinished()
           {
           }

           public void RunStarted(object automationObject,
               Dictionary<string, string> replacementsDictionary,
               WizardRunKind runKind, object[] customParams)
           {
               try
               {
                   // Display a form to the user. The form collects
                   // input for the custom message.
                   inputForm = new UserInputForm();
                   inputForm.ShowDialog();

                   customMessage = UserInputForm.CustomMessage;

                   // Add custom parameters.
                   replacementsDictionary.Add("$custommessage$",
                       customMessage);
               }
               catch (Exception ex)
               {
                   MessageBox.Show(ex.ToString());
               }
           }

           // This method is only called for item templates,
           // not for project templates.
           public bool ShouldAddProjectItem(string filePath)
           {
               return true;
           }
       }
   }
   ```

    此代码中引用**的用户输入形式**将在以后实现。

    该`WizardImplementation`类包含<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>的每个成员的方法实现。 在此示例中，只有 方法<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A>执行任务。 所有其他方法要么不执行任何操作，`true`要么返回 。

    该方法<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A>接受四个参数：

   - 可以<xref:System.Object>强制转换为根<xref:EnvDTE._DTE>对象的参数，以便自定义项目。

   - 包含<xref:System.Collections.Generic.Dictionary%602>模板中所有预定义参数的集合的参数。 有关模板参数的详细信息，请参阅[模板参数](../ide/template-parameters.md)。

   - 包含有关<xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind>正在使用哪种模板的信息的参数。

   - 包含<xref:System.Object>由 Visual Studio 传递给向导的一组参数的数组。

     本示例将用户输入窗体中的参数值添加到参数。 <xref:System.Collections.Generic.Dictionary%602> 项目中`$custommessage$`参数的每个实例都将替换为用户输入的文本。

7. 现在创建**用户输入表单**。 在*WizardImplementation.cs*文件中，在`WizardImplementation`类结束后添加以下代码。

   ```csharp
   public partial class UserInputForm : Form
       {
           private static string customMessage;
           private TextBox textBox1;
           private Button button1;

           public UserInputForm()
           {
               this.Size = new System.Drawing.Size(155, 265);

               button1 = new Button();
               button1.Location = new System.Drawing.Point(90, 25);
               button1.Size = new System.Drawing.Size(50, 25);
               button1.Click += button1_Click;
               this.Controls.Add(button1);

               textBox1 = new TextBox();
               textBox1.Location = new System.Drawing.Point(10, 25);
               textBox1.Size = new System.Drawing.Size(70, 20);
               this.Controls.Add(textBox1);
           }
           public static string CustomMessage
           {
               get
               {
                   return customMessage;
               }
               set
               {
                   customMessage = value;
               }
           }
           private void button1_Click(object sender, EventArgs e)
           {
               customMessage = textBox1.Text;
               this.Close();
           }
       }
   ```

    用户输入窗体提供了用于输入自定义参数的简单窗体。 该窗体包含一个名称为`textBox1`的文本框和名为`button1`的按钮。 单击按钮时，文本框中的文本将存储在 参数中`customMessage`。

## <a name="connect-the-wizard-to-the-custom-template"></a>将向导连接到自定义模板

为了使自定义项目模板使用自定义向导，您需要对向导程序集进行签名，并将一些行添加到自定义项目模板中，以便知道在创建新项目时在哪里可以找到向导实现。

1. 对程序集进行签名。 在**解决方案资源管理器**中，选择 VSIX 项目，右键单击，然后选择 **"项目属性**"。

2. 在"**项目属性**"窗口中，在 **"签名**"选项卡中选择"**签名**"选项卡，选中 **"对程序集进行签名**"。 在 **"选择强名称键文件"字段中**，选择**\<"新>**"。 在 **"创建强名称键"** 窗口中，在 **"键文件名**"字段中，键入**key.snk**。 使用密码字段取消选中 **"保护我的密钥文件**"。

3. 在**解决方案资源管理器**中，选择 VSIX 项目并找到 **"属性"** 窗口。

4. 将 **"将生成输出复制到输出目录"** 字段设置为**true**。 这允许在重建解决方案时将程序集复制到输出目录中。 它仍然包含在`.vsix`文件中。 您需要查看程序集，以便找出其签名密钥。

5. 重新生成解决方案。

6. 您现在可以在 MyProjectWizard 项目目录中找到 key.snk 文件（*\<您的磁盘位置>_MyProjectTemplate_MyProjectWizard_key.snk）。* 复制*密钥.snk*文件。

7. 转到输出目录并找到程序集（*\<您的磁盘位置>_MyProjectTemplate/MyProjectWizard_bin_Debug_MyProjectWizard.dll）。* 在此处粘贴*密钥.snk*文件。 （这不是绝对必要的，但它将使以下步骤更容易。

8. 打开命令窗口，并更改为在其中创建程序集的目录。

9. 查找*sn.exe*签名工具。 例如，在 Windows 10 64 位操作系统上，典型的路径如下：

     *C：\程序文件 （x86）\微软 SDK\Windows\v10.0A\bin_NETFX 4.6.1 工具*

     如果找不到该工具，请尝试在命令窗口中运行 **/R . sn.exe 的位置**。 记下路径。

10. 从*key.snk*文件中提取公钥。 在命令窗口中，键入

     **\<sn.exe>\sn.exe-p 键.snk outfile.key 的位置。**

     如果目录名称中有空格，不要忘记用引号环绕*sn.exe*的路径！

11. 从外文件获取公钥令牌：

     **\<sn.exe>\sn.exe-t outfile.key 的位置。**

     再次，不要忘记引号。 您应该在输出中看到如下所示的行

     **公钥令牌是\<令牌>**

     记下此值。

12. 将对自定义向导的引用添加到项目模板的 *.vstemplate*文件中。 在**解决方案资源管理器**中，找到名为*MyProjectTemplate.vstemplate*的文件，然后打开它。 \<在"模板内容>"部分结束后，添加以下部分：

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     **其中 MyProjectWizard**是程序集的名称，**令牌**是您在上一步中复制的令牌。

13. 保存项目中的所有文件并重新生成。

## <a name="add-the-custom-parameter-to-the-template"></a>将自定义参数添加到模板

在此示例中，用作模板的项目显示在自定义向导的用户输入窗体中指定的消息。

1. 在**解决方案资源管理器**中，转到**MyProjectTemplate**项目并打开*Class1.cs*。

2. 在`Main`应用程序的方法中，添加以下代码行。

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    当从`$custommessage$`模板创建项目时，参数将替换为在用户输入窗体中输入的文本。

下面是完整代码文件，在该文件已导出到模板之前。

```csharp
using System;
using System.Collections.Generic;
$if$ ($targetframeworkversion$ >= 3.5)using System.Linq;
$endif$using System.Text;

namespace $safeprojectname$
{
    public class Class1
    {
          static void Main(string[] args)
          {
               Console.WriteLine("$custommessage$");
          }
    }
}
```

## <a name="use-the-custom-wizard"></a>使用自定义向导

现在，您可以使用模板创建项目并使用自定义向导。

1. 重建解决方案并开始调试。 将显示 Visual Studio 的第二个实例。

2. 创建新的 MyProjectTemplate 项目。 （**文件** > **新项目** > **Project**）。

3. 在 **"新项目**"对话框中，搜索"我的项目"以查找模板、键入名称，然后单击"**确定**"。

     向导用户输入窗体将打开。

4. 键入自定义参数的值，然后单击该按钮。

     向导用户输入窗体将关闭，并且从模板创建项目。

5. 在**解决方案资源管理器**中，右键单击源代码文件，然后单击 **"查看代码**"。

     `$custommessage$`已替换为向导用户输入窗体中输入的文本的通知。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [自定义模板](../ide/customizing-project-and-item-templates.md)
- [向导扩展元素（可视化工作室模板）](../extensibility/wizardextension-element-visual-studio-templates.md)
- [视觉工作室模板中的 NuGet 包](/nuget/visual-studio-extensibility/visual-studio-templates)
