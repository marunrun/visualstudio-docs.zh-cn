---
title: 将搜索添加到工具窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, adding search
ms.assetid: f78c4892-8060-49c4-8ecd-4360f1b4d133
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9112a3368ba604c4291f9018e763022e953c4fc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740146"
---
# <a name="add-search-to-a-tool-window"></a>将搜索添加到工具窗口
在扩展中创建或更新工具窗口时，可以添加 Visual Studio 中其他位置显示的相同搜索功能。 此功能包括以下功能：

- 始终位于工具栏自定义区域中的搜索框。

- 覆盖在搜索框本身上的进度指示器。

- 一旦输入每个字符（即时搜索）或仅在选择**Enter**键（按需搜索）后，才能够显示结果。

- 显示您最近搜索的术语的列表。

- 按特定字段或搜索目标的各个方面筛选搜索的能力。

通过本演练，您将学习如何执行以下任务：

1. 创建 VSPackage 项目。

2. 创建包含具有只读文本框的用户控件的工具窗口。

3. 向工具窗口添加搜索框。

4. 添加搜索实现。

5. 启用进度栏的即时搜索和显示。

6. 添加**匹配案例**选项。

7. 添加**仅搜索偶数行**筛选器。

## <a name="to-create-a-vsix-project"></a>创建 VSIX 项目

1. 使用名为**TestSearch**`TestToolWindowSearch`的工具窗口创建名为的 VSIX 项目。 如果需要帮助执行此操作，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="to-create-a-tool-window"></a>创建工具窗口

1. 在项目中`TestToolWindowSearch`，打开*TestSearchControl.xaml*文件。

2. 将现有`<StackPanel>`块替换为以下块，该块向工具窗口中的 块<xref:System.Windows.Controls.TextBox><xref:System.Windows.Controls.UserControl>添加只读。

    ```xaml
    <StackPanel Orientation="Vertical">
        <TextBox Name="resultsTextBox" Height="800.0"
            Width="800.0"
            IsReadOnly="True">
        </TextBox>
    </StackPanel>
    ```

3. 在*TestSearchControl.xaml.cs*文件中，添加以下使用指令：

    ```csharp
    using System.Text;
    ```

