---
title: 演练： 调试多线程应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- multithreaded debugging, walkthrough
- walkthroughs, multithreaded debugging
ms.assetid: 590ffd57-0556-43d8-8962-ee27e5b2b7d7
caps.latest.revision: 42
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a13fa717cc7f3952e44fe0dffecf735e7b53345a
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47480637"
---
# <a name="walkthrough-debugging-a-multithreaded-application"></a>演练：调试多线程应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[调试使用线程窗口的多线程应用](https://docs.microsoft.com/visualstudio/debugger/how-to-use-the-threads-window)。  
  
[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 提供了改进**线程**窗口和其他用户界面改进，从而使其更易于调试多线程应用程序。 本演练只需几分钟即可完成，但完成后您将熟悉用于调试多线程应用程序的一些新增界面功能。  
  
 若要开始本演练，您需要创建一个多线程应用程序项目。 请按照下面列出的步骤创建该项目。  
  
#### <a name="to-create-the-walkthrough-project"></a>创建演练项目  
  
1.  上**文件**菜单中，选择**新建**，然后单击**项目**。  
  
     此时将出现 “新建项目” 对话框。  
  
2.  在中**项目类型**s 框中，单击所选的语言： **Visual Basic**， **Visual C#**，或者**Visual c + +**。  
  
3.  在中**模板**框中，选择**控制台应用程序**或**CLR 控制台应用程序**。  
  
4.  在中**名称**框中，键入名称 MyThreadWalkthroughApp。  
  
5.  单击 **“确定”**。  
  
     新的控制台项目随即显示。 创建该项目后，将显示源文件。 根据所选的语言，源文件的名称可能是 Module1.vb、Program.cs 或 MyThreadWalkthroughApp.cpp  
  
6.  删除出现在源代码文件中的代码并替换该主题的"创建线程"的部分中显示的示例代码[创建线程并传递数据的开始时间](http://msdn.microsoft.com/library/52b32222-e185-4f42-91a7-eaca65c0ab6d)。  
  
7.  上**文件**菜单上，单击**全部保存**。  
  
#### <a name="to-begin-the-walkthrough"></a>开始演练  
  
-   在源窗口中查找以下代码：  
  
    ```vb  
    Thread.Sleep(3000)   
    Console.WriteLine(  
    ```  
  
```csharp  
Thread.Sleep(3000);  
Console.WriteLine();  
```  
  
```cpp  
Thread::Sleep(3000);  
Console.WriteLine();  
```  
  
#### <a name="to-start-debugging"></a>开始调试  
  
1.  右键单击`Console.WriteLine`语句中，依次指向**断点**，然后单击**插入断点**。  
  
     在源窗口左侧的滚动条槽中将显示一个红色球。 这表示现在已在该位置设置了一个断点。  
  
2.  在“调试”菜单上，单击“启动调试”。  
  
     调试开始，您的控制台应用程序开始运行，随后在断点处停止。  
  
3.  如果此时控制台应用程序窗口具有焦点，请在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 窗口中单击以使焦点返回到 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
4.  在源窗口中，找到包含以下代码的行：  
  
    ```vb  
    Thread.Sleep(5000)   
    ```  
  
```csharp  
Thread.Sleep(3000);  
```  
  
```cpp  
Thread::Sleep(3000);  
```  
  
1.  
  
#### <a name="to-discover-the-thread-marker"></a>发现线程标记  
  
1.  在中右击**线程**窗口中，然后单击**在源中显示线程**。  
  
2.  查看窗口左侧的滚动条槽。 在这条槽线上，您将看到一个类似于两根细线的图标。 一根线是红色的，另一根是蓝色的。 线程标记指示线程在此位置停止。 线程有可能在此位置停止。  
  
3.  将指针悬停在线程标记上。 数据提示随即显示。 数据提示将告诉您每个已停止线程的名称和线程 ID 号。 在此情况下，只有一个线程，其名称可能是 `<noname>`。  
  
4.  右击线程标记。 请注意快捷菜单上的选项。  
  
 此图标是*线程标记*:  
  
 ![线程标记](../debugger/media/threadmarker.gif "ThreadMarker")  
  
## <a name="flagging-and-unflagging-threads"></a>标记线程和取消标记线程  
 在 [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] 中，可以标记要格外关注的线程。 标记线程是一种跟踪重要线程并忽略您不关心的线程的好方法。  
  
#### <a name="to-flag-threads"></a>标记线程  
  
1.  上**视图**菜单，依次指向**工具栏**。  
  
     请确保**调试位置**选中工具栏。  
  
2.  转到**调试位置**工具栏，然后单击**线程**列表。  
  
    > [!NOTE]
    >  可以通过三个突出显示的列表来识别此工具栏：**进程**，**线程**，并**堆栈帧**。  
  
3.  请注意列表中显示的线程数目。  
  
4.  返回到源窗口中，然后右键单击**线程**再次标记。  
  
5.  在快捷菜单上，指向**标志**，然后单击线程名称和 ID 号。  
  
6.  返回到**调试位置**工具栏，然后单击**线程**再次列出。  
  
     现在只有标记的线程显示在该列表中。 标记按钮的右侧**线程**列表。 之前该按钮上的标记图标灰显， 现在显示为纯鲜红色。  
  
7.  将指针悬停在标记图标上。  
  
     弹出消息随即显示。 此弹出消息告诉您所处的模式**线程**列表：**仅显示标记的线程**。  
  
8.  单击标记按钮切换回**显示所有线程**模式。  
  
9. 单击**线程**再次列出并验证，您可以立即再次看到所有线程。  
  
10. 单击标记按钮切换回**仅显示标记的线程**。  
  
11. 上**调试**菜单，依次指向**Windows** ，然后单击**线程**。  
  
     **线程**窗口会显示。 其中有一个线程上附加了突出显示的标记图标。  
  
12. 在源窗口中再次右击线程标记。  
  
     请注意此时快捷菜单上提供的选项。 而不是**标志**，现在你会看到**取消标记**。 不要单击**取消标记**。  
  
13. 转到有关如何取消标记线程的下一个过程。  
  
#### <a name="to-unflag-threads"></a>取消标记线程  
  
1.  上**线程**窗口中，右键单击标记的线程与对应的行。  
  
     一个快捷菜单随即显示。 其中包括选项**取消标记**并**取消标记所有**。  
  
2.  若要取消标记线程，请单击**取消标记**。  
  
3.  单击红色的标记图标。  
  
4.  看看**调试位置**再次工具栏。 标记按钮再次灰显。 这是因为您已取消标记唯一的已标记线程。 由于没有已标记的线程，工具栏已将返回到**显示所有线程**模式。 单击**线程**列出并验证是否可以看到所有线程。  
  
5.  返回到**线程**窗口，并检查信息列。  
  
     在每一列顶部，大多数按钮都带有相应的标题，用于标识该列。 不过，左侧的第一列上没有标题， 而是显示了一个图标，即标记的边框。 您将注意到该线程列表的每一行中有相同的边框。 该边框意味着该线程已取消标记。  
  
6.  单击两个线程（即从列表底部起的第二和第三个线程）的标记边框。  
  
     标记图标变为纯红色，而非空心边框。  
  
7.  单击该标记列顶部的按钮。  
  
     单击该按钮时，线程列表的顺序将会改变。 此时，线程列表的排序形式为标记的线程位于顶部。  
  
8.  再次单击该标记列顶部的按钮。  
  
     排序顺序再次改变。  
  
## <a name="more-about-the-threads-window"></a>有关“线程”窗口的更多信息  
  
#### <a name="to-learn-more-about-the-threads-window"></a>了解有关“线程”窗口的更多信息  
  
1.  在中**线程**窗口中，检查从左侧的第三个列。 在此列顶部的按钮**ID**。  
  
2.  单击**ID**。  
  
     此时，线程列表按照线程 ID 号排序。  
  
3.  右击列表中的任意线程。 在快捷菜单上，单击**十六进制显示**。  
  
     线程 ID 号的格式将会改变。  
  
4.  将鼠标指针悬停在列表中的任意线程上。  
  
     经过短暂的延迟后，将会出现数据提示。 其中显示线程的部分调用堆栈。  
  
5.  查看第四个列，从标记为左**类别**。 线程按类别分类。  
  
     进程中创建的第一个线程称为主线程。 请在线程列表中找到它。  
  
6.  右击主线程，然后单击**切换到线程**。  
  
     一个警告对话框随即显示。 它通知您 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 无法显示主线程的源代码。  
  
     单击 **“确定”**。  
  
7.  看看**调用堆栈**窗口和**调试位置**工具栏。  
  
     内容**调用堆栈**窗口已更改。  
  
## <a name="switching-the-active-thread"></a>切换活动线程  
  
#### <a name="to-switch-threads"></a>切换线程  
  
1.  在中**线程**窗口中，检查从左侧的第二个列。 此列顶部的按钮上没有文本或图标。 此列为**活动线程**列。  
  
2.  看看**活动线程**列，请注意，一个线程带有黄色箭头。 这是*活动线程指示符*。  
  
3.  记下活动线程指示符所在位置的线程 ID 号。 您可以将活动线程指示符移到另一个线程，但在完成操作后必须将其移回原位。  
  
4.  右键单击另一个线程，然后单击**切换到线程**。  
  
5.  看看**调用堆栈**源窗口中的窗口。 其内容已经更改。  
  
6.  看看**调试位置**工具栏。 其中的活动线程也已更改。  
  
7.  转到**调试位置**工具栏。 单击**线程**框并从下拉列表中选择不同的线程。  
  
8.  看看**线程**窗口。 活动线程指示符已经更改。  
  
9. 在源窗口中右击线程标记。 在快捷菜单上，指向**切换到**单击线程名称 /ID 号。  
  
     您现在已经了解更改活动线程的三种方法： 使用**线程**窗口中，**线程**框中**调试位置**工具栏和中的线程指示符源窗口。  
  
     使用线程指示符只能切换到在特定位置停止的线程。 通过使用**线程**窗口和**调试位置**工具栏中，您可以切换到任何线程。  
  
## <a name="freezing-and-thawing-thread-execution"></a>线程执行的冻结和解冻  
  
#### <a name="to-freeze-and-unfreeze-threads"></a>冻结和解冻线程  
  
1.  在中**线程**窗口中，右击任何线程，然后单击**冻结**。  
  
2.  查看活动线程列。 此时该列中出现一对竖线。 这两条蓝色竖线表示该线程已冻结。  
  
3.  看看**挂起**列。 此时线程的挂起计数是 1。  
  
4.  右击冻结的线程，然后单击**解冻**。  
  
     活动线程列和**挂起**列发生更改。  
  
## <a name="see-also"></a>请参阅  
 [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [如何：在调试时切换到另一个线程](../debugger/how-to-switch-to-another-thread-while-debugging.md)


