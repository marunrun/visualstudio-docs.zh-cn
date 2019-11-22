---
title: Prefetch content for Windows Store apps | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: b4481fef-3ebf-4f7d-9748-d43821a0ebac
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4ac6479b4dbb0815374174140deb0d660636ac9e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300517"
---
# <a name="prefetch-content-for-windows-store-apps"></a>预提取 Windows 应用商店应用的内容
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Applies to Windows only](../Image/windows_only_content.png "windows_only_content")  
  
 To make your Windows Store app more responsive, you can request Windows to preload some web content, such as web pages or images, into the app's [WinINet](https://msdn.microsoft.com/0a06f2af-957a-4dff-a8cc-187370181b5c)[WinINet](https://msdn.microsoft.com/library/aa383630.aspx)cache. 此功能称为“预提取”。 它对于启动时使用的内容特别有效，但你也可以预提取其他常用内容。 利用 [Windows.Networking.BackgroundTransfer.ContentPrefetcher](https://msdn.microsoft.com/library/windows/apps/windows.networking.backgroundtransfer.contentprefetcher.aspx) 类的方法，可以指定要预加载的内容的 URI。  
  
 Windows 使用试探法来确定何时及是否应进行预提取，以及将下载哪些资源。 试探法将考虑系统网络和电源情况、用户应用使用情况历史记录和之前预提取尝试的结果。 在 Visual Studio 中，可以使用“触发 Microsoft Store 应用预提取”命令来强制 Windows 忽略 ContentPrefetcher 试探法并预加载所有指定的 Web 内容。 若要在已知状态（已加载或未加载）下使用要预提取的内容测试应用程序的行为或性能，这会很有用。  
  
## <a name="to-force-preloading-of-contentprefetcher-specified-resources"></a>强制预加载 ContentPrefetcher 指定的资源  
 此过程假定你已在应用程序项目中设置 ContentPrefetcher 功能并指定预加载的内容 URI。 若要在指定资源为新的或已修改的资源时强制预加载内容，必须在选择“触发 Microsoft Store 应用预提取”命令之前启动和停止此应用程序。 先运行应用程序以注册 URI。 然后，“触发 Microsoft Store 应用预提取”命令将强制 ContentPrefetcher 下载此内容并将其添加到缓存。 在应用程序的后续运行中，你可以假定已预加载此内容。  
  
1. 启动应用程序以将预提取内容 URI 注册到应用程序。 在“调试”菜单上，选择“开始调试”（键盘快捷键：F5）。  
  
2. 在“调试”菜单上，选择“停止调试”（键盘快捷键：Shift + F5）。  
  
3. 在“调试”菜单上，选择“其他调试目标”，然后选择“触发 Microsoft Store 应用预提取”。  
  
   现在可以利用预提取的 Web 资源来调试、测试或分析应用程序。  
  
> [!NOTE]
> 当你添加或修改指定的 Web 内容时，请重复上述步骤。  
  
## <a name="see-also"></a>请参阅  
 [Blog post: Triggering Prefetch for Windows Store Apps in Visual Studio 2013 Update 2](https://devblogs.microsoft.com/devops/triggering-prefetch-for-windows-store-apps-in-visual-studio-2013-update-2/)
