---
title: 为 Web 性能测试结果查看器创建加载项
ms.date: 10/20/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, Visual Studio Add-in
- Visual Studio Add-in, Web performance tests
ms.assetid: 1118c604-4b1b-4b21-a04e-45995b676fa8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e2330f5d1c47c9fc3cc578f286be005710b08f59
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68918205"
---
# <a name="how-to-create-an-add-in-for-the-web-performance-test-results-viewer"></a>如何：为 Web 性能测试结果查看器创建加载项

可以使用以下命名空间来扩展“Web 性能测试结果查看器”  的 UI：

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>

- <xref:Microsoft.VisualStudio.TestTools.WebTesting>

此外，还需要添加对位于 %ProgramFiles(x86)%\Microsoft Visual Studio\\\<version>\Enterprise\Common7\IDE\PrivateAssemblies 文件夹中的 LoadTestPackage DLL 的引用  。

若要扩展“Web 性能测试结果查看器”  的 UI，必须创建 Visual Studio 加载项和用户控件。 下面的过程说明如何创建加载项、用户控件以及如何实现扩展“Web 性能测试结果查看器”  的 UI 所需的类。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="create-or-open-a-solution-that-contains-an-aspnet-web-application-and-a-web-performance-and-load-test-project"></a>创建或打开包含 ASP.NET Web 应用程序、Web 性能和负载测试项目的解决方案

### <a name="to-prepare-for-extending-the-web-performance-test-results-viewer"></a>准备扩展 Web 性能测试结果查看器

创建或打开一个可用来进行试验的非生产解决方案，该解决方案包含一个 ASP.NET Web 应用程序以及一个带有针对 ASP.NET Web 应用程序的一个或多个 Web 性能测试的 Web 性能和负载测试项目。

> [!NOTE]
> 要创建 ASP.NET Web 应用程序和包含 Web 性能测试的 Web 性能和负载测试项目，请遵循[如何：创建 Web 服务测试](../test/how-to-create-a-web-service-test.md)和[生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)中的步骤。

## <a name="create-a-visual-studio-add-in"></a>创建 Visual Studio 外接程序

外接程序是在 Visual Studio 集成开发环境 (IDE) 中运行的已编译的 DLL。 编译有助于保护知识产权和提高性能。 虽然可以手动创建外接程序，但可能会发现使用“外接程序向导”更为简便  。 此向导创建一个功能全面但却很基本的外接程序，创建完该程序后可立即运行它。 “外接程序向导”生成基本程序后，可向其添加代码并对其进行自定义  。

“外接程序向导”让你可以为外接程序提供显示名称和说明  。 这两项内容都将出现在“外接程序管理器”中  。 还可以选择让向导生成代码，用于向“工具”菜单中添加可打开外接程序的命令  。 也可以选择为外接程序显示一个自定义“关于”对话框  。 向导完成时，将生成只有一个实现外接程序的类的新项目。 该类名为“Connect”。

本主题末尾将使用外接程序管理器  。

### <a name="to-create-an-add-in-by-using-the-add-in-wizard"></a>使用“外接程序向导”创建外接程序

1. 在解决方案资源管理器中，右键单击该解决方案，选择“添加”，然后选择“新项目”    。

2. 创建新的“Visual Studio 加载项”项目  。

    此时 Visual Studio“外接程序向导”将启动  。

3. 选择“下一步”  。

4. 在“选择编程语言”页上，选择要用于编写外接程序的编程语言  。

   > [!NOTE]
   > 本主题使用 Visual C# 编写代码示例。

5. 在“选择应用程序主机”页上，选择“Visual Studio”并清除“Visual Studio 宏”    。

6. 选择“下一步”  。

7. 在“输入名称和说明”页中键入外接程序的名称和说明  。

     创建了外接程序后，其名称和说明将显示在“外接程序管理器”的“可用外接程序”列表中   。 向外接程序的说明中添加足够的详细信息，以便用户能够了解外接程序的功能、工作方式等信息。

8. 选择“下一步”  。

