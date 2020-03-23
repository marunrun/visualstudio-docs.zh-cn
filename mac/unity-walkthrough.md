---
title: 开始使用 Unity 生成游戏
description: Unity 和 Visual Studio for Mac 入门
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/20/2019
ms.technology: vs-ide-general
ms.assetid: D07FA43B-9D18-4DFA-8343-CD538FAD84DB
ms.openlocfilehash: c25df777a9af10859c70741a78c880a57c6f5b8e
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "74984793"
---
# <a name="getting-started-building-games-with-unity-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中开始使用 Unity 生成游戏

Unity 是一款可让你在 C# 中开发游戏的游戏引擎。 本演练演示如何使用 Visual Studio for Mac 和 Visual Studio for Mac Tools for Unity 扩展及 Unity 环境开始开发和调试 Unity 游戏。

Visual Studio for Mac Tools for Unity 是免费扩展，随 Visual Studio for Mac 一起安装。 它使 Unity 开发者能够利用 Visual Studio for Mac 的高效功能，包括出色的 IntelliSense 支持、调试功能等。

## <a name="objectives"></a>目标

> [!div class="checklist"]
> * 了解如何使用 Visual Studio for Mac 进行 Unity 开发

## <a name="prerequisites"></a>先决条件

- Visual Studio for Mac ([https://www.visualstudio.com/vs/mac](https://www.visualstudio.com/vs/visual-studio-mac))
- Unity 5.6.1 Personal Edition 或更高版本（[https://store.unity.com](https://store.unity.com/)，需要 unity.com 帐户才能运行）

## <a name="intended-audience"></a>目标受众

本实验室适用于熟悉 C# 但不具有丰富经验的开发者。

## <a name="task-1-creating-a-basic-unity-project"></a>任务 1：创建基本 Unity 项目

1. 启动 Unity  。 如果要求，请登录。

2. 单击“新建”  。

    ![Unity 中的“新建”按钮](media/unity-image1.png)

3. 将“项目名称”设置为 UnityLab，然后选择 3D    。 单击“创建项目”  。

    ![创建新的项目屏幕](media/unity-image2.png)

4. 你现在看到的是默认 Unity 界面。 界面左侧为游戏对象的场景层次结构，中间显示空白场景的 3D 视图，底部为项目文件窗格，右侧为检查器和服务。 当然，除此之外还有很多部分，但这些是更重要的组成部分。

    ![空白 Unity 界面](media/unity-image3.png)

5. 对于刚接触 Unity 的开发者，在应用中运行的所有内容都将存在于“场景”的上下文中  。 场景文件是一个文件，其中包含各种关于项目中用于当前场景的资源的元数据及其属性。 当你针对某个平台打包应用时，由此产生的应用最终将成为一个或多个场景的集合，包括你添加的所有依赖于平台的代码。 在一个项目中你可以根据需要拥有足够多场景。

6. 新场景中只有照相机和定向光。 场景需要“照相机”才能看到任何内容，需要“音频侦听器”才能听到任何声音   。 这些组件附加到 GameObject  。

7. 从“层次结构”窗格中选择“主照相机”对象   。

    ![“层次结构”窗格中突出显示的主照相机对象](media/unity-image4.png)

8. 从窗口右侧选择“检查器”窗格，可查看其属性  。 照相机属性包括转换信息、背景、投影类型、视野等。 还默认添加音频侦听器组件，它实际上从连接到照相机的虚拟麦克风中呈现场景音频。

    ![“检查器”窗格](media/unity-image5.png)

9. 选择“定向光”对象  。 这将为场景提供光，便于着色器等组件了解如何呈现对象。

    ![突出显示定向光对象](media/unity-image6.png)

10. 使用“检查器”可以看到其中包含常见的光照属性，包括类型、颜色、强度、阴影类型等  。

    ![在“检查器”窗格中查看属性](media/unity-image7.png)

11. 请务必指出 Unity 中的该项目与 Visual Studio for Mac 对应项目略有不同。 在底部的“项目”选项卡中，右键单击“资产”文件夹，然后选择“在查找器中展现”    。

    ![在查找器中展现上下文操作](media/unity-image8.png)

12. 如你所见，项目包含“资产”、“库”、“ProjectSettings”和“Temp”文件夹     。 但是，唯一在界面中显示的文件夹是“资产”文件夹  。 “库”文件夹是导入资产的本地缓存；它为资产保留所有元数据  。 “ProjectSettings”文件夹存储可配置的设置  。 “Temp”文件夹用于生成过程中来自 Mono 和 Unity 的临时文件  。 还有一个解决方案文件可在 Visual Studio for Mac 中打开（此处为 UnityLab.sln）  。

    ![查找器中的资产](media/unity-image9.png)

13. 关闭“查找器”窗口并返回 Unity   。

14. “资产”文件夹中包含你所有的资产 - 艺术品、代码、音频等  。该文件夹此时为空，但你引入项目的每个文件都将进入该文件夹。 这始终是 Unity 编辑器中的顶层文件夹  。 但始终通过 Unity 界面（或 Visual Studio for Mac）添加和删除文件，从不直接通过文件系统添加和删除文件。

    ![Unity 中的资产文件夹](media/unity-image10.png)

15. GameObject 是 Unity 开发的核心，因为几乎所有内容都派生自该类型，包括模型、光、粒子系统等  。 通过依次选择“GameObject”、“3D 对象”、“多维数据集”菜单，将新的“多维数据集”对象添加到场景中   。

    ![场景中的多维数据集对象](media/unity-image11.png)

16. 快速浏览新 GameObject 的属性，并查看该属性是否有名称、标记、层和转换  。 这些属性是所有 GameObjects 共有的  。 此外，几个组件已附加到“多维数据集”，用于提供所需的功能，包括网格筛选器、盒状碰撞体和呈现器  。

    ![游戏对象属性](media/unity-image12.png)

17. 将“多维数据集”对象（默认名称为“多维数据集”）重命名为“敌人”    。 确保按 Enter 保存更改  。 这将是我们的简单游戏中的敌人多维数据集。

    ![多维数据集对象重命名属性](media/unity-image13.png)

18. 使用以上相同过程，将另一个“多维数据集”对象添加到场景中，并将其命名为“玩家”   。

    ![重命名第二个多维数据集对象](media/unity-image14.png)

19. 同样将玩家对象标记为“玩家”（请参阅名称字段下的“标记”下拉控件）   。 我们将在敌人脚本中使用该对象来帮助查找玩家游戏对象。

    ![标记玩家对象](media/unity-image15.png)

20. 在“场景”视图中，使用鼠标沿 Z 轴按照远离敌人对象的方向移动玩家对象  。 通过选择多维数据集并将其从红色面板拖向蓝色行，沿 Z 轴移动   。 由于多维数据集存在于 3D 空间中，但每次只能在 2D 中拖动，因此拖动中心轴尤其重要。

    ![显示多维数据集的场景视图](media/unity-image16.png)

21. 沿轴向下和向右移动多维数据集。 此操作可更新“检查器”中的 Transform.Position 属性   。 请务必拖动到与此处显示的位置类似的位置，以轻松执行实验室中的后续步骤。

    ![沿轴移动一个多维数据集](media/unity-image17.png)

22. 现可添加一些代码，用来驱动敌人逻辑，使其追逐玩家。 右键单击“项目”板中的“资产”文件夹，然后依次选择“创建”、“C# 脚本”    。

    ![C# 脚本上下文操作](media/unity-image18.png)

23. 将新的 C# 脚本命名为 EnemyAI  。

    ![C# 脚本](media/unity-image19.png)

24. 要将脚本附加到游戏对象，请将新创建的脚本拖到“层次结构”窗格中的“敌人”对象上   。 该对象现将使用此脚本中的行为。

    ![突出显示向游戏对象添加脚本](media/unity-image20.png)

25. 依次选择“文件”、“保存场景”，保存当前场景  。 将其命名为 MyScene  。

## <a name="task-2-working-with-visual-studio-for-mac-tools-for-unity"></a>任务 2：与 Visual Studio for Mac Tools for Unity 配合使用

1. 编辑 C# 代码的最佳方法是使用 Visual Studio for Mac。 可以将 Unity 配置为使用 Visual Studio for Mac 作为默认处理程序。 依次选择“Unity”、“首选项”  。

2. 选择“外部工具”选项卡  。从“外部脚本编辑器”下拉列表中，选择“浏览”并选择 Applications/Visual Studio.app    。 或者如果已有 Visual Studio 选项，则只需选择该选项即可  。

    ![首选项中的外部工具选项卡](media/unity-image21.png)

3. Unity 现配置为使用 Visual Studio for Mac 进行脚本编辑  。 关闭“Unity 首选项”对话框  。

    ![在首选项中已选中 Visual Studio](media/unity-image22.png)

4. 双击 EnemyAI.cs，在 Visual Studio for Mac 中打开它   。

    ![在 Unity 中已选中“敌人”资产](media/unity-image23.png)

5. Visual Studio 解决方案非常简单。 其中包含“资产”文件夹（来自查找器的相同文件夹）和之前创建的 EnemyAI.cs 脚本    。 在更复杂的项目中，层次结构可能与你在 Unity 中看到的不同。

    ![Visual Studio for Mac 中的 Solution Pad](media/unity-image24.png)

6. EnemyAI.cs 在编辑器中打开  。 初始脚本仅包含 Start 和 Update 方法的存根   。

7. 用下面的代码替换最初的敌人代码。

    ```csharp
    public class EnemyAI : MonoBehaviour
    {
        public float Speed = 50;
        private Transform _playerTransform;
        private Transform _myTransform;

        void Start()
        {
            var player = GameObject.FindGameObjectWithTag("Player");
            if (!player)
            {
                Debug.LogError(
                    "Could not find the main player. Ensure it has the player tag set.");
            }
            else
            {
                _playerTransform = player.transform;
            }
            _myTransform = this.transform;
        }

        void Update()
        {
            var moveAmount = Speed * Time.deltaTime;
            _myTransform.position = Vector3.MoveTowards(_myTransform.position,
                _playerTransform.position, moveAmount);

            if (_myTransform.position == _playerTransform.position)
            {
                _myTransform.position = Vector3.back * 10;
            }
        }
    }
    ```

8. 快速浏览此处定义的简单敌人行为。 在 Start 方法中，我们可以引用玩家对象（按标记）及其转换   。 在每帧调用的 Update 方法中，敌人将向玩家对象移动  。 关键字和名称使用颜色编码，这样可更容易理解 Visual Studio for Mac 中的代码库。

9. 将更改保存到 Visual Studio for Mac 中的敌人脚本  。

## <a name="task-3-debugging-the-unity-project"></a>任务 3：调试 Unity 项目

1. 在 Start 方法的第一行代码上设置断点  。 可以在目标行上单击编辑器边距，或者将光标放在该行上，然后按 F9  。

    ![在 Visual Studio for Mac 中设置断点](media/unity-image25.png)

2. 单击“开始调试”按钮或按 F5   。 此操作将生成项目并将其附加到 Unity 进行调试。

    ![Visual Studio for Mac 中的“开始”按钮](media/unity-image26.png)

3. 返回 Unity，然后单击“运行”按钮，开始游戏   。

    ![Unity 中的“运行”按钮](media/unity-image27.png)

4. 应命中断点，并且现在可以使用 Visual Studio for Mac 调试工具。

    ![Visual Studio for Mac 中的断点命中](media/unity-image28.png)

5. 在“局部变量”板中，找到引用 EnemyAI 对象的 this 指针    。 展开引用，可发现你可以浏览“速度”等关联成员  。

    ![Visual Studio for Mac 中的局部变量调试板](media/unity-image29.png)

6. 采用与添加断点相同的方法从 Start 方法中删除断点，即在边距中单击断点或选择所在行并按 F9   。

    ![Visual Studio for Mac 中的断点命中](media/unity-image30.png)

7. 按 F10 跳过使用标记作为参数查找“玩家”游戏对象的第一行代码   。

8. 将鼠标光标悬停在代码编辑器窗口中的“玩家”变量上，查看其关联成员  。 你甚至可以展开层叠，查看子属性。

    ![Visual Studio for Mac 编辑器中的调试窗口](media/unity-image31.png)

9. 按 F5 或按“运行”按钮，继续执行操作   。 返回 Unity，查看反复接近玩家多维数据集的敌人多维数据集。 如果照相机不可见，则可能需要进行调整。

    ![Unity 中的场景播放](media/unity-image32.png)

10. 切换回 Visual Studio for Mac 并在 Update 方法的第一行设置断点   。 应该立即击中该断点。

    ![在 Visual Studio for Mac 中设置断点](media/unity-image33.png)

11. 假设速度太快，而我们想要在不重新启动应用的情况下测试更改的影响。 在“自动”或“局部变量”窗口中找到“速度”变量，然后将其更改为“10”并按 Enter      。

    ![在局部变量窗口中调整变量](media/unity-image34.png)

12. 删除断点并按 F5，继续执行操作  。

13. 返回 Unity，查看正在运行的应用程序  。 敌人多维数据集现以原始速度的五分之一移动。

    ![正在运行应用程序的 Unity 窗口](media/unity-image35.png)

14. 再次单击“播放”按钮，停止 Unity 应用  。

    ![停止 Unity 应用](media/unity-image36.png)

15. 返回 Visual Studio for Mac  。 单击“停止”按钮，停止调试会话  。

    ![在 Visual Studio for Mac 中停止调试会话](media/unity-image37.png)

## <a name="task-4-exploring-unity-features-in-visual-studio-for-mac"></a>任务 4：在 Visual Studio for Mac 中探索 Unity 功能

1. Visual Studio for Mac 提供在代码编辑器中快速访问 Unity 文档的功能。 将光标放在 Update 方法中 Vector3 符号的某处，然后按 ⌘ 命令+'    。

    ![在 Visual Studio for Mac 编辑器中选择方法](media/unity-image38.png)

2. 针对 Vector3 的文档，打开新的浏览器窗口  。 满意后关闭浏览器窗口。

    ![针对文档打开浏览器窗口](media/unity-image39.png)

3. Visual Studio for Mac 还提供一些帮助程序用于快速创建 Unity 行为类。 在“解决方案资源管理器”中，右键单击“资产”，然后依次选择“添加”、“新的 MonoBehaviour”    。

    ![新的 MonoBehaviour 上下文操作](media/unity-image40.png)

4. 新创建的类提供 Start 和 Update 方法的存根   。 在 Update 方法的右大括号之后，开始键入 onmouseup   。 键入时，请注意 Visual Studio 的 IntelliSense 会快速将你计划实施的方法归零。 从提供的自动完成列表中选择它。 它将为你填充方法存根，包括任何参数。

    ![Visual Studio for Mac 中的 IntelliSense](media/unity-image41.png)

5. 在 OnMouseUp 方法内，键入 base.   查看可调用的所有基本方法。 还可以使用 IntelliSense 浮出控件右上角的分页选项，探索每个函数的不同重载。

    ![在 Visual Studio for Mac 中探索重载](media/unity-image42.png)

6. Visual Studio for Mac 还使你可以轻松定义新的着色器。 在“解决方案资源管理器”中，右键单击“资产”，然后依次选择“添加”、“新的着色器”    。

    ![Visual Studio for Mac 中的新着色器操作](media/unity-image43.png)

7. 着色器文件格式获得全彩色和字体处理，便于阅读和理解。

    ![语法突出显示](media/unity-image44.png)

8. 返回 Unity  。 你将看到，由于 Visual Studio for Mac 使用相同的项目系统，因此在任一位置所做的更改将自动与另一位置同步。 现可始终轻松地使用最佳工具来完成任务。

    ![Unity 资产面板](media/unity-image45.png)

## <a name="summary"></a>总结

在本实验室中，你已了解了如何使用 Unity 和 Visual Studio for Mac 开始创建游戏。 有关 Unity 的详细信息，请参阅 [https://unity3d.com/learn](https://unity3d.com/learn)。
