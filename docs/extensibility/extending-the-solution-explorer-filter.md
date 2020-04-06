---
title: 扩展解决方案资源管理器筛选器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Solution Explorer, extending
- extensibility [Visual Studio], projects and solutions
ms.assetid: df976c76-27ec-4f00-ab6d-a26a745dc6c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af0824edd4188481bec8c0703d71043354f5dbcc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711570"
---
# <a name="extend-the-solution-explorer-filter"></a>扩展解决方案资源管理器筛选器
您可以扩展**解决方案资源管理器**筛选器功能以显示或隐藏不同的文件。 例如，您可以创建一个筛选器，该筛选器在**解决方案资源管理器**中仅显示 C# 类工厂文件，正如本演练所示。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-visual-studio-package-project"></a>创建可视化工作室包项目

1. 创建名为 的`FileFilter`VSIX 项目。 添加名为**FileFilter 的**自定义命令项模板。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 添加 对`System.ComponentModel.Composition`和`Microsoft.VisualStudio.Utilities`的引用。

3. 使菜单命令显示在**解决方案资源管理器**工具栏上。 打开*文件筛选器包.vsct*文件。

4. 将`<Button>`块更改为以下内容：

    ```xml
    <Button guid="guidFileFilterPackageCmdSet" id="FileFilterId" priority="0x0400" type="Button">
        <Parent guid="guidSHLMainMenu" id="IDG_VS_TOOLBAR_PROJWIN_FILTERS" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>FileNameFilter</ButtonText>
        </Strings>
    </Button>
    ```

### <a name="update-the-manifest-file"></a>更新清单文件

1. 在*source.扩展.vsixmanifest 文件中*，添加作为 MEF 组件的资产。

2. 在"**资产**"选项卡上，选择"**新建"** 按钮。

3. 在 **"类型"** 字段中，选择**Microsoft.VisualStudio.Mef组件**。

4. 在 **"源"** 字段中，选择**当前解决方案中的项目**。

5. 在 **"项目"** 字段中，选择 **"文件筛选器**"，然后选择"**确定**"按钮。

### <a name="add-the-filter-code"></a>添加筛选器代码

1. 向*FileFilterPackageGuids.cs*文件添加一些 GUID：

    ```csharp
    public const string guidFileFilterPackageCmdSetString = "00000000-0000-0000-0000-00000000"; // get your GUID from the .vsct file
    public const int FileFilterId = 0x100;
    ```

2. 将类文件添加到名为*FileNameFilter.cs*的文件筛选器项目。

3. 将空命名空间和空类替换为下面的代码。

     该方法`Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem rootItems)`采用包含解决方案 （`rootItems`） 根的集合，并返回要包含在筛选器中的项的集合。

     该方法`ShouldIncludeInFilter`根据指定的条件筛选**解决方案资源管理器**层次结构中的项。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio.Shell;

    namespace FileFilter
    {
        // Implements ISolutionTreeFilterProvider. The SolutionTreeFilterProvider attribute declares it as a MEF component
        [SolutionTreeFilterProvider(FileFilterPackageGuids.guidFileFilterPackageCmdSetString, (uint)(FileFilterPackageGuids.FileFilterId))]
        public sealed class FileNameFilterProvider : HierarchyTreeFilterProvider
        {
            SVsServiceProvider svcProvider;
            IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;

            // Constructor required for MEF composition
            [ImportingConstructor]
            public FileNameFilterProvider(SVsServiceProvider serviceProvider, IVsHierarchyItemCollectionProvider hierarchyCollectionProvider)
            {
                this.svcProvider = serviceProvider;
                this.hierarchyCollectionProvider = hierarchyCollectionProvider;
            }

            // Returns an instance of Create filter class.
            protected override HierarchyTreeFilter CreateFilter()
            {
                return new FileNameFilter(this.svcProvider, this.hierarchyCollectionProvider, FileNamePattern);
            }

            // Regex pattern for CSharp factory classes
            private const string FileNamePattern = @"\w*factory\w*(.cs$)";

            // Implementation of file filtering
            private sealed class FileNameFilter : HierarchyTreeFilter
            {
                private readonly Regex regexp;
                private readonly IServiceProvider svcProvider;
                private readonly IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;

                public FileNameFilter(
                    IServiceProvider serviceProvider,
                    IVsHierarchyItemCollectionProvider hierarchyCollectionProvider,
                    string fileNamePattern)
                {
                    this.svcProvider = serviceProvider;
                    this.hierarchyCollectionProvider = hierarchyCollectionProvider;
                    this.regexp = new Regex(fileNamePattern, RegexOptions.IgnoreCase);
                }

                // Gets the items to be included from this filter provider.
                // rootItems is a collection that contains the root of your solution
                // Returns a collection of items to be included as part of the filter
                protected override async Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem> rootItems)
                {
                    IVsHierarchyItem root = HierarchyUtilities.FindCommonAncestor(rootItems);
                    IReadOnlyObservableSet<IVsHierarchyItem> sourceItems;
                    sourceItems = await hierarchyCollectionProvider.GetDescendantsAsync(
                                        root.HierarchyIdentity.NestedHierarchy,
                                        CancellationToken);

                    IFilteredHierarchyItemSet includedItems = await hierarchyCollectionProvider.GetFilteredHierarchyItemsAsync(
                        sourceItems,
                        ShouldIncludeInFilter,
                        CancellationToken);
                    return includedItems;
                }

                // Returns true if filters hierarchy item name for given filter; otherwise, false</returns>
                private bool ShouldIncludeInFilter(IVsHierarchyItem hierarchyItem)
                {
                    if (hierarchyItem == null)
                    {
                        return false;
                    }
                    return this.regexp.IsMatch(hierarchyItem.Text);
                }
            }
        }
    }

    ```

4. 在*FileFilter.cs*中，从 FileFilter 构造函数中删除命令放置和处理代码。 结果应如下所示：

    ```csharp
    private FileFilter(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;
    }
    ```

     也删除`ShowMessageBox()`方法。

5. 在*FileFilterPackage.cs*中，将方法中`Initialize()`的代码替换为以下内容：

    ```csharp
    protected override void Initialize()
    {
        Debug.WriteLine (string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));
        base.Initialize();
    }
    ```

### <a name="test-your-code"></a>测试代码

1. 生成并运行该项目。 将出现 Visual Studio 的第二个实例。 这称为实验实例。

2. 在 Visual Studio 的实验中，打开 C# 项目。

3. 查找在**解决方案资源管理器**工具栏上添加的按钮。 它应该是左侧的第四个按钮。

4. 单击该按钮时，应筛选出所有文件，并且应看到**所有项目都已从视图中筛选出来。** 在**解决方案资源管理器**中。
