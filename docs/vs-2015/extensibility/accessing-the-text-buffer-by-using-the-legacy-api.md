---
title: 使用旧 API 访问文本缓冲区 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text buffers
ms.assetid: cd6cf4ae-fff5-4e23-b293-7cbafdb8aed2
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f2cfbd84bc4f9298358a2a2d1ba87f76d6e5303c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185004"
---
# <a name="accessing-the-text-buffer-by-using-the-legacy-api"></a>使用旧版 API 访问文本缓冲区
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本负责管理文本流和文件持久性。 尽管缓冲区可以读取或写入其他格式，但使用 Unicode 执行与缓冲区的所有普通通信。 在旧 Api 中，文本缓冲区可以使用单或二维坐标系统来标识缓冲区中的字符位置。  
  
## <a name="one--and-two-dimension-coordinate-systems"></a>一维坐标系统和二维坐标系统  
 一维坐标位置基于缓冲区中第一个字符的字符位置，例如147。 使用接口可以 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream> 访问缓冲区中的一维位置。 二维坐标系统基于行和索引对。 例如，位于43，5的缓冲区中的字符将在行43，第5个字符在该行的第一个字符右侧。 使用接口访问缓冲区中的二维位置 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> 。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream> 接口都是由 () 的文本缓冲区对象实现的， <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 并且可以使用从彼此访问 `QueryInterface` 。 下图显示了上的这些和其他密钥接口 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 。  
  
 ![文本缓冲区对象](../extensibility/media/vstextbuffer.gif "vsTextBuffer")  
文本缓冲区对象  
  
 尽管坐标系统在文本缓冲区中起作用，但它经过优化，可使用二维坐标。 一维坐标系统可能会产生性能开销。 因此，请尽可能使用二维坐标系统。  
  
 文本缓冲区的第二个责任是文件暂留。 为此，文本缓冲区对象实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 并充当持久性所涉及的项目项和其他环境组件的文档数据对象组件。 有关详细信息，请参阅 [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [使用旧版 API 更改视图设置](../extensibility/changing-view-settings-by-using-the-legacy-api.md)  
 介绍如何使用旧版 API 更改视图设置。  
  
 [使用文本管理器监视全局设置](../extensibility/using-the-text-manager-to-monitor-global-settings.md)  
 介绍如何使用文本管理器监视全局设置。  
  
## <a name="see-also"></a>另请参阅  
 [核心编辑器内](../extensibility/inside-the-core-editor.md)
