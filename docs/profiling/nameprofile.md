---
title: NameProfile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NameProfile
- NameProfileA
ms.assetid: 1bb05441-c4ff-4323-9fef-f3924fba4430
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e0d4cdfd393961566a0aef0c649e6ff788fdc8ac
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63403625"
---
# <a name="nameprofile"></a>NameProfile
`NameProfile` 函数会将字符串分配给指定的进程或线程。

 NameProfile API 仅可用于检测分析。 NameProfile API 不支持用于采样分析。

## <a name="syntax"></a>语法

```cpp
PROFILE_COMMAND_STATUS PROFILERAPI NameProfile(
                                   LPCTSTR pszName,
                                   PROFILE_CONTROL_LEVEL Level,
                                   unsigned int dwId);
```

#### <a name="parameters"></a>参数
 `pszName`

 分析元素的名称。 以下情况下，名称无效（导致 NameProfileA 返回 NAME_ERROR_INVALID_NAME）：

- 传递到 NameProfileA 的指针为 NULL 值

- pszName 的字符串数据以数字开头

- pszName 的字符串数据包含空格

- pszName 的字符串数据包含以下任意字符：,;.`~!@#$%^&*()=[]{}&#124;\\?/<>

  `Level`

  指示性能数据集合可应用到的分析级别。 以下 PROFILE_CONTROL_LEVEL 值可用于指示性能数据集合可应用到的三个级别之一：

|枚举器|说明|
|----------------|-----------------|
|PROFILE_GLOBALLEVEL|全局级别设置影响分析运行中的所有进程和线程。|
|PROFILE_PROCESSLEVEL|进程级别设置影响指定进程包含的所有线程。|
|PROFILE_THREADLEVEL|线程分析级别设置影响指定的线程。|

 `dwId`

 分析级别标识符。 使用由系统生成的进程或线程标识符。

## <a name="property-valuereturn-value"></a>属性值/返回值
 函数通过使用 **PROFILE_COMMAND_STATUS** 枚举来指示成功或失败。 返回值可以是下列值之一：

|枚举器|说明|
|----------------|-----------------|
|NAME_ERROR_ID_NOEXIST|指定的分析元素不存在。|
|NAME_ERROR_INVALID_NAME|名称无效。|
|NAME_ERROR_LEVEL_NOEXIST|指定的配置文件级别不存在。|
|NAME_ERROR_NO_SUPPORT|不支持指定的操作。|
|NAME_ERROR_OUTOFMEMORY|内存不可用来记录事件。|
|NAME_ERROR_REDEFINITION|名称已分配给配置文件元素。 忽略此函数中的名称。|
|NAME_ERROR_TEXTTRUNCATED|名称文本超过 32 个字符（包括空字符），因此已截断。|
|NAME_OK|成功注册了名称。|

## <a name="remarks"></a>备注
 只有一个名称可以分配给每个进程或线程。 命名分析元素后，忽略对该元素的 NameProfile 的后续调用。

 如果为不同的线程或进程提供了相同的名称，则报表会包含该级别下具有该名称的所有元素的数据。

 如果指定当前进程或线程以外的进程或线程，则必须先确保它已初始化并开始运行，然后才能对其命名。 否则，NameProfile 方法会失败。

> [!IMPORTANT]
> CreateProcess() 和 CreateThread() API 函数可以在初始化线程或进程前返回。

## <a name="net-framework-equivalent"></a>.NET Framework 等效项
 Microsoft.VisualStudio.Profiler.dll

## <a name="function-information"></a>函数信息

|||
|-|-|
|**Header**|包括 VSPerf.h|
|**Library**|使用 VSPerf.lib|
|**Unicode**|作为 `NameProfileW` (Unicode) 和 `NameProfileA` (ANSI) 实现。|

## <a name="example"></a>示例
 下面的代码阐释了 NameProfile 函数调用。 该示例假设使用 Win32 字符串宏和 ANSI 编译器设置，确定代码是否调用启用了 ANSI 的函数。

```cpp
void ExerciseNameProfile()
{
    // Variables used to print output.
    HRESULT hResult;
    TCHAR tchBuffer[256];

    // Create and initialize variables to pass to
    // ExerciseNameProfile.  The value of this
    // parameter is based on the needs of the code;
    // and for the sake of simplicity in this example,
    // the variable is assigned an arbitrary value.
    TCHAR * profileName = TEXT("ExerciseNameProfile");

    // Declare enumeration to hold result of call to
    // ExerciseNameProfle.
    PROFILE_COMMAND_STATUS nameResult;

    nameResult =  NameProfile(
        profileName,
        PROFILE_GLOBALLEVEL,
        PROFILE_CURRENTID);

    // Format and print result.
    LPCTSTR pszFormat = TEXT("%s %d.\0");
    TCHAR* pszTxt = TEXT("NameProfile returned");
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,
        pszTxt, nameResult);

#ifdef DEBUG
    OutputDebugString(tchBuffer);
#endif
}
```

## <a name="see-also"></a>请参阅
- [Visual Studio 探查器 API 参考（本机）](../profiling/visual-studio-profiler-api-reference-native.md)