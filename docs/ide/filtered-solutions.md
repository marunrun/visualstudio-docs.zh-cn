---
title: 加载项目的子集
ms.date: 04/22/2019
ms.prod: visual-studio-dev16
ms.topic: conceptual
helpviewer_keywords:
- filtered solution
- solution filtering
author: jillre
ms.author: stsu
manager: jillfra
monikerRange: '>= vs-2019'
ms.openlocfilehash: 4c44d267ef5686d04e9549601e05866aabbfb62d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "72650842"
---
# <a name="filtered-solutions-in-visual-studio"></a>Visual Studio 中筛选的解决方案

大型开发团队通常使用包含许多项目的单个大型解决方案进行协作。 但是，个别开发人员通常只处理这些项目的一小部分。 为了在打开大型解决方案时提高性能，Visual Studio 2019 中引入了解决方案筛选  。 通过解决方案筛选，可打开仅加载选择性项目的解决方案。 在解决方案中加载项目子集可以减少解决方案加载、构建和测试运行时间，并实现更有针对性的审查。

可以使用以下功能：

- 通过在不加载任何项目的情况下打开解决方案，可以更快获得代码。 解决方案打开后，可以有选择地选择要加载的项目。

- 重新打开解决方案时，Visual Studio 会记住在上一个会话中加载的项目，并仅加载这些项目。

- 可以创建解决方案筛选器文件以保存一个或多个项目加载配置或与队友共享配置。

## <a name="open-a-filtered-solution"></a>打开已筛选的解决方案

直接从“打开项目”  对话框或通过[命令行](#command-line)打开解决方案时，可以不加载任何项目。

### <a name="open-project-dialog"></a>“打开项目”对话框

若要使用“打开项目”  对话框打开一个解决方案而不加载它的任何项目，请执行以下操作：

1. 在菜单栏上，依次选择“文件” **“打开”** “项目/解决方案” >    >   。

2. 在“打开项目”对话框中，  选择解决方案，然后选择“不加载项目”  。

   ![Visual Studio 的“打开项目”对话框，其中已选中“不加载项目”](media/filtered-solutions/do-not-load-projects.png)

3. 选择“打开”。 

   解决方案打开，其中已卸载其所有项目。

4. 在“解决方案资源管理器”中，选择要加载的项目（按住 Ctrl 同时单击以选择多个项目），然后右键单击项目并选择“重新加载项目”    。

   ![在 Visual Studio 解决方案资源管理器重新加载多个项目](media/filtered-solutions/reload-project.png)

   Visual Studio 将记住下次在本地打开解决方案时要加载的项目。

### <a name="command-line"></a>命令行

（Visual Studio 2019 版本 16.1 中的新增功能。）

如果要从命令行打开某个解决方案但不加载任何项目，可以使用如下示例所示的 [`/donotloadprojects`](../ide/reference/donotloadprojects-devenv-exe.md) 开关：

```cmd
devenv /donotloadprojects MySln.sln
```

## <a name="toggle-unloaded-project-visibility"></a>切换已卸载的项目可见性

可以选择在“解决方案资源管理器”中使用以下选项之一查看解决方案中的所有项目或仅查看已加载的项目： 

- 右键单击解决方案，然后选择“显示已卸载的项目”或“隐藏已卸载的项目”   。

- 选择解决方案节点来启用“显示所有文件”  按钮；然后单击按钮切换已卸载项目的可见性。

   ![Visual Studio“解决方案资源管理器”中的“显示所有文件”按钮](media/filtered-solutions/show-all-files.PNG)

## <a name="load-project-dependencies"></a>加载项目依赖项

在只加载选定项目的解决方案中，可能并未加载项目的全部项目依赖项。 使用“加载项目依赖项”  菜单选项，确保同时加载项目所依赖的任何项目。 右键单击“解决方案资源管理器”  中一个或多个已加载的项目，然后选择“加载项目依赖项”  。

![在 Visual Studio 2019 中加载项目依赖项](media/filtered-solutions/load-project-dependencies.png)

## <a name="solution-filter-files"></a>解决方案筛选器文件

如果要共享项目加载配置或将其提交给源代码管理，则可以创建解决方案筛选器文件（扩展名为 .slnf）  。 打开解决方案筛选器文件时，解决方案将在 Visual Studio 中打开，其中已加载指定的项目并已隐藏所有卸载的项目。 可以[切换](#toggle-unloaded-project-visibility)以查看已卸载的项目。

从外观来看，解决方案筛选器文件与常规解决方案文件不同，前者在“解决方案资源管理器”的解决方案旁附加了一个漏斗字形图标  。 筛选器的名称和已加载项目的数量也显示在解决方案名称旁边。

![在 Visual Studio 解决方案资源管理器中打开的解决方案筛选器文件](media/filtered-solutions/solution-filter.PNG)

> [!NOTE]
> 如果在创建解决方案筛选器文件后将新项目添加到原始解决方案，则它们在“解决方案资源管理器”中显示为已卸载的项目  。

### <a name="create-a-solution-filter-file"></a>创建解决方案筛选器文件

1. 在“解决方案资源管理器”中，右键单击“解决方案”，然后选择“另存为解决方案资源管理器筛选器”   。

   ![Visual Studio 解决方案资源管理器中的“另存为解决方案资源管理器筛选器”菜单](media/filtered-solutions/save-as-solution-filter.png)

2. 选择解决方案筛选器文件的名称和位置。

创建解决方案筛选器文件后，它会添加到你的“最近项目和解决方案”列表中，以便访问： 

![在 Visual Studio 中打开最近文件](media/filtered-solutions/open-recent.png)

## <a name="see-also"></a>另请参阅

- [在解决方案资源管理器中自定义文件嵌套](file-nesting-solution-explorer.md)
- [优化 Visual Studio 性能](optimize-visual-studio-performance.md)
