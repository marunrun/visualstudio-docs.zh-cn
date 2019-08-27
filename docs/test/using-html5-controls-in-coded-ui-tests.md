---
title: 在编码的 UI 测试中使用 HTML5 控件
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: c7087f08743e58426663734295339d9ca6550a0d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926590"
---
# <a name="using-html5-controls-in-coded-ui-tests"></a>在编码的 UI 测试中使用 HTML5 控件

编码的 UI 测试包括对某些包含在 Internet Explorer 9 和 Internet Explorer 10 中的 HTML5 控件的支持。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**要求**

- Visual Studio Enterprise

> [!WARNING]
> 在 Internet Explorer 10 之前的版本中，可以在比 Internet Explorer 进程更高的特权级别中运行编码的 UI 测试。 当在 Internet Explorer 10 中运行编码的 UI 测试时，编码的 UI 测试和 Internet Explorer 进程必须处于相同的特权级别。 这是因为 Internet Explorer 10 提供了更安全的 AppContainer 功能。

> [!WARNING]
> 如果你在 Internet Explorer 10 中创建编码的 UI 测试，则使用 Internet Explorer 9 或 Internet Explorer 8 可能无法运行它。 这是因为 Internet Explorer 10 包含 HTML5 控件（如音频、视频、进度条和滑块）。 Internet Explorer 9 或 Internet Explorer 8 无法识别这些 HTML5 控件。 同样，使用 Internet Explorer 9 的编码的 UI 测试可能包含 Internet Explorer 8 无法识别的某些 HTML5 控件。

## <a name="audio-control"></a>音频控件

**音频控件：** 正确录制和播放 HTML5 音频控件上的操作。

![HTML5 音频控件](../test/media/codedui_html5_audio.png)

|操作|录制|生成的代码|
|-|---------------|-|
|**播放音频**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|从 00:00:00 开始播放 \<名称> 音频|HtmlAudio.Play(TimeSpan)|
|**搜寻音频中的特定时间**|搜寻 \<名称> 音频的 00:01:48|HtmlAudio.Seek(TimeSpan)|
|**暂停音频**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|在 00:01:53 暂停 \<名称> 音频|HtmlAudio.Pause(TimeSpan)|
|**音频静音**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|使 \<名称> 音频静音|HtmlAudio.Mute()|
|**取消静音音频**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|使 \<名称> 音频取消静音|HtmlAudio.Unmute()|
|**更改音频音量**|将 \<名称> 音频的音量设为 79%|HtmlAudio.SetVolume(float)|

有关可在其添加断言的属性列表，请参阅 [HTMLAudioElement](https://developer.mozilla.org/docs/Web/API/HTMLAudioElement)。

**搜索属性：** `HtmlAudio` 的搜索属性为 `Id`、`Name` 和 `Title`。

**筛选器属性：** `HtmlAudio` 的筛选器属性为 `Src`、`Class`、`ControlDefinition` 和 `TagInstance`。

> [!NOTE]
> 定位和暂停的时间可以很长。 在播放期间，编码的 UI 测试将一直等到 `(TimeSpan)` 中指定的时间再暂停音频。 如果由于某种特殊情况，过了指定的时间才命中暂停命令，将引发异常。

## <a name="video-control"></a>视频控件
**视频控件：** 正确录制和播放 HTML5 视频控件上的操作。

![HTML5 视频控件](../test/media/codedui_html5_video.png)

|操作|录制|生成的代码|
|-|---------------|-|
|**播放视频**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|从 00:00:00 开始播放 \<名称> 视频|HtmlVideo.Play(TimeSpan)|
|**搜寻视频中的特定时间**|搜寻 \<名称> 视频的 00:01:48|HtmlVideo.Seek(TimeSpan)|
|**暂停视频**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|在 00:01:53 暂停 \<名称> 视频|HtmlVideo.Pause(TimeSpan)|
|**视频静音**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|使 \<名称> 视频静音|HtmlVideo.Mute()|
|**取消静音视频**<br /><br /> 直接通过控件，或通过控件的右键单击菜单。|使 \<名称> 视频取消静音|HtmlVideo.Unmute()|
|**更改视频音量**|将 \<名称> 视频的音量设为 79%||

有关可在其添加断言的属性列表，请参阅 [HTMLVideoElement](https://developer.mozilla.org/docs/Web/HTML/Element/video)。

**搜索属性：** `HtmlVideo` 的搜索属性为 `Id`、`Name` 和 `Title`。

**筛选器属性：** `HtmlVideo` 的筛选属性为 `Src`、`Poster``Class``ControlDefinition` 和 `TagInstance`。

> [!NOTE]
> 如果使用 -30s 或 +30s 标签对视频后退或快进，将聚合标签以定位到相应的时间。

## <a name="progressbar"></a>ProgressBar
**进度条控件：** 进度条是一种不可交互的控件。 你可以对此控件的 `Value` 和 `Max` 属性添加断言。 有关详细信息，请参阅 [HTMLProgressElement](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress)。

![HTML5 进度条控件](../test/media/codedui_html5_progressbar.png)

## <a name="see-also"></a>请参阅

- [HTML 元素](https://developer.mozilla.org/docs/Web/HTML/Element)
- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)
- [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