4. 删除`button1_Click()`方法。

     在**测试搜索控制**类中，添加以下代码。

     此代码添加了名为<xref:System.Windows.Controls.TextBox>**"搜索结果文本Box"** 的公共属性和名为 **"搜索内容"** 的公共字符串属性。 在构造函数中，Search结果文本Box 设置为文本框，并且 SearchContent 被初始化为一组新行分隔的字符串。 文本框的内容也会初始化为字符串集。

     [!code-csharp[ToolWindowSearch#1](../extensibility/codesnippet/CSharp/adding-search-to-a-tool-window_1.cs)]
     [!code-vb[ToolWindowSearch#1](../extensibility/codesnippet/VisualBasic/adding-search-to-a-tool-window_1.vb)]

5. 生成项目并启动调试。 视觉工作室的实验实例出现。

6. 在菜单栏上，选择 **"查看** > **其他 Windows** > **测试搜索**"。

     将显示工具窗口，但尚未显示搜索控件。

## <a name="to-add-a-search-box-to-the-tool-window"></a>向工具窗口添加搜索框

1. 在*TestSearch.cs*文件中，将以下代码添加到`TestSearch`类。 代码重写属性<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A>，以便 get 访问器返回`true`。

     要启用搜索，必须重写该<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A>属性。 类<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch>并提供不启用搜索的默认实现。

    ```csharp
    public override bool SearchEnabled
    {
        get { return true; }
    }
    ```

2. 生成项目并启动调试。 出现实验实例。

3. 在可视化工作室的实验实例中，打开**测试搜索**。

     在工具窗口的顶部，将显示一个搜索控件，其中带有**搜索**水印和放大镜图标。 但是，搜索尚未工作，因为搜索过程尚未实现。

## <a name="to-add-the-search-implementation"></a>添加搜索实现
 在 启用 上搜索<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>时，如上一过程所述，工具窗口将创建搜索主机。 此主机设置和管理搜索进程，这些进程始终发生在后台线程上。 由于<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>类管理搜索主机的创建和搜索的设置，因此只需创建搜索任务并提供搜索方法。 搜索过程发生在后台线程上，对工具窗口控件的调用发生在 UI 线程上。 因此，您必须使用[ThreadHelper.Invoke®](https://msdn.microsoft.com/data/ee197798(v=vs.85))方法来管理在处理控件时进行的任何调用。

1. 在*TestSearch.cs*文件中，添加以下`using`指令：

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Runtime.InteropServices;
    using System.Text;
    using System.Windows.Controls;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. 在类`TestSearch`中，添加以下代码，该代码执行以下操作：

    - 重写方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A>以创建搜索任务。

    - 重写方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A>以还原文本框的状态。 当用户取消搜索任务以及用户设置或取消设置选项或筛选器时，将调用此方法。 和<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A>都调用 UI 线程。 因此，您无需通过[ThreadHelper.Invoke®](https://msdn.microsoft.com/data/ee197798(v=vs.85))方法访问文本框。

    - 创建名为`TestSearchTask`从 继承<xref:Microsoft.VisualStudio.Shell.VsSearchTask>的类，该类提供 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsSearchTask>默认实现。

         在`TestSearchTask`中，构造函数设置引用工具窗口的专用字段。 要提供搜索方法，请重写 和<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A><xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStopSearch%2A>方法。 该方法<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A>是实现搜索过程的位置。 此过程包括执行搜索、在文本框中显示搜索结果以及调用此方法的基类实现以报告搜索已完成。

    ```csharp
    public override IVsSearchTask CreateSearch(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback)
    {
        if (pSearchQuery == null || pSearchCallback == null)
            return null;
         return new TestSearchTask(dwCookie, pSearchQuery, pSearchCallback, this);
    }

    public override void ClearSearch()
    {
        TestSearchControl control = (TestSearchControl)this.Content;
        control.SearchResultsTextBox.Text = control.SearchContent;
    }

    internal class TestSearchTask : VsSearchTask
    {
        private TestSearch m_toolWindow;

        public TestSearchTask(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback, TestSearch toolwindow)
            : base(dwCookie, pSearchQuery, pSearchCallback)
        {
            m_toolWindow = toolwindow;
        }

        protected override void OnStartSearch()
        {
            // Use the original content of the text box as the target of the search.
            var separator = new string[] { Environment.NewLine };
            TestSearchControl control = (TestSearchControl)m_toolWindow.Content;
            string[] contentArr = control.SearchContent.Split(separator, StringSplitOptions.None);

            // Get the search option.
            bool matchCase = false;
            // matchCase = m_toolWindow.MatchCaseOption.Value;

                // Set variables that are used in the finally block.
                StringBuilder sb = new StringBuilder("");
                uint resultCount = 0;
                this.ErrorCode = VSConstants.S_OK;

                try
                {
                    string searchString = this.SearchQuery.SearchString;

                    // Determine the results.
                    uint progress = 0;
                    foreach (string line in contentArr)
                    {
                        if (matchCase == true)
                        {
                            if (line.Contains(searchString))
                            {
                                sb.AppendLine(line);
                                resultCount++;
                            }
                        }
                        else
                            {
                                if (line.ToLower().Contains(searchString.ToLower()))
                                {
                                    sb.AppendLine(line);
                                    resultCount++;
                                }
                            }

                            // SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));

                            // Uncomment the following line to demonstrate the progress bar.
                            // System.Threading.Thread.Sleep(100);
                        }
                    }
                    catch (Exception e)
                    {
                        this.ErrorCode = VSConstants.E_FAIL;
                    }
                    finally
                    {
                        ThreadHelper.Generic.Invoke(() =>
                        { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });

                        this.SearchResults = resultCount;
                    }

            // Call the implementation of this method in the base class.
            // This sets the task status to complete and reports task completion.
            base.OnStartSearch();
        }

        protected override void OnStopSearch()
        {
            this.SearchResults = 0;
        }
    }
    ```

3. 通过执行以下步骤测试搜索实现：

    1. 重建项目并开始调试。

    2. 在 Visual Studio 的实验实例中，再次打开工具窗口，在搜索窗口中输入一些搜索文本，然后单击**ENTER**。

         应显示正确的结果。

## <a name="to-customize-the-search-behavior"></a>自定义搜索行为
 通过更改搜索设置，可以对搜索控件的显示方式和搜索执行方式进行各种更改。例如，您可以更改水印（搜索框中显示的默认文本）、搜索控件的最小宽度和最大宽度，以及是否显示进度条。 您还可以更改搜索结果开始显示的点（按需搜索或即时搜索），以及是否显示最近搜索的字词列表。 您可以在<xref:Microsoft.VisualStudio.PlatformUI.SearchSettingsDataSource>类中找到完整的设置列表。

1. 在* TestSearch.cs* 文件中，将以下代码添加到`TestSearch`类。 此代码支持即时搜索，而不是按需搜索（这意味着用户不必单击**ENTER**）。 代码重写`ProvideSearchSettings``TestSearch`类中的方法，这是更改默认设置所必需的。

    ```csharp
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)
    {
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchStartTypeProperty.Name,
            (uint)VSSEARCHSTARTTYPE.SST_INSTANT);}
    ```

2. 通过重建解决方案并重新启动调试器来测试新设置。

     每次在搜索框中输入字符时，都会显示搜索结果。

3. 在`ProvideSearchSettings`方法中，添加以下行，从而显示进度条。

    ```csharp
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)
    {
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchStartTypeProperty.Name,
             (uint)VSSEARCHSTARTTYPE.SST_INSTANT);
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchProgressTypeProperty.Name,
             (uint)VSSEARCHPROGRESSTYPE.SPT_DETERMINATE);
    }
    ```

     要显示进度条，必须报告进度。 要报告进度，请取消注释`OnStartSearch``TestSearchTask`类方法中的以下代码：

    ```csharp
    SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));
    ```

4. 要使处理速度足够慢，使进度条可见，请取消注释`OnStartSearch``TestSearchTask`类方法中的以下行：

    ```csharp
    System.Threading.Thread.Sleep(100);
    ```

5. 通过重建解决方案并开始调试来测试新设置。

     每次执行搜索时，进度栏都会显示在搜索窗口中（作为搜索文本框下方的蓝线）。

## <a name="to-enable-users-to-refine-their-searches"></a>使用户能够优化其搜索
 您可以允许用户通过匹配**大小写**或 **"匹配整个单词**"等选项来优化其搜索。 选项可以是布尔，显示为复选框，也可以显示为按钮的命令。 在本演练中，您将创建一个布尔选项。

1. 在*TestSearch.cs*文件中，将以下代码添加到`TestSearch`类。 代码重写该方法`SearchOptionsEnum`，该方法允许搜索实现检测给定选项是打开还是关闭。 中`SearchOptionsEnum`的代码添加一个选项，用于将大小写匹配<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumWindowSearchOptions>到枚举器。 匹配大小写的选项也作为`MatchCaseOption`属性提供。

    ```csharp
    private IVsEnumWindowSearchOptions m_optionsEnum;
    public override IVsEnumWindowSearchOptions SearchOptionsEnum
    {
        get
        {
            if (m_optionsEnum == null)
            {
                List<IVsWindowSearchOption> list = new List<IVsWindowSearchOption>();

                list.Add(this.MatchCaseOption);

                m_optionsEnum = new WindowSearchOptionEnumerator(list) as IVsEnumWindowSearchOptions;
            }
            return m_optionsEnum;
        }
    }

    private WindowSearchBooleanOption m_matchCaseOption;
    public WindowSearchBooleanOption MatchCaseOption
    {
        get
        {
            if (m_matchCaseOption == null)
            {
                m_matchCaseOption = new WindowSearchBooleanOption("Match case", "Match case", false);
            }
            return m_matchCaseOption;
        }
    }
    ```

2. 在类`TestSearchTask`中，取消注释`OnStartSearch`方法中的以下行：

    ```csharp
    matchCase = m_toolWindow.MatchCaseOption.Value;
    ```

3. 测试选项：

    1. 生成项目并启动调试。 出现实验实例。

    2. 在工具窗口中，选择文本框右侧的向下箭头。

         将显示 **"匹配"案例**复选框。

    3. 选择 **"匹配"案例**复选框，然后执行一些搜索。

## <a name="to-add-a-search-filter"></a>添加搜索筛选器
 您可以添加允许用户优化搜索目标集的搜索筛选器。 例如，您可以按文件资源管理器中的文件最近修改的日期及其文件名扩展名筛选文件。 在本演练中，您将只为偶数行添加筛选器。 当用户选择该筛选器时，搜索主机会将指定的字符串添加到搜索查询中。 然后，您可以在搜索方法中标识这些字符串，并相应地筛选搜索目标。

1. 在*TestSearch.cs*文件中，将以下代码添加到`TestSearch`类。 代码通过添加`SearchFiltersEnum`<xref:Microsoft.VisualStudio.PlatformUI.WindowSearchSimpleFilter>指定来筛选搜索结果，以便只显示偶数行来实现。

    ```csharp
    public override IVsEnumWindowSearchFilters SearchFiltersEnum
    {
        get
        {
            List<IVsWindowSearchFilter> list = new List<IVsWindowSearchFilter>();
            list.Add(new WindowSearchSimpleFilter("Search even lines only", "Search even lines only", "lines", "even"));
            return new WindowSearchFilterEnumerator(list) as IVsEnumWindowSearchFilters;
        }
    }

    ```

     现在搜索控件显示搜索筛选器`Search even lines only`。 当用户选择筛选器时，字符串`lines:"even"`将显示在搜索框中。 其他搜索条件可以与筛选器同时显示。 搜索字符串可能出现在筛选器之前、筛选器之后或两者。

2. 在*TestSearch.cs*文件中，将以下方法添加到类中`TestSearchTask`，该类位于类中。 `TestSearch` 这些方法支持该方法`OnStartSearch`，您将在下一步中修改该方法。

    ```csharp
    private string RemoveFromString(string origString, string stringToRemove)
    {
        int index = origString.IndexOf(stringToRemove);
        if (index == -1)
            return origString;
        else 
             return (origString.Substring(0, index) + origString.Substring(index + stringToRemove.Length)).Trim();
    }

    private string[] GetEvenItems(string[] contentArr)
    {
        int length = contentArr.Length / 2;
        string[] evenContentArr = new string[length];

        int indexB = 0;
        for (int index = 1; index < contentArr.Length; index += 2)
        {
            evenContentArr[indexB] = contentArr[index];
            indexB++;
        }

        return evenContentArr;
    }
    ```

3. 在`TestSearchTask`类中，使用`OnStartSearch`以下代码更新方法。 此更改更新代码以支持筛选器。

    ```csharp
    protected override void OnStartSearch()
    {
        // Use the original content of the text box as the target of the search. 
        var separator = new string[] { Environment.NewLine };
        string[] contentArr = ((TestSearchControl)m_toolWindow.Content).SearchContent.Split(separator, StringSplitOptions.None);

        // Get the search option. 
        bool matchCase = false;
        matchCase = m_toolWindow.MatchCaseOption.Value;

        // Set variables that are used in the finally block.
        StringBuilder sb = new StringBuilder("");
        uint resultCount = 0;
        this.ErrorCode = VSConstants.S_OK;

        try
        {
            string searchString = this.SearchQuery.SearchString;

            // If the search string contains the filter string, filter the content array. 
            string filterString = "lines:\"even\"";

            if (this.SearchQuery.SearchString.Contains(filterString))
            {
                // Retain only the even items in the array.
                contentArr = GetEvenItems(contentArr);

                // Remove 'lines:"even"' from the search string.
                searchString = RemoveFromString(searchString, filterString);
            }

            // Determine the results. 
            uint progress = 0;
            foreach (string line in contentArr)
            {
                if (matchCase == true)
                {
                    if (line.Contains(searchString))
                    {
                        sb.AppendLine(line);
                        resultCount++;
                    }
                }
                else
                {
                    if (line.ToLower().Contains(searchString.ToLower()))
                    {
                        sb.AppendLine(line);
                        resultCount++;
                    }
                }

                SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));

                // Uncomment the following line to demonstrate the progress bar. 
                // System.Threading.Thread.Sleep(100);
            }
        }
        catch (Exception e)
        {
            this.ErrorCode = VSConstants.E_FAIL;
        }
        finally
        {
            ThreadHelper.Generic.Invoke(() =>
            { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });

            this.SearchResults = resultCount;
        }

        // Call the implementation of this method in the base class. 
        // This sets the task status to complete and reports task completion. 
        base.OnStartSearch();
    }
    ```

4. 测试代码。

5. 生成项目并启动调试。 在 Visual Studio 的实验实例中，打开工具窗口，然后选择搜索控件上的向下箭头。

     "**匹配"案例**复选框和 **"搜索偶数行"仅**显示筛选器。

6. 选择筛选器。

     搜索框包含**行："偶数"，** 并显示以下结果：

     2 好

     4 好

     6 再见

7. 从`lines:"even"`搜索框中删除，选择"**匹配"案例**复选框，然后在搜索框中输入`g`。

     将显示以下结果：

     1 次

     2 好

     5 再见

8. 选择搜索框右侧的 X。

     清除搜索，并显示原始内容。 但是，"**匹配"案例**复选框仍被选中。
