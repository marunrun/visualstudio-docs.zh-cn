---
title: 将搜索添加到工具窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, adding search
ms.assetid: f78c4892-8060-49c4-8ecd-4360f1b4d133
caps.latest.revision: 39
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 81043cc87dd659f14ec634dc14990956a0864f9b
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263578"
---
# <a name="adding-search-to-a-tool-window"></a>将搜索添加到工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当创建或更新您的扩展插件中的工具窗口时，可以在 Visual Studio 中添加相同的搜索功能的其他位置出现。 此功能包括以下功能：  
  
- 在工具栏的自定义区域中始终位于一个搜索框。  
  
- 在搜索框本身叠加一个进度指示器。  
  
- 只要输入每个字符 （即时搜索） 或者仅在选择 Enter 键 （按需搜索） 后，才显示结果的功能。  
  
- 一个列表，显示为其已搜索最新的条款。  
  
- 筛选搜索按特定字段或搜索目标的各个方面的功能。  
  
  通过完成本演练，你将了解如何执行以下任务：  
  
1. 创建 VSPackage 项目。  
  
2. 创建一个包含与只读文本框 UserControl 的工具窗口。  
  
3. 将搜索框添加到工具窗口。  
  
4. 添加搜索实现。  
  
5. 启用即时搜索和显示一个进度栏。  
  
6. 添加**区分大小写**选项。  
  
7. 添加**搜索偶数行仅**筛选器。  
  
## <a name="to-create-a-vsix-project"></a>创建 VSIX 项目  
  
