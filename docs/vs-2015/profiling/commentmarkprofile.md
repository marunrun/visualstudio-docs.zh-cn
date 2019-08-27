---
title: CommentMarkProfile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- CommentMarkProfile
- CommentMarkProfileA
ms.assetid: 33ccff45-c33a-4672-b41f-5b317b848cd1
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 28535db3e129029d6767ac969d121ee4cbb1aec5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63416548"
---
# <a name="commentmarkprofile"></a>CommentMarkProfile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`CommentMarkProfile` 函数在 .vsp 文件中插入数值标记和文本字符串。 为了插入标记和注释，对包含 `CommentMarkProfile` 函数的线程进行的分析必须为 ON。  
  
## <a name="syntax"></a>语法  
  
```  
PROFILE_COMMAND_STATUS PROFILERAPI CommentMarkProfile(  
                                   long lMarker,   
                                   LPCTSTR szComment);  
```  
  
#### <a name="parameters"></a>参数  
 `lMarker`  
  
 要插入的数值标记。 标记必须大于或等于 0（零）。  
  
 `szComment`  
  
 指向要插入的文本字符串的指针。 该字符串的长度必须小于 256 个字符（包括 NULL 终止符）。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 函数通过使用 **PROFILE_COMMAND_STATUS** 枚举来指示成功或失败。 返回值可以是下列值之一：  
  
|枚举器|说明|  
|----------------|-----------------|  
|MARK_ERROR_MARKER_RESERVED|参数小于或等于零。 这些值将保留。 不会记录标记和注释。|  
|MARK_ERROR_MODE_NEVER|调用函数时，分析模式设置为“从不”。 不会记录标记和注释。|  
|MARK_ERROR_MODE_OFF|调用函数时，分析模式设置为“关闭”。 不会记录标记和注释。|  
|MARK_ERROR_NO_SUPPORT|此上下文中无标记支持。 不会记录标记和注释。|  
|MARK_ERROR_OUTOFMEMORY|内存不可用来记录事件。 不会记录标记和注释。|  
|MARK_TEXTTOOLONG|该字符串超过 256 个字符的最大限制。 注释字符串将截断，且会记录标记和注释。|  
|MARK_OK|返回 MARK_OK 以指示成功。|  
  
## <a name="remarks"></a>备注  
 当使用 VSInstr Mark 命令或函数（CommentMarkAtProfile、CommentMarkProfile 或 MarkProfile）插入标记和注释时，包含标记配置文件函数的线程的分析状态必须为“开”。  
  
 配置文件标记具有全局范围。 例如，在一个线程中插入的配置文件标记可用于标记 .vsp 文件中任何线程的数据段的开头或结尾。  
  
> [!IMPORTANT]
> CommentMarkProfile 方法只能用于检测。  
  
## <a name="net-framework-equivalent"></a>.NET Framework 等效项  
 Microsoft.VisualStudio.Profiler.dll  
  
## <a name="function-information"></a>函数信息  
  
|||  
|-|-|  
|**Header**|包括 VSPerf.h|  
|**Library**|使用 VSPerf.lib|  
|**Unicode**|作为 `CommentMarkProfileW` (Unicode) 和 `CommentMarkProfileA` (ANSI) 实现。|  
  
## <a name="example"></a>示例  
 下面的代码阐释了 CommentMarkProfile 函数调用。 该示例假设使用 Win32 字符串宏和 Unicode 编译器设置，确定代码是否调用了 [!INCLUDE[vcpransi](../includes/vcpransi-md.md)] 函数调用。  
  
```  
void ExerciseCommentMarkProfile()  
{  
    // Declare and initalize variables to pass to   
    // CommentMarkProfile.  The values of these   
    // parameters are assigned based on the needs   
    // of the code; and for the sake of simplicity  
    // in this example, the variables are assigned  
    // arbitrary values.  
    long markId = 01;  
    TCHAR * markText = TEXT("Exercising CommentMarkProfile...");  
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare MarkOperationResult Enumerator.    
    // Holds return value from call to CommentMarkProfile.  
    PROFILE_COMMAND_STATUS markResult;  
  
    markResult = CommentMarkProfile(  
        markId,  
        markText);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("CommentMarkProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, markResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 探查器 API 参考（本机）](../profiling/visual-studio-profiler-api-reference-native.md)