9. 在“选择外接程序选项”页上，选择“我希望我的外接程序在主机应用程序启动时加载”   。

10. 清除其余复选框。

11. 在“选择‘帮助’中的‘关于’信息”页上，可指定是否将有关外接程序的信息显示在“关于”对话框中   。 如果确实希望显示此信息，则选中“是的，我希望我的外接程序提供‘关于’对话框信息”复选框  。

     可以添加到 Visual Studio 的“关于”对话框中的信息包括版本号、支持详细信息和授权数据等信息  。

12. 选择“下一步”  。

13. 所选的选项将显示在“摘要”页上以供检查  。 如果满意，请选择“完成”以创建外接程序  。 若要更改某些内容，请选择“返回”按钮  。

     此时将创建新的解决方案和项目，并且新外接程序的 Connect.cs 文件将显示在代码编辑器中   。

     在完成下面的创建将由此 WebPerfTestResultsViewerAddin 项目引用的用户控件的过程后，将向 Connect.cs 文件添加代码  。

    创建了外接程序后，必须先向 Visual Studio 注册此外接程序，然后才能在“外接程序管理器”中激活它  。 使用具有 .addin 文件扩展名的 XML 文件来执行此操作  。

    .addin 文件描述了 Visual Studio 在外接程序管理器中显示外接程序所需的信息   。 启动 Visual Studio 时，它会查找 .addin 文件位置，获取任何可用的 .addin 文件   。 如果找到相应文件，则会读取 XML 文件，并向“外接程序管理器”提供在单击外接程序进行启动时所需的信息  。

    使用外接程序向导创建外接程序时，会自动创建一个 .addin 文件   。

### <a name="add-in-file-locations"></a>外接程序文件位置

外接程序向导会自动创建 .addin 文件的两个副本，如下所示   ：

|**.Addin 文件位置**|**说明**|
|-|----------------------------|-|
|根项目文件夹|用于部署外接程序项目。 包含在项目中以方便编辑，并使用本地路径安装以进行 XCopy 式部署。|
|外接程序文件夹|用于在调试环境中运行外接程序。 应该始终指向当前生成配置的输出路径。|

## <a name="create-a-windows-form-control-library-project"></a>创建 Windows 窗体控件库项目

在前面过程中创建的 Visual Studio 外接程序将引用 Windows 窗体控件库项目来创建 <xref:System.Windows.Forms.UserControl> 类的实例。

### <a name="to-create-a-control-to-be-used-in-the-web-test-results-viewer"></a>创建要在 Web 测试结果查看器中使用的控件

1. 在解决方案资源管理器中，右键单击该解决方案，选择“添加”，然后选择“新项目”    。

2. 创建新的“Windows 窗体控件库”项目  。

3. 从“工具箱”中将 <xref:System.Windows.Forms.DataGridView> 拖动到 userControl1 的图面上  。

4. 单击 <xref:System.Windows.Forms.DataGridView> 的右上角的操作标记字形（![智能标记字形](../test/media/vs_winformsmttagglyph.gif)），并按照以下步骤操作：

    1. 选择“在父容器中停靠”  。

    2. 清除“启用添加”、“启用编辑”、“启用删除”和“启用列重新排序”复选框     。

    3. 选择“添加列”  。

         随即出现“添加列”对话框  。

    4. 在“类型”下拉列表中，选择“DataGridViewTextBoxColumn”   。

    5. 清除“标头文本”中的文本“Column1”  。

    6. 选择“添加”  。

    7. 选择“关闭”  。

5. 在“属性”窗口中，将 <xref:System.Windows.Forms.DataGridView> 的“(Name)”属性更改为“resultControlDataGridView”    。

6. 右键单击设计图面并选择“查看代码”  。

     UserControl1.cs 文件将显示在代码编辑器中   。

7. 将实例化的 <xref:System.Windows.Forms.UserControl> 类的名称从 UserContro1 更改为 resultControl：

    ```csharp
    namespace WebPerfTestResultsViewerControl
    {
        public partial class resultControl : UserControl
        {
            public resultControl()
            {
                InitializeComponent();
            }
    ```

     在下一过程中，将向 WebPerfTestResultsViewerAddin 项目的引用 resultControl 类的 Connect.cs 文件添加代码  。

     稍后将向 Connect.cs 文件添加一些附加代码  。

