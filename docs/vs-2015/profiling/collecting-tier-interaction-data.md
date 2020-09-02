---
title: 收集层交互数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.tierinteraction
helpviewer_keywords:
- Profiling Tools,ADO.NET profiling
- tier interaction profiling method
- Profiling Tools,tier-interaction method
- ADO.NET performance profiling
ms.assetid: 47a944c2-3098-497c-8fc7-e1f43d750bbc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a20266c870316be9b6be67e661d13eb4e6fdbaee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62568042"
---
# <a name="collecting-tier-interaction-data"></a>收集层交互数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

层交互分析提供有关多层应用程序函数执行时间的附加信息，这些应用程序通过 ADO.NET 服务与数据库进行通信。 仅针对同步函数调用收集数据。  
  
 **Visual Studio 版本**  
  
 层交互分析数据可使用 Visual Studio 旗舰版、Visual Studio 高级专业版或 Visual Studio 专业版来收集。 但是，层交互分析数据只能在 VS 旗舰版和 VS 高级专业版中查看。  
  
 **Windows 8 和 Windows Server 2012**  
  
 若要收集有关 Windows 8 桌面应用 和 Windows Server 2012 应用的层交互数据，必须使用检测方法。 不能收集 Windows 应用商店应用的层交互数据。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。 您可以在所有分析方法中包含有关其他支持的 Windows 版本的层交互数据。  
  
 **性能向导**  
  
 由于性能向导中的一个 Bug，您必须从性能资源管理器将层交互数据收集选项添加到性能运行。 还必须将项目、可执行文件或网站添加到性能资源管理器的目标节点。  
  
### <a name="to-add-tier-interaction-data-to-a-profiling-run-by-using-the-performance-session-property-pages"></a>使用性能会话属性页将层交互数据添加到分析运行中  
  
1. 在“性能资源管理器”中，从上下文菜单中选择“属性”  。  
  
2. 选择“层交互”  页，然后选中“启用层交互分析”  复选框。  
  
3. 在“性能资源管理器”中，选择“目标”  节点，然后指定要分析的项目、可执行文件或网站。  
  
## <a name="see-also"></a>另请参阅  
 [“层交互”视图](../profiling/tier-interactions-view.md)
