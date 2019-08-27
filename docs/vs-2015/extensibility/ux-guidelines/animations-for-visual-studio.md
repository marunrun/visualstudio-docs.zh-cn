---
title: Animations
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 446773a9-e6f7-4c0c-8dbc-9e303bf32eb1
caps.latest.revision: 3
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c07fb0887ae01ec917b39f5d7537d5a78fb5a4c6
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825356"
---
# <a name="animations-for-visual-studio"></a>Visual Studio 的动画
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="animation-fundamentals"></a>动画基础知识

### <a name="animation-best-practices-in-visual-studio"></a>在 Visual Studio 中的动画最佳实践
 请遵循这些规则，以确保一致且易于动画样式在整个 Visual Studio IDE。

- **为选择性。** 限制为特定目的的动画。

- **计时和速度非常重要，** 以确保转换感觉快速和自然：

  - 半秒 （500 毫秒） 内完成动画的过渡。

  - 将发生的频率的动画需要快速，它们不会中断用户的工作流。

  - 因此快速或他们疑惑不解，它是难以理解，但不是速度很慢，它可用于一个耐心转换完成，不应为动画。

  - 使用变量计时强调重要性。 例如，导航时通过一系列在类图上的项，项之间的转换通过速度则速度下降，以专注于重要事项。

- **通过逐步非线性缓动**从一个状态到另一个，使冷静和自然移动的了解

- 如果可能，请**悬停时的使用微动画**以指示在鼠标交互元素。

- 如果您依赖于动画中您的功能然后**提供一种方法要关闭它们**本地 （适用于所有功能） 中的一个选项作为**工具 > 选项**对话框。

- **只有一个动画应发生一次**和传达只是一条信息。

- **一个要点非常重要。** 在大多数情况下动画不具有到需用户采取行动，以提供其用途。 细微计时、 序列化和行为中的更改可能会显著影响感知，并且可以使有效和无效动画之间的差异。

- 当使用动画来吸引对某件事情，注意**确保，因此有必要中断用户**的思路。

- **显示进度或状态时**通过动画：

  - 不再显示进度移动时不前移基本过程。

  - 确定进程区分开来不确定的进程。

  - 请确保动画具有可识别的完成和失败状态。

  - 最小化效果动画显示状态并确保它们具有真正的价值，通过提供的实际应用中的其他信息的使用。 示例包括暂时性的状态更改和紧急情况

#### <a name="do-not"></a>不要：

- 使用小移动 （在内存占用较小的运动），首选淡并更改通过移动对象。

- 使用屏幕空间在较大区域上发生的动画。 而不考虑大小，这种样式是动画的让人分散注意力到该用户。

- 使用不与用户正在致力于提供的对象或与之交互的动画。

