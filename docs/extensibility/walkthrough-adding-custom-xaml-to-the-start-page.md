---
title: 演练：将自定义 XAML 添加到起始页 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 4e2afc90dc96978e8a8290afaa2d3278e8b621b3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697676"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>演练：将自定义 XAML 添加到起始页

本演练演示如何创建包含 Web 浏览器的自定义可视化工作室起始页。

## <a name="add-custom-xaml"></a>添加自定义 XAML

1. 按照["创建自定义起始页](../extensibility/creating-a-custom-start-page.md)"中的说明创建起始页。

2. 在*MainWindow.xaml*文件中，查找\<网格>部分。

3. 在\<\<网格>元素中添加 TabControl> 元素和\<TabItem>，如以下示例所示。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. 使用打开新项目\<的按钮>元素添加第\<二个 TabItem>：

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="MyButton" Height="Auto">
                <Button Name="btnNewProj" Content="New Project"
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
                    CommandParameter="File.NewProject" >
                </Button>
            </TabItem>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

## <a name="test-the-custom-start-page"></a>测试自定义起始页

1. 按 **F5**。

     Visual Studio 的实验实例将打开，并安装自定义起始页，但未选择。

2. 在可视化工作室的实验实例中，打开**工具/选项/环境**页面。

3. 选择**启动**。 在 **"自定义起始页"** 列表中，选择 *.xaml*文件，然后单击 **"确定**"。

4. 在“视图” **** 菜单上，单击“起始页” ****。

5. 单击**必应**选项卡。

     您应该会看到必应网页。

6. 单击 **"我的按钮"** 选项卡。

     您应该会看到一个 **"我的项目"** 按钮，该按钮将打开 **"新项目"** 对话框。

7. 关闭实验实例。

要应用自定义起始页，请在 **"工具** > **选项** > **环境**"中，选择 **"启动**"。 在 **"自定义起始页"** 列表中，选择 *.xaml*文件，然后单击 **"确定**"。

## <a name="next-steps"></a>后续步骤

Visual Studio 起始页现在包含一个选项卡，该选项卡显示 Web 浏览器选项卡和 MyButton 选项卡。可以使用*代码背后的*模型添加自定义 .dll 来创建具有其他功能的自定义起始页，如[将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)中所示。 通过将生成的 .vsix 文件发布到[Visual Studio 应用商店](https://marketplace.visualstudio.com/)网站或其他网站或网络共享，可以与其他用户共享自定义起始页。 有关更多信息，请参见 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)。

## <a name="see-also"></a>请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF 容器控件](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