## <a name="add-code-to-the-webperftestresultsvieweraddin"></a>向 WebPerfTestResultsViewerAddin 添加代码

1. 在解决方案资源管理器中，右键单击 WebPerfTestResultsViewerAddin 项目中的“引用”节点，然后选择“添加引用”    。

2. 在“添加引用”对话框中，选择“.NET”选项卡   。

3. 向下滚动并选择“Microsoft.VisualStudio.QualityTools.WebTestFramework”和“System.Windows.Forms”   。

4. 选择 **“确定”** 。

5. 再次右键单击“引用”节点，然后选择“添加引用”   。

6. 在“添加引用”对话框中，选择“浏览”选项卡   。

7. 选择“查找范围”下拉列表，并导航到 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\PrivateAssemblies，然后选择 Microsoft.VisualStudio.QualityTools.LoadTestPackage.dll 文件    。

8. 选择 **“确定”** 。

9. 右键单击“WebPerfTestResultsViewerAddin”项目节点，然后选择“添加引用”  。

10. 在“添加引用”对话框中，选择“项目”选项卡   。

11. 在“项目名称”下，选择“WebPerfTestResultsViewerControl”项目，然后选择“确定”    。

12. 如果 Connect.cs 文件仍未打开，请在解决方案资源管理器中，右键单击“WebPerfTestResultsViewerAddin”项目中的“Connect.cs”文件，然后选择“查看代码”     。

13. 在 Connect.cs 文件中，添加以下 Using 语句  ：

    ```csharp
    using System.IO;
    using System.Windows.Forms;
    using System.Collections.Generic;
    using Microsoft.VisualStudio.TestTools.LoadTesting;
    using Microsoft.VisualStudio.TestTools.WebTesting;
    using WebPerfTestResultsViewerControl;
    ```

14. 向下滚动到 Connect.cs 文件的底端  。 如果打开“Web 性能测试结果查看器”  的多个实例，则需要为 <xref:System.Windows.Forms.UserControl> 添加 GUID 列表。 稍后您将添加使用此列表的代码。

     稍后在将编码的 OnDiscconection 方法中使用另一个字符串列表。

    ```csharp
    private DTE2 _applicationObject;
    private AddIn _addInInstance;

    private Dictionary<Guid, List<UserControl>> m_controls = new Dictionary<Guid, List<UserControl>>();        private List<string> temporaryFilePaths = new List<string>();
    ```

15. Connect.cs 文件从 <xref:Extensibility.IDTExtensibility2> 类对名为 Connect 的类进行实例化，还包括一些用于实现 Visual Studio 外接程序的方法  。 其中一种方法为 OnConnection 方法，用于接收有关外接程序正在加载的通知。 在 OnConnection 方法中，你将使用 LoadTestPackageExt 类为“Web 性能测试结果查看器”  创建扩展性包。 将以下代码添加到 OnConnection 方法中：

    ```csharp
    public void OnConnection(object application, ext_ConnectMode connectMode, object addInInst, ref Array custom)
                {
                _applicationObject = (DTE2)application;
                _addInInstance = (AddIn)addInInst;

                // Create a load test packge extensibility class.            LoadTestPackageExt loadTestPackageExt = _applicationObject.GetObject("Microsoft.VisualStudio.TestTools.LoadTesting.LoadTestPackageExt") as LoadTestPackageExt;            // Process open windows.            foreach (WebTestResultViewer webTestResultViewer in loadTestPackageExt.WebTestResultViewerExt.ResultWindows)            {                WindowCreated(webTestResultViewer);            }            // Create event handlers.            loadTestPackageExt.WebTestResultViewerExt.WindowCreated += new EventHandler<WebTestResultViewerExt.WindowCreatedEventArgs>(WebTestResultViewerExt_WindowCreated);            loadTestPackageExt.WebTestResultViewerExt.WindowClosed += new EventHandler<WebTestResultViewerExt.WindowClosedEventArgs>(WebTesResultViewer_WindowClosed);            loadTestPackageExt.WebTestResultViewerExt.SelectionChanged += new EventHandler<WebTestResultViewerExt.SelectionChangedEventArgs>(WebTestResultViewer_SelectedChanged);
            }
    ```