- 使用需要用户交互才能重置状态，例如，强制用户响应以使其停止闪烁闪烁通知的动画。 以任何方式与它们交互应足以消除它们。

  这些最佳实践的应用程序的详细信息，请参阅[动画模式](../../extensibility/ux-guidelines/animations-for-visual-studio.md#BKMK_AnimationPatterns)。

### <a name="animation-metrics"></a>动画指标

- 系统应以可视方式响应用户操作以小于 10 毫秒为单位。

- 动画的过渡不应超过 500 毫秒才能完成。

- 一种方法来弥补的转换，需要更长的时间是分离到两个部分：例如，动画的第一个部分可能是到容器 （最多 500 毫秒） 后跟内容淡入淡出空内容容器 （最多 500 毫秒）。

- 对于可以计算的加载时间、 决定进度指示器 （%完成进度指示器） 是首选。

- 为不能计算的加载时间，例如游标或嵌入的旋转动画 （加载或工作指示器） 忙碌状态指示器适合。

### <a name="animation-as-communicator"></a>作为 communicator 的动画
 在 Visual Studio UI 中，动画函数只能作为通信工具。  它用于通信的各种信息，例如在用户界面; 中的结构更改例如，当一个菜单，打开或关闭。 动画可以帮助您可视化复杂系统，例如安装正在进行可视化的时间相关的行为，或用于吸引注意力使用警报和通知。

 UI 动画函数，通常在四种方法： 可视化、 吸引注意力，模拟，并指示响应时间/进度。

#### <a name="visualize"></a>可视化
 动画可以强调三维对象的性质，并使用户更轻松地可视化其空间的结构。 若要实现此目的，动画可能需要旋转一整圈中的对象缓慢，并且反复打开或将对象更接近和会略微增加其大小以强调滚动更新或焦点。

 尽管三维对象可能会在移动与用户控件 （以编程方式或手动），在设计器应提前确定如何最适合进行动画处理提供了最佳了解对象的移动。 此动画可以进行编程，然后激活由用户通过将光标放置的对象，而用户控制移动需要用户若要了解如何操作对象。 将移动限制为单个轴或一次; 的方向可以缩放、 旋转，或转换，但不同时执行多个。

 可视化类别包括的方面的数据、 关系、 状态、 结构、 序列和时间。

##### <a name="data"></a>数据
 演示了复杂和变量信息：

- 移动通过信息可视化效果，如图表和图形

- 通过一系列单步执行、 指导的教程和分页

- 调用详细信息，指向，和突出显示的特定信息

- 覆盖详细信息和顶部具有焦点的元素的其他信息

- 到另一个结构或组织的表示形式变形

- 持续使用时间滑块、 慢走 shuttle 车轮和传输控件 （播放、 停止和暂停） 表示的更改。

##### <a name="relationships"></a>关系

- 说明了项之间的相互或与给定项相关的项。

- 显示层次结构和父-子链接或同级关系

- 一个元素会生成另一个

- 一个元素到另一个元素最小化

- 已接入的到另一个元素

##### <a name="state"></a>状态

- 内容更新。

- 用户焦点和选择内容

- 进度

- 错误

##### <a name="structure"></a>结构

- 正在切换一个节点上的结构

- 重定向

- 最小化和最大化，或展开和折叠

##### <a name="sequence"></a>序列

- 幻灯片放映序列

- 逐一浏览图片

##### <a name="time"></a>时间

- 显示随时间、 时间失效和截屏视频

- 将移动以放入回收站、 撤消和重做

- 还原历史记录状态

#### <a name="attract-attention"></a>吸引注意力
 如果目标是要绘制为单个元素从多个用户的注意力，或更新的信息向用户发出警报，则动画可能比较合适。 例如，你的应用程序起始页可能会采用滑入到位，在页面加载后的开始按钮。

 通常，在屏幕上的最后一个移动元素方面吸引用户的注意力。  在动画元素的一系列，将用户的注意力将遵循的最后一个移动对象。

##### <a name="alert"></a>警报

- 警报用户、 引起注意，显示进度

- 显示的执行某些操作正在正确或不正确或显示进度或正在进行的更改

- 在一个任务，例如查找的详细联机信息或了解当前任务过程中提示用户

##### <a name="notifications"></a>通知

- 用户的错误条件发出警报

- 中断用户，请参阅是否他们想要处理其他事项

- 轻轻地通知过程已完成或发生更改，如完成下载后的用户。

#### <a name="simulate"></a>模拟
 此类别包含 physicality 和维数。

- 说明对象来自何处或转到其中

- 展开和折叠或打开和关闭

- 平移、 滚动和页面启用

- 堆栈和 z 顺序

- 轮播和可折叠面板

- 翻转和旋转用户界面

#### <a name="response-and-progress-indicators"></a>响应和进度指示器
 进度指示器等有几个值得注意的优点：

- 这两个确定并不确定的进度指示器等我们发现的用户的系统未损坏，着手解决的问题。

- 确定指示器授予该用户的某种意义上，以及操作时的进展情况，以及获取更接近于完成的感觉。

## <a name="BKMK_AnimationPatterns"></a> 动画模式

### <a name="overview"></a>概述
 在 Visual Studio 中的动画用于充当特定的功能并不会影响用户工作效率。 若要符合以包括常规动画特征：

- 小型和非介入式

- 自然而真实

- 微妙、 subdued

- 快速且高效

- 放松、 不名匆忙之中

  下图显示了建议在 Visual Studio 中使用的动画样式。 没有动画和精致的动画效果如淡入/淡出最常使用。 有限的应用程序的移动动画如扩展和收缩，X 和 Y 位置更改和旋转。

  ![Visual Studio 的建议动画样式](../../extensibility/ux-guidelines/media/1202-a-vsanimstyles.png "1202 a_VSAnimStyles")

  **Visual Studio 的建议的动画样式**

#### <a name="appear-and-disappear"></a>显示和隐藏
 使用此模式时，元素的切换可见从返回，而不转换动画和扩展视图：

 ![显示&#47;消失 Visual Studio 中的动画](../../extensibility/ux-guidelines/media/1202-b-appearanddisappear.png "1202 b_AppearAndDisappear")

##### <a name="correct-usage"></a>正确用法
 需要立即显示或消失，以便用户是将注意力集中既不挡住全新的 UI 元素。 此外，缓慢移动动画可能会被视为性能拖动，不会发生与出现和消失样式。

##### <a name="incorrect-usage"></a>不正确的用法
 在其中用户界面出现突然用户完全不知道发生了什么情况，并将动画添加与上下文的理解将帮助的情况。

##### <a name="animation-properties"></a>动画属性
 时间延迟通常是零秒。

##### <a name="examples"></a>示例

- 自动隐藏工具窗口

- 键盘激活编辑器 UI，例如智能感知和参数帮助

- 展开折叠代码区域

#### <a name="fade-in-and-fade-out"></a>淡入和淡出
 UI 元素不可见 （0%不透明） 从使用此模式时，将转换为可见 （100%不透明），反之亦然：

 ![淡入&#45;中&#47;淡入&#45;Visual Studio 中的动画 out](../../extensibility/ux-guidelines/media/1202-c-fadeinfadeout.png "1202 c_FadeInFadeOut")

##### <a name="correct-usage"></a>正确用法
 这是最常用建议 UI 动画。 它是添加感兴趣，而不中断流的细微效果。 在某些情况下，用户可能没有甚至意识到认为存在是一个动画，并只是感觉流动的平滑 UI 系统。

##### <a name="animation-properties"></a>动画属性

- 从开始不透明度：淡入淡出的 100%的 0%

- 停用不透明度：淡入淡出的 0%的 100%

- 持续时间：是独立 200 毫秒，100 毫秒时用作组合动画序列的一部分

- 缓动样式：InOut 正弦值

##### <a name="examples"></a>示例

- 自动隐藏工具窗口

- 菜单打开和关闭

- 前景色和背景选项卡转换

#### <a name="color-blend-from-a-to-b"></a>从 A 到 B 的颜色混合
 使用此模式时，UI 元素更改从一个颜色为颜色 b:

 ![Visual Studio 中的动画的颜色混合](../../extensibility/ux-guidelines/media/1202-d-colorblend.png "1202 d_ColorBlend")

##### <a name="correct-usage"></a>正确用法
 为 UI 元素从一个上下文或状态到另一个更改颜色时的动画转换。

##### <a name="animation-properties"></a>动画属性

- 开始颜色：特定于 UI

- 结束色：特定于 UI

- 持续时间：是独立 200 毫秒，100 毫秒时用作组合动画序列的一部分

- 缓动样式：InOut 正弦值

##### <a name="examples"></a>示例

- 文档窗口状态转换 (处于活动状态，最后处于活动状态，以及处于非活动状态)

- 工具窗口状态转换 （有针对性和失去焦点）

#### <a name="expand-and-contract"></a>扩展和收缩
 使用此模式时，UI 元素会在 X、 Y、 或两个方向中展开：

 ![展开&#47;协定 Visual Studio 中的动画](../../extensibility/ux-guidelines/media/1202-e-expandcontract.png "1202 e_ExpandContract")

##### <a name="correct-usage"></a>正确用法
 为 UI 元素到另一个上下文从更改大小时的动画转换。

##### <a name="animation-properties"></a>动画属性

- 缩放 x: %或特定的尺寸 （以像素为单位）

- Y 小数位数: %或特定的尺寸 （以像素为单位）

- 定位点位置：通常 （对于从左到右的语言） 的左上角或右上方 （对于从右到左的语言）

- 持续时间：是独立 200 毫秒，100 毫秒时用作组合动画序列的一部分

##### <a name="examples"></a>示例

- 体系结构资源管理器面板展开和折叠

- 起始的页项目展开和折叠

#### <a name="x-y-position-change"></a>X，Y 位置更改
 使用此模式时，UI 元素更改和 / 或其 X 或 Y 位置：

 ![X&#47;y 轴位置更改 Visual Studio 中的动画](../../extensibility/ux-guidelines/media/1202-f-xypositionchange.png "1202 f_XYPositionChange")

##### <a name="correct-usage"></a>正确用法
 为 UI 元素到另一个上下文从更改位置时的动画转换。

##### <a name="animation-properties"></a>动画属性

- 从 X 和 Y 位置：特定于 UI

- 结束 X 和 Y 位置：特定于 UI

- 运动路径：无

- 持续时间：是独立 200 毫秒，100 毫秒时用作组合动画序列的一部分

- 缓动样式：InOut 正弦值

##### <a name="example"></a>示例
 选项卡重新排序

#### <a name="rotate"></a>旋转
 使用此模式时，UI 元素旋转：

 ![Visual Studio 中的旋转动画](../../extensibility/ux-guidelines/media/1202-g-rotate.png "1202 g_Rotate")

##### <a name="correct-usage"></a>正确用法
 仅对不确定旋转进度指示器。

##### <a name="animation-properties"></a>动画属性

- 旋转度数：360

- 旋转中心：该对象的中间

- 持续时间：Continuous

##### <a name="example"></a>示例
 不确定的进度指示器 （旋转）

### <a name="common-shell-ui-actions-and-recommended-animations"></a>常见 shell UI 操作和建议的动画

#### <a name="tab-open"></a>选项卡上打开

- 样式：显示

- 持续时间：零秒

  ![选项卡上的 Visual Studio 中的打开动画](../../extensibility/ux-guidelines/media/1202-h-tabopen.png "1202 h_TabOpen")

#### <a name="tab-close"></a>关闭选项卡

- 样式：X 位置更改

- 持续时间：200 毫秒

  ![选项卡上的 Visual Studio 中的关闭动画](../../extensibility/ux-guidelines/media/1202-i-tabclose.png "1202 i_TabClose")

#### <a name="tab-reorder"></a>选项卡重新排序

- 样式：X 位置更改

- 持续时间：200 毫秒

  ![选项卡上的 Visual Studio 中的重新排序动画](../../extensibility/ux-guidelines/media/1202-j-tabreorder.png "1202 j_TabReorder")

#### <a name="close-floating-document"></a>关闭浮动文档

- 样式：显示

- 持续时间：200 毫秒

  ![关闭 Visual Studio 中浮动文档动画](../../extensibility/ux-guidelines/media/1202-k-closefloatingdocument.png "1202 k_CloseFloatingDocument")

#### <a name="window-state-transition"></a>窗口的状态转换

- 样式：若要与其他 windows 保持一致，让当前操作系统定义文档关闭动画。

- 持续时间：200 毫秒

  ![在 Visual Studio 中的窗口状态过渡动画](../../extensibility/ux-guidelines/media/1202-l-windowstatetransition.png "1202 l_WindowStateTransition")

#### <a name="menu-open"></a>打开菜单

- 样式：淡入

- 持续时间：200 毫秒

  ![在 Visual Studio 中的菜单打开动画](../../extensibility/ux-guidelines/media/1202-m-menuopen.png "1202 m_MenuOpen")

#### <a name="menu-close"></a>关闭菜单

- 样式：Fade-out

- 持续时间：200 毫秒

  ![在 Visual Studio 中的菜单关闭动画](../../extensibility/ux-guidelines/media/1202-n-menuclose.png "1202 n_MenuClose")

#### <a name="auto-hide-tool-window-reveal"></a>自动隐藏工具窗口显示

- 样式：显示

- 持续时间：零秒

  ![自动&#45;隐藏在 Visual Studio 中的工具窗口动画](../../extensibility/ux-guidelines/media/1202-o-autohidetoolwindowreveal.png "1202 o_AutoHideToolWindowReveal")