1. 创建一个名为的 VSIX 项目`TestToolWindowSearch`通过名为工具窗口**TestSearch**。 如果你在执行此操作时需要帮助，请参阅 [Creating an Extension with a Tool Window](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
## <a name="to-create-a-tool-window"></a>若要创建工具窗口  
  
1. 在`TestToolWindowSearch`项目中，打开 TestSearchControl.xaml 文件。  
  
2. 替换现有`<StackPanel>`具有以下块，将添加一个只读的块<xref:System.Windows.Controls.TextBox>到<xref:System.Windows.Controls.UserControl>工具窗口中。  
  
    ```xaml  
    <StackPanel Orientation="Vertical">  
        <TextBox Name="resultsTextBox" Height="800.0"  
            Width="800.0"  
            IsReadOnly="True">  
        </TextBox>  
    </StackPanel>  
    ```  
  
3. 在 TestSearchControl.xaml.cs 文件中，添加以下 using 语句：  
  
    ```csharp  
    using System.Text;  
    ```  
  
4. 删除`button1_Click()`方法。  
  
     在中**TestSearchControl**类中，添加以下代码。  
  
     此代码将添加一个公共<xref:System.Windows.Controls.TextBox>名为属性**SearchResultsTextBox**和名为的公共字符串属性**SearchContent**。 在构造函数 SearchResultsTextBox 设置文本框中，为和 SearchContent 初始化为一组换行分隔的字符串。 文本框的内容也将初始化为一系列字符串。  
  
    ```csharp  
    public partial class TestSearchControl : UserControl  
    {  
        public TextBox SearchResultsTextBox { get; set; }  
        public string SearchContent { get; set; }  
  
        public TestSearchControl()  
        {  
            InitializeComponent();  
  
            this.SearchResultsTextBox = resultsTextBox;  
            this.SearchContent = BuildContent();  
  
            this.SearchResultsTextBox.Text = this.SearchContent;  
        }  
  
        private string BuildContent()  
        {  
            StringBuilder sb = new StringBuilder();  
            sb.AppendLine("1 go");  
            sb.AppendLine("2 good");  
            sb.AppendLine("3 Go");  
            sb.AppendLine("4 Good");  
            sb.AppendLine("5 goodbye");  
            sb.AppendLine("6 Goodbye");  
  
            return sb.ToString();  
        }  
    }  
    ```  
  
     [!code-csharp[ToolWindowSearch#1](../snippets/csharp/VS_Snippets_VBCSharp/toolwindowsearch/cs/mycontrol.xaml.cs#1)]
     [!code-vb[ToolWindowSearch#1](../snippets/visualbasic/VS_Snippets_VBCSharp/toolwindowsearch/vb/mycontrol.xaml.vb#1)]  
  
5. 生成项目并启动调试。 将显示 Visual Studio 的实验实例。  
  
6. 在菜单栏上依次选择**视图**，**其他 Windows**， **TestSearch**。  
  
     工具窗口将显示，但尚未未显示搜索控件。  
  
## <a name="to-add-a-search-box-to-the-tool-window"></a>若要将搜索框添加到工具窗口  
  
1. 在 TestSearch.cs 文件中，以下代码添加到`TestSearch`类。 该代码重写<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A>属性，以便 get 访问器返回`true`。  
  
     若要启用搜索，必须重写<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A>属性。 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane>类实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch>，并提供一个默认实现，不会启用搜索。  
  
    ```csharp  
    public override bool SearchEnabled  
    {  
        get { return true; }  
    }  
    ```  
  
2. 生成项目并启动调试。 将显示在实验实例。  
  
3. 在 Visual Studio 的实验实例中，打开**TestSearch**。  
  
     在工具窗口的顶部，将显示使用的搜索控件**搜索**水印和放大玻璃图标。 但是，搜索不起作用还因为尚未实现对搜索过程。  
  
## <a name="to-add-the-search-implementation"></a>若要添加搜索实现  
 如果在启用搜索<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>，如工具窗口在上一过程中，创建搜索主机。 此主机将设置和管理搜索过程，始终在后台线程发生。 因为<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>类管理搜索主机和设置创建了搜索的仅需要创建搜索任务，并提供搜索方法。 在后台线程上发生搜索过程和工具窗口控件对的调用发生在 UI 线程上。 因此，必须使用[ThreadHelper.Invoke*](https://msdn.microsoft.com/data/ee197798(v=vs.85))方法来管理与该控件的处理中所做的任何调用。  
  
1. 在 TestSearch.cs 文件中，添加以下`using`语句：  
  
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
  
2. 在`TestSearch`类中，添加以下代码，执行以下操作：  
  
    - 重写<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A>方法创建搜索任务。  
  
    - 重写<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A>方法要还原的文本框中的状态。 当用户取消搜索任务和用户设置或取消设置选项或筛选器时，调用此方法。 这两<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A>UI 线程上调用。 因此，无需访问通过文本框[ThreadHelper.Invoke*](https://msdn.microsoft.com/data/ee197798(v=vs.85))方法。  
  
    - 创建名为的类`TestSearchTask`，它继承自<xref:Microsoft.VisualStudio.Shell.VsSearchTask>，它提供的默认实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSearchTask>。  
  
         在`TestSearchTask`，构造函数设置引用工具窗口的私有字段。 若要提供的搜索方法，重写<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A>和<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStopSearch%2A>方法。 <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A>方法是在其中实现搜索过程。 此过程包括执行搜索，搜索结果显示在文本框中，并调用此方法来报告搜索已完成的基类实现。  
  
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
  
3. 通过执行以下步骤来测试您的搜索实现：  
  
    1. 重新生成项目并启动调试。  
  
    2. 在 Visual Studio 的实验实例中，再次打开工具窗口、 搜索窗口中输入一些搜索文本和单击 ENTER。  
  
         应显示正确的结果。  
  
## <a name="to-customize-the-search-behavior"></a>若要自定义搜索行为  
 通过更改搜索设置，可以在搜索控件的显示方式和搜索执行方式进行各种更改。例如，可以更改水印 （在搜索框中显示的默认文本）、 最小和最大宽度的搜索控件，以及是否显示一个进度栏。 此外可以更改的点时的搜索结果开始显示 （按需或即时搜索），以及是否显示最近搜索的术语的列表。 您可以查找中的设置的完整列表<xref:Microsoft.VisualStudio.PlatformUI.SearchSettingsDataSource>类。  
  
1. 在 TestSearch.cs 文件中，以下代码添加到`TestSearch`类。 此代码，而不是按需搜索 （即用户无需单击输入） 的即时搜索。 该代码重写`ProvideSearchSettings`中的方法`TestSearch`类，该类是需要更改默认设置。  
  
    ```csharp  
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)  
    {  
        Utilities.SetValue(pSearchSettings,   
            SearchSettingsDataSource.SearchStartTypeProperty.Name,   
            (uint)VSSEARCHSTARTTYPE.SST_INSTANT);}  
    ```  
  
2. 测试新设置重新生成解决方案并重新启动调试器。  
  
     搜索结果将显示每次您在搜索框中输入一个字符。  
  
3. 在`ProvideSearchSettings`方法中，添加以下行，可以显示一个进度栏。  
  
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
  
     若要显示的进度条，必须报告进度。 若要报告进度，请取消注释中的以下代码`OnStartSearch`方法的`TestSearchTask`类：  
  
    ```csharp  
    SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));  
    ```  
  
4. 缓慢足够的处理进度条是可见的取消注释以下行中的`OnStartSearch`方法的`TestSearchTask`类：  
  
    ```csharp  
    System.Threading.Thread.Sleep(100);  
    ```  
  
5. 通过重新生成解决方案并启动到 debugb 测试新的设置。  
  
     进度栏将显示在搜索窗口中 （作为搜索文本框下一条蓝线） 每次执行搜索。  
  
## <a name="to-enable-users-to-refine-their-searches"></a>若要使用户能够优化其搜索  
 您可以允许用户以如通过选项来优化其搜索**区分大小写**或**全字匹配**。 选项可将布尔值，其中显示为复选框或显示为按钮的命令。 对于本演练中，将创建一个布尔值的选项。  
  
1. 在 TestSearch.cs 文件中，以下代码添加到`TestSearch`类。 该代码重写`SearchOptionsEnum`方法，它允许搜索实现来检测给定的选项是否处于打开或关闭。 中的代码`SearchOptionsEnum`中添加一个选项以匹配大小写到<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumWindowSearchOptions>枚举器。 若要区分大小写的选项都还可作为`MatchCaseOption`属性。  
  
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
  
2. 在中`TestSearchTask`类中，取消注释中的 matchCase 行`OnStartSearch`方法：  
  
    ```csharp  
    private IVsEnumWindowSearchOptions m_optionsEnum;  
    public override IVsEnumWindowSearchOptions SearchOptionsEnum  
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
  
3. 测试选项：  
  
    1. 生成项目并启动调试。 将显示在实验实例。  
  
    2. 在工具窗口中，选择文本框右侧的向下箭头。  
  
         **区分大小写**显示复选框。  
  
    3. 选择**区分大小写**复选框，然后再执行一些搜索。  
  
## <a name="to-add-a-search-filter"></a>若要添加搜索筛选器  
 您可以添加搜索筛选器，使用户能够修改搜索目标的设置。 例如，可以在其修改最新的日期和及其文件扩展名筛选文件资源管理器中的文件。 在本演练中，您将添加仅偶数行的筛选器。 当用户选择该筛选器时，搜索主机会将你指定的字符串添加到搜索查询。 然后，可以确定这些字符串内搜索方法，并相应地筛选的搜索目标。  
  
1. 在 TestSearch.cs 文件中，以下代码添加到`TestSearch`类。 这段代码实现`SearchFiltersEnum`通过添加<xref:Microsoft.VisualStudio.PlatformUI.WindowSearchSimpleFilter>，指定要筛选搜索结果，以便仅偶数行显示。  
  
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
  
     现在，在搜索控件显示在搜索筛选器`Search even lines only`。 当用户选择的筛选器，该字符串`lines:"even"`出现在搜索框中。 其他搜索条件可以出现在同一时间作为筛选器。 搜索字符串后和 / 或筛选器中，情况下可能出现在筛选器之前,。  
  
2. 在 TestSearch.cs 文件中，添加以下方法来`TestSearchTask`类，该类是在`TestSearch`类。 这些方法支持`OnStartSearch`方法，将在下一步中修改。  
  
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
  
3. 在中`TestSearchTask`类中，更新`OnStartSearch`用下面的代码的方法。 此更改更新代码以支持筛选器。  
  
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
  
4. 测试你的代码。  
  
5. 生成项目并启动调试。 在 Visual Studio 的实验实例中，打开工具窗口中，并选择搜索控件上的向下箭头。  
  
     **区分大小写**复选框并**搜索偶数行仅**筛选器显示。  
  
6. 选择的筛选器。  
  
     搜索框中包含**行:"甚至"** ，并且显示以下结果：  
  
     很好的 2  
  
     4 个良好  
  
     6 goodbye  
  
7. 删除`lines:"even"`搜索框中，选择**区分大小写**复选框，并输入`g`在搜索框中。  
  
     显示以下结果：  
  
     1 转  
  
     很好的 2  
  
     5 goodbye  
  
8. 选择搜索框右侧的 X。  
  
     清除搜索，并显示原始内容。 但是，**区分大小写**复选框仍处于选中状态。
