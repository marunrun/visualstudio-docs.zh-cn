---
title: 如何：将检测限定为特定函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, limiting instrumentation to functions
ms.assetid: bd98d6bf-2560-4eba-b063-2facb09f87c4
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8923323a3aed96a9dd441a4a36b2084ffd8197e6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432650"
---
# <a name="how-to-limit-instrumentation-to-specific-functions"></a>如何：为特定函数的限制规范
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过在“性能会话”属性页的“高级”页或目标二进制文件的属性页中设置选项，可以将检测和数据收集限定为一个或多个函数：  
  
- 如果在性能会话的属性页上指定函数，则仅检测会话的所有受检测二进制文件中的函数。  
  
- 如果在目标二进制文件的属性页上指定函数，则仅检测该特定二进制文件中的函数。 性能会话的其他二进制文件中的函数照常受到检测。  
  
  仅当选择检测分析方法时，才支持以此方式限制数据收集。  
  
> [!NOTE]
> 还可以使用“性能会话”属性页的“高级”页来设置可用于分析工具 [VSInstr](../profiling/vsinstr.md) 命令行检测工具的其他选项。  
  
### <a name="to-limit-instrumentation-to-specific-functions-in-a-performance-session"></a>将检测限定为性能会话中的特定函数  
  
1. 在“性能资源管理器”中，右键单击会话名称，然后单击“属性”。  
  
    随即显示“属性页”对话框。  
  
2. 在“属性页”对话框中，单击“高级”。  
  
3. 在“其他检测选项”文本框中，使用以下语法键入要检测的函数的名称：  
  
    **/include:** `FuncSpec` **[;** `FuncSpec` **]** `...`  
  
    `FuncSpec` 是命名空间和函数名。 其格式为 `Namespace`**::**`FunctionName`。 可使用分号分隔多个函数。 可使用星号 (\*) 指定一个或多个字符的通配符。 例如，/include:MyNS::\\* 指定 MyNS 命名空间中的所有函数。  
  
   > [!NOTE]
   > 若要列出某个二进制文件中的函数，请在分析工具安装目录（通常是 [!INCLUDE[vsprvsts](../includes/vsprvsts-md.md)]安装目录下的 \Team Tools\Performance Tools 目录）中打开命令提示符窗口，然后键入 **vsinstr /DumpFuncs**  
  
### <a name="to-limit-instrumentation-to-specific-functions-in-a-binary"></a>将检测限定为二进制文件中的特定函数  
  
1. 在“性能资源管理器”中，在性能会话的“目标”节点中找到二进制文件名称。  
  
2. 右键单击该二进制文件名称，然后单击“属性”。  
  
    随即显示“属性页”对话框。  
  
3. 在“属性页”对话框中，单击“高级”。  
  
4. 在“其他检测选项”文本框中，使用以下语法键入要检测的函数的名称：  
  
    **/include:** `FuncSpec` **[;** `FuncSpec` **]** `...`  
  
    `FuncSpec` 是命名空间和函数名。 其格式为 `Namespace`**::**`FunctionName`。 可使用分号分隔多个函数。 可使用星号 (\*) 指定一个或多个字符的通配符。 例如，/include:MyNS::\\* 指定 MyNS 命名空间中的所有函数。  
  
   > [!NOTE]
   > 若要列出某个二进制文件中的函数，请在分析工具安装目录（通常是 [!INCLUDE[vsprvsts](../includes/vsprvsts-md.md)]安装目录下的 \Team Tools\Performance Tools 目录）中打开命令提示符窗口，然后键入 **vsinstr /DumpFuncs**  
  
## <a name="see-also"></a>请参阅  
 [控制数据收集](../profiling/controlling-data-collection.md)   
 [如何：为特定 Dll 的限制规范](../profiling/how-to-limit-instrumentation-to-specific-dlls.md)   
 [如何：指定其他检测选项](../profiling/how-to-specify-additional-instrumentation-options.md)
