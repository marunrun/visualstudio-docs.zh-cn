---
title: 向工具窗口添加搜索 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66263578"
---
# <a name="adding-search-to-a-tool-window"></a>将搜索添加到工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你在扩展中创建或更新工具窗口时，可以添加在 Visual Studio 中的其他位置显示的相同搜索功能。 此功能包括以下功能：  
  
- 始终位于工具栏自定义区域中的搜索框。  
  
- 在搜索框本身上叠加的进度指示器。  
  
- 在输入每个字符 ("即时搜索") 或仅在选择 "输入密钥" ("按需搜索") 之后，才能显示结果。  
  
- 显示您最近搜索过的术语的列表。  
  
- 能够按特定字段或搜索目标的各个方面来筛选搜索。  
  
  按照此演练操作，你将学习如何执行以下任务：  
  
1. 创建 VSPackage 项目。  
  
2. 创建一个工具窗口，其中包含一个具有只读文本框的 UserControl。  
  
3. 将搜索框添加到工具窗口。  
  
4. 添加搜索实现。  
  
5. 启用即时搜索并显示进度栏。  
  
6. 添加 **匹配大小写** 选项。  
  
7. 添加 " **仅搜索行** " 筛选器。  
  
## <a name="to-create-a-vsix-project"></a>创建 VSIX 项目  
  