16. 将下面的代码添加到 connect 类，以便为在 OnConnection 方法中添加的 loadTestPackageExt.WebTestResultViewerExt.WindowCreated 事件处理程序和 WebTestResultViewerExt_WindowCreated 方法调用的 WindowCreated 方法创建 WebTestResultViewerExt_WindowCreated 方法。

    ```csharp
            void WebTestResultViewerExt_WindowCreated(object sender, WebTestResultViewerExt.WindowCreatedEventArgs e)
            {
                // New control added to new result viewer window.
                WindowCreated(e.WebTestResultViewer);
            }

    private void WindowCreated(WebTestResultViewer viewer)        {            // Instantiate an instance of the resultControl referenced in the WebPerfTestResultsViewerControl project.
                resultControl resultControl = new resultControl();            // Add to the dictionary of open playback windows.            System.Diagnostics.Debug.Assert(!m_controls.ContainsKey(viewer.TestResultId));            List<UserControl> userControls = new List<UserControl>();            userControls.Add(resultControl);            // Add Guid to the m_control List to manage Result viewers and controls.            m_controls.Add(viewer.TestResultId, userControls);            // Add tabs to the playback control.            resultControl.Dock = DockStyle.Fill;            viewer.AddResultPage(new Guid(), "Sample", resultControl);        }
    ```

17. 将下面的代码添加到 connect 类，以便为在 OnConnection 方法中添加的 loadTestPackageExt.WebTestResultViewerExt.SelectionChanged 事件处理程序创建 WebTestResultViewer_SelectedChanged 方法：

    ```csharp
    void WebTestResultViewer_SelectedChanged(object sender, WebTestResultViewerExt.SelectionChangedEventArgs e)
    {
        foreach (UserControl userControl in m_controls[e.TestResultId])            {                // Update the userControl in each result viewer.                resultControl resultControl = userControl as resultControl;                if (resultControl != null)                    // Call the resultControl's Update method (This will be added in the next procedure).                    resultControl.Update(e.WebTestRequestResult);            }
    }
    ```

18. 将下面的代码添加到 connect 类，以便为在 OnConnection 方法中添加的 loadTestPackageExt.WebTestResultViewerExt.WindowClosed 事件处理程序创建 WebTesResultViewer_WindowClosed 方法：

    ```csharp
    void WebTesResultViewer_WindowClosed(object sender, WebTestResultViewerExt.WindowClosedEventArgs e)
    {
        if (m_controls.ContainsKey(e.WebTestResultViewer.TestResultId))
        {
            m_controls.Remove(e.WebTestResultViewer.TestResultId);
        }
    }
    ```

     现在 Visual Studio 外接程序的代码已完成，你需要向 WebPerfTestResultsViewerControl 项目中的 resultControl 添加 Update 方法。

## <a name="add-code-to-the-webperftestresultsviewercontrol"></a>向 WebPerfTestResultsViewerControl 添加代码

1. 在解决方案资源管理器中右键单击 WebPerfTestResultsViewerControl 项目节点，然后选择“属性”   。

2. 选择“应用程序”选项卡，再选择“目标框架”下拉列表，然后选择“.NET Framework 4”（或更高版本）    。 关闭“属性”窗口  。

   为支持扩展“Web 性能测试结果查看器”  所需的 DLL 引用，此操作是必需的。

3. 在解决方案资源管理器中，在 WebPerfTestResultsViewerControl 项目中右键单击“引用”节点，然后选择“添加引用”    。

4. 在“添加引用”对话框中，单击“.NET”选项卡   。

5. 向下滚动并选择“Microsoft.VisualStudio.QualityTools.WebTestFramework”  。

