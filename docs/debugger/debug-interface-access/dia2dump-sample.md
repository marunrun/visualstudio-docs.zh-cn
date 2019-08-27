---
title: Dia2dump 示例 |Microsoft Docs
ms.date: 07/24/2018
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c8b92ae2f607ae449b7b4392fc3638fcdcb6a80
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715341"
---
# <a name="dia2dump-sample"></a>Dia2dump 示例

Dia2dump 示例演示如何使用 Microsoft 调试接口访问软件开发工具包 (DIA SDK) 来查询信息的 PDB 文件。

Dia2dump 示例随 Visual Studio 安装，并包含文件的解决方案和源文件。 从命令行运行已编译可执行文件。 它可以显示整个程序数据库 (.pdb) 文件的内容或只是部分你感兴趣。

## <a name="install-the-sample"></a>安装示例

该示例安装时选择**使用的桌面开发C++**  Visual Studio 安装程序中的工作负荷。 有关如何安装 Visual Studio 并选择特定的工作负荷和各个组件的信息，请参阅[安装 Visual Studio](../../install/install-visual-studio.md)。

安装时，该示例是在 Visual Studio 安装目录中名为 \DIA SDK\Samples\DIA2Dump 子目录中。

## <a name="build-the-sample"></a>生成示例

默认情况下，安装目录为受保护的目录。 这意味着您必须使用提升的开发人员命令提示符或 Visual Studio 的实例可以生成和编辑此位置中的示例解决方案。 为了简化生成，我们建议首先将文件从示例目录复制到另一个目录，如在文档文件夹的文件夹，然后生成该示例。

### <a name="to-build-the-dia2dump-sample-in-visual-studio"></a>若要生成 Visual Studio 中的 Dia2Dump 示例

1. 在 Visual Studio 中打开 DIA2Dump.sln 文件。 如果您未将该解决方案复制到另一个目录，可能提示您重新启动 Visual Studio，使用提升的权限。

1. 在中**解决方案资源管理器**，选择 Dia2Dump 项目 （而不是解决方案）。

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[使用项目属性](/cpp/build/working-with-project-properties)。

1. 打开**配置属性** > **C /C++**  > **常规**属性页。

1. 在中**附加包含目录**属性中，选择下拉列表控件，然后选择**编辑**。

1. 在中**附加包含目录**对话框中的，编辑字段中输入`$(VSInstallDir)DIA SDK\include`目录。 将此目录以保证编译器可以找到 dia2.h 文件添加。 选择“确定”以保存更改  。

1. 选择**确定**若要将所做的更改保存到项目属性。

1. 上**构建**菜单中，选择**重新生成解决方案**。 默认情况下，Visual Studio 生成此示例中，位于调试解决方案目录的子目录中的调试版本。

1. 关闭 Visual Studio。

### <a name="to-build-the-dia2dump-sample-at-the-command-line"></a>若要生成在命令行 Dia2Dump 示例

1. 在开发人员命令提示符窗口中，更改为复制示例文件的目录。 如果未将示例复制到另一个目录，则必须使用提升 （以管理员身份运行） 开发人员命令提示窗口。

1. 输入命令`nmake makefile`以生成 dia2dump.exe 的默认调试配置。

## <a name="run-the-dia2dump-sample"></a>运行 Dia2Dump 示例

Dia2Dump.exe 依赖 msdia*版本*.dll COM 服务器提供其服务。 从 Visual Studio 2015 开始，版本为 msdia140.dll。 如果 msdia*版本*.dll COM 服务器未初始化，可以开始工作 dia2dump.exe 前必须将其注册。 DIA SDK 目录中包含的 bin 子目录包含 x86 版本的 DLL。 版本针对 x64 体系结构机处于 bin\amd64，并且 ARM 版本为 bin\arm 中。 若要注册该 dll，打开提升的开发人员命令提示符窗口，并将更改为包含您的计算机体系结构的版本的目录。 输入命令`regsvr32 msdia140.dll`注册 COM 服务器。

### <a name="to-run-the-sample"></a>运行示例

1. 打开命令提示符，并将更改为包含生成 dia2dump.exe 的目录。

1. 输入命令`dia2dump filename`其中*文件名*是要检查的 PDB 文件的名称。 如果 PDB 文件是另一个目录中，使用完整路径将文件作为*文件名*。 此命令将列出在 PDB 文件中的所有数据。

1. Dia2Dump 具有其他选项以只显示所选的信息。 使用`dia2dump -?`命令以列出所有可用的选项。

## <a name="see-also"></a>请参阅

- [移植、迁移和升级 Visual Studio 项目](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)