1. `TestToolWindowSearch`使用名为**TestSearch**的工具窗口创建一个名为的 VSIX 项目。 如果你在执行此操作时需要帮助，请参阅 [Creating an Extension with a Tool Window](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
## <a name="to-create-a-tool-window"></a>创建工具窗口  
  
1. 在 `TestToolWindowSearch` 项目中，打开 TestSearchControl 文件。  
  
2. 将现有块替换为 `<StackPanel>` 以下块，这会 <xref:System.Windows.Controls.TextBox> 在工具窗口中将一个只读添加到 <xref:System.Windows.Controls.UserControl> 中。  
  
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
  
4. 删除 `button1_Click()` 方法。  
  
     在 **TestSearchControl** 类中，添加以下代码。  
  
     此代码将添加一个 <xref:System.Windows.Controls.TextBox> 名为 **SearchResultsTextBox** 的公共属性和一个名为 **SearchContent**的公共字符串属性。 在构造函数中，将 SearchResultsTextBox 设置为文本框，并将 SearchContent 初始化为换行符分隔的字符串集。 文本框的内容也初始化为字符串集。  
  
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
  
5. 生成项目并启动调试。 此时将显示 Visual Studio 的实验实例。  
  
6. 在菜单栏上，依次选择 " **视图**"、" **其他窗口**"、" **TestSearch**"。  
  
     此时将显示工具窗口，但不会显示 "搜索" 控件。  
  
## <a name="to-add-a-search-box-to-the-tool-window"></a>向工具窗口添加搜索框  
  
1. 在 TestSearch.cs 文件中，将以下代码添加到 `TestSearch` 类。 此代码将重写 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A> 属性，以便 get 访问器返回 `true` 。  
  
     若要启用搜索，必须重写 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A> 属性。 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane>类实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch> 并提供不启用搜索的默认实现。  
  
    ```csharp  
    public override bool SearchEnabled  
    {  
        get { return true; }  
    }  
    ```  
  
2. 生成项目并启动调试。 这将显示实验实例。  
  
3. 在 Visual Studio 的实验实例中，打开 **TestSearch**。  
  
     在工具窗口的顶部，搜索控件显示为一个 **搜索** 水印和一个放大镜图标。 不过，搜索仍不起作用，因为尚未实现搜索过程。  
  
## <a name="to-add-the-search-implementation"></a>添加搜索实现  
 当你在上启用搜索时（ <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> 如前面的过程中），工具窗口会创建一个搜索主机。 此主机设置并管理在后台线程上始终发生的搜索过程。 因为 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> 类管理搜索主机的创建和搜索的设置，所以只需创建搜索任务并提供搜索方法。 搜索过程在后台线程上发生，并且对工具窗口控件的调用会在 UI 线程上发生。 因此，你必须使用 [ThreadHelper *](https://msdn.microsoft.com/data/ee197798(v=vs.85)) 方法来管理你在处理控件时所做的任何调用。  
  
1. 在 TestSearch.cs 文件中，添加以下 `using` 语句：  
  
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
  
2. 在 `TestSearch` 类中，添加以下代码，以执行以下操作：  
  
    - 重写 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A> 方法以创建搜索任务。  
  
    - 重写 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A> 方法以还原文本框的状态。 当用户取消搜索任务以及用户设置或取消设置选项或筛选器时，将调用此方法。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A>和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A> 都在 UI 线程上调用。 因此，您不需要通过 [ThreadHelper *](https://msdn.microsoft.com/data/ee197798(v=vs.85)) 方法访问文本框。  
  
    - 创建一个从继承的名为 `TestSearchTask` 的类 <xref:Microsoft.VisualStudio.Shell.VsSearchTask> ，它提供的默认实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSearchTask> 。  
  
         在中 `TestSearchTask` ，构造函数设置引用工具窗口的私有字段。 若要提供搜索方法，请重写 <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A> 和 <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStopSearch%2A> 方法。 <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A>方法是实现搜索过程的位置。 此过程包括执行搜索、在文本框中显示搜索结果以及调用此方法的基类实现，以报告搜索已完成。  
  
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
  
    1. 重新生成项目并启动调试。  
  
    2. 在 Visual Studio 的实验实例中，再次打开工具窗口，在 "搜索" 窗口中输入一些搜索文本，然后单击 "ENTER"。  
  
         应显示正确的结果。  
  
## <a name="to-customize-the-search-behavior"></a>自定义搜索行为  
 通过更改搜索设置，可以对搜索控件的显示方式和执行方式进行各种更改。例如，可以 (搜索框中显示的默认文本) 、搜索控件的最小和最大宽度，以及是否显示进度栏来更改水印。 您还可以更改搜索结果开始 (按需或即时搜索) 显示的点，以及是否显示您最近搜索过的术语的列表。 可以在类中找到完整的设置列表 <xref:Microsoft.VisualStudio.PlatformUI.SearchSettingsDataSource> 。  
  
1. 在 TestSearch.cs 文件中，将以下代码添加到 `TestSearch` 类。 此代码启用即时搜索，而不是按需搜索 (意味着用户无需单击 "ENTER") 。 此代码将重写 `ProvideSearchSettings` 类中的方法 `TestSearch` ，这是更改默认设置所必需的。  
  
    ```csharp  
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)  
    {  
        Utilities.SetValue(pSearchSettings,   
            SearchSettingsDataSource.SearchStartTypeProperty.Name,   
            (uint)VSSEARCHSTARTTYPE.SST_INSTANT);}  
    ```  
  
2. 通过重新生成解决方案并重新启动调试器来测试新设置。  
  
     每次在搜索框中输入字符时，都会显示搜索结果。  
  
3. 在 `ProvideSearchSettings` 方法中，添加以下行，以便显示进度栏。  
  
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
  
     若要显示进度栏，必须报告进度。 若要报告进度，请在类的方法中取消对以下代码的注释 `OnStartSearch` `TestSearchTask` ：  
  
    ```csharp  
    SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));  
    ```  
  
4. 若要慢速处理以使进度栏可见，请在类的方法中取消对以下行的注释 `OnStartSearch` `TestSearchTask` ：  
  
    ```csharp  
    System.Threading.Thread.Sleep(100);  
    ```  
  
5. 通过重新生成解决方案并开始 debugb 来测试新设置。  
  
     每次执行搜索时，进度栏都将显示在 "搜索" 窗口中 () "搜索" 文本框下的蓝色线。  
  
## <a name="to-enable-users-to-refine-their-searches"></a>使用户能够优化其搜索  
 您可以允许用户通过诸如 **大小写匹配** 或 **全字匹配**等选项来优化搜索。 选项可以是布尔值（显示为复选框）或显示为按钮的命令。 对于本演练，您将创建一个布尔选项。  
  
1. 在 TestSearch.cs 文件中，将以下代码添加到 `TestSearch` 类。 此代码将重写 `SearchOptionsEnum` 方法，这允许搜索实现检测给定选项是打开还是关闭。 中的代码 `SearchOptionsEnum` 将添加一个选项以匹配大小写到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumWindowSearchOptions> 枚举器。 用于区分大小写的选项也可作为属性使用 `MatchCaseOption` 。  
  
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
  
2. 在 `TestSearchTask` 类中，取消注释方法中的 matchCase 行 `OnStartSearch` ：  
  
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
  
    1. 生成项目并启动调试。 这将显示实验实例。  
  
    2. 在工具窗口中，选择文本框右侧的向下箭头。  
  
         此时将显示 "区分 **大小写** " 复选框。  
  
    3. 选中 "区分 **大小写** " 复选框，然后执行一些搜索。  
  
## <a name="to-add-a-search-filter"></a>添加搜索筛选器  
 您可以添加搜索筛选器，以允许用户精炼搜索目标集。 例如，你可以通过在文件资源管理器中对文件进行修改的日期和文件扩展名进行筛选。 在本演练中，您将为偶数行添加一个筛选器。 当用户选择该筛选器时，搜索主机会将您指定的字符串添加到搜索查询中。 然后，你可以在搜索方法中标识这些字符串并相应地筛选搜索目标。  
  
1. 在 TestSearch.cs 文件中，将以下代码添加到 `TestSearch` 类。 此代码 `SearchFiltersEnum` 通过添加 <xref:Microsoft.VisualStudio.PlatformUI.WindowSearchSimpleFilter> 指定来筛选搜索结果，以便只显示偶数行来实现。  
  
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
  
     现在，搜索控件显示搜索筛选器 `Search even lines only` 。 当用户选择筛选器时，字符串 `lines:"even"` 将显示在搜索框中。 其他搜索条件可以与筛选器同时出现。 搜索字符串可能出现在筛选器之前、筛选器之后或两者之后。  
  
2. 在 TestSearch.cs 文件中，将以下方法添加到类 `TestSearchTask` 中的类 `TestSearch` 。 这些方法支持 `OnStartSearch` 方法，你将在下一步中修改该方法。  
  
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
  
3. 在 `TestSearchTask` 类中， `OnStartSearch` 用以下代码更新方法。 此更改将更新代码以支持筛选器。  
  
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
  
5. 生成项目并启动调试。 在 Visual Studio 的实验实例中，打开工具窗口，然后选择 "搜索" 控件上的向下箭头。  
  
     显示 " **区分大小写** " 复选框和 " **仅搜索行** " 筛选器。  
  
6. 选择筛选器。  
  
     搜索框中包含 **行： "偶数"**，出现以下结果：  
  
     2好  
  
     4好  
  
     6再见  
  
7. `lines:"even"`从搜索框中删除，选择 "**匹配大小写**" 复选框，然后 `g` 在 "搜索" 框中输入。  
  
     将显示以下结果：  
  
     1开始  
  
     2好  
  
     5再见  
  
8. 选择 "搜索" 框右侧的 "X"。  
  
     将清除搜索，并显示原始内容。 但仍选中 "区分 **大小写** " 复选框。
