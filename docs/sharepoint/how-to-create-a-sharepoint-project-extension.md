---
title: 如何：创建 SharePoint 项目扩展 |Microsoft Docs
ms.date: 04/28/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 37f22e085334bf6a18ef1b5482b6b6c206690148
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966869"
---
# <a name="how-to-create-a-sharepoint-project-extension"></a>如何：创建 SharePoint 项目扩展
  当你想要将功能添加到已在 Visual Studio 中打开任何 SharePoint 项目时，请创建一个项目扩展。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

### <a name="to-create-a-project-extension"></a>若要创建项目扩展

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口的类。

4. 添加<xref:System.ComponentModel.Composition.ExportAttribute>到类。 此特性使 Visual Studio 能够发现和加载您<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>实现。 传递<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>特性构造函数的类型。

5. 中的实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A>方法，使用成员*projectService*参数来定义您的扩展插件的行为。 此参数是<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService>提供对中定义的事件的访问的对象<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents>接口。

## <a name="example"></a>示例
 下面的代码示例演示如何创建简单项目扩展的处理大部分由定义的 SharePoint 项目事件<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents>接口。 若要测试此代码，创建 SharePoint 项目中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，然后向解决方案添加更多项目，更改项目属性值，或删除或排除一个项目。 该扩展，通知您有关事件写入到的消息**输出**窗口和**错误列表**窗口。

  ```vb
    Imports Microsoft.VisualStudio.SharePoint
    Imports System.ComponentModel
    Imports System.ComponentModel.Composition

    Namespace Contoso.ExampleProjectExtension
      <Export(GetType(ISharePointProjectExtension))> _
      Class ExampleProjectExtension
        Implements ISharePointProjectExtension

        Private WithEvents projectService As ISharePointProjectService

        Public Sub Initialize(ByVal projectService As ISharePointProjectService) _
            Implements ISharePointProjectExtension.Initialize
            Me.projectService = projectService
        End Sub

        ' A project was added.
        Private Sub projectService_ProjectAdded(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectAdded
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project was added: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project was loaded in the IDE.
        Private Sub projectService_ProjectInitialized(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectInitialized
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project is being initialized: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' The name of a property was changed.
        Private Sub projectService_ProjectNameChanged(ByVal sender As Object, ByVal e As NameChangedEventArgs) _
            Handles projectService.ProjectNameChanged
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The project named {0} was changed to {1}.", e.OldName, project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project property value was changed.
        Private Sub ProjectPropertyChanged(ByVal sender As Object, ByVal e As PropertyChangedEventArgs) _
            Handles projectService.ProjectPropertyChanged
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following property of the {0} project was changed: {1}",
                project.Name, e.PropertyName)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project is being removed or unloaded.
        Private Sub projectService_ProjectRemoved(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectRemoved
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project is being removed or unloaded: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project was removed or unloaded.
        Private Sub projectService_ProjectDisposing(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectDisposing
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project was removed or unloaded: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub
      End Class
    End Namespace
    ```

    ```csharp
    using Microsoft.VisualStudio.SharePoint;
    using System;
    using System.ComponentModel;
    using System.ComponentModel.Composition;

    namespace Contoso.ExampleProjectExtension
    {
      [Export(typeof(ISharePointProjectExtension))]
      internal class ExampleProjectExtension : ISharePointProjectExtension
      {
        public void Initialize(ISharePointProjectService projectService)
        {
            projectService.ProjectAdded += projectService_ProjectAdded;
            projectService.ProjectInitialized += projectService_ProjectInitialized;
            projectService.ProjectNameChanged += projectService_ProjectNameChanged;
            projectService.ProjectPropertyChanged += projectService_ProjectPropertyChanged;
            projectService.ProjectRemoved += projectService_ProjectRemoved;
            projectService.ProjectDisposing += projectService_ProjectDisposing;
        }

        // A project was added.
        void projectService_ProjectAdded(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project was added: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project is loaded in the IDE.
        void projectService_ProjectInitialized(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project is being initialized: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // The name of a project was changed.
        void projectService_ProjectNameChanged(object sender, NameChangedEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The project named {0} was changed to {1}.", e.OldName, project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project property value was changed.
        private void projectService_ProjectPropertyChanged(object sender, PropertyChangedEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following property of the {0} project was changed: {1}",
                project.Name, e.PropertyName);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project is being removed or unloaded.
        void projectService_ProjectRemoved(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project is being removed or unloaded: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project was removed or unloaded.
        void projectService_ProjectDisposing(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project was removed or unloaded: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }
     }
  }
  ```

此示例使用 SharePoint 项目服务将写入到消息**输出**窗口和**错误列表**窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 有关示例，演示如何处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested>并<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested>事件，请参阅[如何：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)和[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[在 Visual Studio 工具部署 SharePoint 扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [如何：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
