---
title: 指定自定义生成事件
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- build events, customizing
ms.assetid: 69e935a5-e208-4bcd-865c-3e5f9b047ca8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fda60ffb97ecb44bd4a881cb42e4d9199cc958b8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "76115344"
---
# <a name="specify-custom-build-events-in-visual-studio"></a>在 Visual Studio 中指定自定义生成事件

通过指定自定义生成事件，可以在生成开始之前或在它完成之后自动运行命令。 例如，可以在生成开始之前运行 .bat 文件，或是在生成完成之后将新文件复制到文件夹中  。 仅当生成在生成过程中成功到达这些点时，生成事件才会运行。

有关所使用的编程语言的特定信息，请参阅以下主题：

- Visual Basic--[如何：指定生成事件 (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md)。

- C# 和 F#--[如何：指定生成事件 (C#)](../ide/how-to-specify-build-events-csharp.md)。

- Visual C++--[指定生成事件](/cpp/build/specifying-build-events)。

## <a name="syntax"></a>语法

生成事件遵循与 DOS 命令相同的语法，但可以使用宏更轻松地创建生成事件。 有关可用宏的列表，请参阅[预生成事件/生成后事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)。

为获得最佳结果，请遵循以下这些格式设置提示：

- 在运行 .bat 文件的所有生成事件之前，先添加 `call` 语句  。

   示例：`call C:\MyFile.bat`

   示例：`call C:\MyFile.bat call C:\MyFile2.bat`

- 将文件路径用引号引起来。

   示例（对于 [!INCLUDE[win8](../debugger/includes/win8_md.md)]）："%ProgramFiles(x86)%\Microsoft SDKs\Windows\v8.0A\Bin\NETFX 4.0 Tools\gacutil.exe" -if "$(TargetPath)"

- 使用换行符分隔多个命令。

- 根据需要包含通配符。

   示例：`for %I in (*.txt *.doc *.html) do copy %I c:\`*mydirectory*`\`

  > [!NOTE]
  > 以上代码中的 `%I` 在批处理脚本中应是 `%%I`。

## <a name="see-also"></a>另请参阅

- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
- [预生成事件/生成后事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [MSBuild 特殊字符](../msbuild/msbuild-special-characters.md)
- [演练：生成应用程序](../ide/walkthrough-building-an-application.md)
