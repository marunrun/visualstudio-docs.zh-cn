---
title: 使用性能数据文件保存符号信息 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- packsymbols, in profiling tools reports
- profiling tools, packsymbols
ms.assetid: 8b802505-e94d-4ee0-83e4-fdd790a332c1
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e9d2e8b0414746523d0f76e8266f6463d9c05574
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160287"
---
# <a name="saving-symbol-information-with-performance-data-files"></a>使用性能数据文件保存符号信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 集成开发环境 (IDE) 分析文件并且计划将 VSP 文件移动到其他计算机，则必须设置性能项目设置以在报告文件中保存或序列化  符号。 这会增加报告文件的大小。 出于以下两个原因，需要序列化符号：  
  
- 在目标程序集从它们在临时存储中的位置丢失之前，将代码符号嵌入到性能报告中。  
  
- 保留符号，以便性能报告可从分析的计算机进行移植，当在其他计算机（可能具有不同符号）上打开报告进行分析时可输出相同信息。  
  
  **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  可以从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 或是从命令行序列化符号：  
  
- 要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 中序列化符号，请指向菜单栏上的“工具”  ，然后单击“选项”  。 在“选项”  窗口中，选择“性能工具”  ，然后选中“自动序列化符号信息”  复选框。  
  
- 保存报告文件时，PACKSYMBOLS 是等效命令行选项。 若要序列化符号，请输入 **vsperfreport /summary:all /packsymbols filename.vsp**。  
  
## <a name="troubleshooting-symbol-problems"></a>符号问题疑难解答  
 如果在自己的代码中看不到任何符号，下面提供了一些常见解决方案：  
  
- 在命令行上运行 vsperfreport /debugsympath 以显示探查器组件加载符号信息的位置的完整列表，以及使用的符号文件是否与项目使用的文件匹配。  
  
- 确保使用 /PACKSYMBOLS 标志运行 vsperfreport，或是在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 中，确保在常规性能资源管理器选项中选择了序列化符号信息选项。  
  
- 如果收集了类型数据，请将 /SUMMARY:TYPE 添加到 vsperfreport 命令行。  
  
  如果从 Windows 或其他 Microsoft 程序看不到符号：  
  
- 确保设置了 Windows 符号缓存的路径。 执行以下操作之一以设置符号缓存路径：  
  
  - 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 中将“调试器”->“符号”选项设置为正确路径。  
  
  - 向 VSPerfReport 命令行添加 -symbolpath 选项以包含符号。  
  
- 如果在 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 中看不到任何符号，请确保为 ASP 服务器正确设置了符号服务器。  
  
## <a name="repacking-symbols"></a>重新打包符号  
 如果要将符号重新打包到报告中，可以使用命令行工具 VsPerfReport 执行此操作。 使用以下命令行：  
  
 VsPerfReport -clearpackedsymbols filename.vsp  
  
 VsPerfReport -packsymbols -summary:all filename.vsp  
  
## <a name="see-also"></a>请参阅  
 [保存和导出性能工具数据](../profiling/saving-and-exporting-performance-tools-data.md)   
 [如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)   
 [VSPerfReport](../profiling/vsperfreport.md)