6. 选择 **“确定”** 。

7. 在 UserControl1.cs 文件中，添加以下 Using 语句  ：

    ```csharp
    using Microsoft.VisualStudio.TestTools.WebTesting;
    using Microsoft.VisualStudio.TestTools.WebTesting.Rules;
    ```

8. 添加 Update 方法，然后从 Connect.cs 文件中的 WebPerfTestResultsViewerAddin WebTestResultViewer_SelectedChanged 方法调用该方法并传递 WebTestRequestResult  。 Update 方法使用在 WebTestRequestResult 中传递给它的各种属性填充 DataGridView。

    ```csharp
    public void Update(WebTestRequestResult WebTestResults)
            {
                // Clear the DataGridView when a request is selected.
                resultControlDataGridView.Rows.Clear();
                // Populate the DataGridControl with properties from the WebTestResults.
                this.resultControlDataGridView.Rows.Add("Request: " + WebTestResults.Request.Url.ToString());
                this.resultControlDataGridView.Rows.Add("Response: " + WebTestResults.Response.ResponseUri.ToString());
                foreach (RuleResult ruleResult in WebTestResults.ExtractionRuleResults)
                {
                    this.resultControlDataGridView.Rows.Add("Extraction rule results: " + ruleResult.Message.ToString());
                }
                foreach (RuleResult ruleResult in WebTestResults.ValidationRuleResults)
                {
                    this.resultControlDataGridView.Rows.Add("Validation rule results: " + ruleResult.Message.ToString());
                }
                foreach (WebTestError webTestError in WebTestResults.Errors)
                {
                    this.resultControlDataGridView.Rows.Add("Error: " + webTestError.ErrorType.ToString() + " " + webTestError.ErrorSubtype.ToString() + " " + webTestError.ExceptionText.ToString());
                }
            }
    ```

## <a name="build-the-solution"></a>生成解决方案

- 在“生成”菜单上，选择“生成解决方案”   。

## <a name="register-the-webperftestresultsvieweraddin-add-in"></a>注册 WebPerfTestResultsViewerAddin 外接程序

1. 在“工具”菜单上，选择“外接程序管理器”   。

2. 随即出现“外接程序管理器”对话框  。

3. 在“可用外接程序”列中，选中 WebPerfTestResultsViewerAddin 外接程序对应的复选框，然后清除“启动”列和“命令行”列下方的复选框    。

4. 选择 **“确定”** 。

## <a name="run-the-web-performance-test-using-the-web-test-results-viewer"></a>使用 Web 性能测试结果查看器运行 Web 性能测试

1. 运行 Web 性能测试，你将会看到在“Web 性能测试结果查看器”  中显示的 WebPerfTestResultsViewerAddin 加载项的标题为“Sample”的新选项卡。

2. 选择此选项卡可查看 DataGridView 中显示的属性。

## <a name="net-security"></a>.NET 安全

为了通过防止恶意外接程序自动激活来改进安全性，Visual Studio 在名为“外接程序/宏的安全性”的“工具选项”页中提供了一些设置   。

另外，通过该选项页，可指定供 Visual Studio 在其中搜索 .AddIn 注册文件的文件夹  。 通过此方式，可对可读取 .AddIn 注册文件的位置进行限制，从而提高安全性  。 这可防止无意中使用 .AddIn 恶意文件  。

**外接程序安全性设置**

选项页中外接程序安全性的设置如下所示：

- **允许加载外接程序组件。** 默认情况下选中此选项。 在选中时，允许在 Visual Studio 中加载外接程序。 在未选中时，禁止在 Visual Studio 中加载外接程序。

- **允许从 URL 加载外接程序组件。** 默认情况下不选择此选项。 在选中时，可从外部网站加载外接程序。 在未选中时，禁止在 Visual Studio 中加载远程外接程序。 如果某个外接程序由于某种原因无法加载，则无法从网站加载它。 此设置只控制外接程序 DLL 的加载。 .Addin 注册文件必须始终位于本地系统上  。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.UserControl>
- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.DataGrid>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)