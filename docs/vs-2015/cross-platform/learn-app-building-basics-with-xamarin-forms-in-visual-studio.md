---
title: 通过 Xamarin 了解应用程序构建基础知识
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: d22b5186-9e03-4e85-afc9-7cbe28522a6d
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: bc7e46af7e29ef554b80bd9244910e0c67d373af
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299756"
---
# <a name="learn-app-building-basics-with-xamarinforms-in-visual-studio"></a>学习在 Visual Studio 中使用 Xamarin.Forms 生成应用的基础知识
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

完成 [Setup and install](../cross-platform/setup-and-install.md) 和 [Verify your Xamarin environment](../cross-platform/verify-your-xamarin-environment.md)中的步骤后，此演练会立即演示如何借助 Xamarin.Forms 生成基本应用（如下所示）。 借助 Xamarin.Forms，将在可移植类库 (PCL) 中将全部 UI 代码编写一次。 Xamarin 随后会自动呈现 iOS、Android 和 Windows 平台的本机 UI 控件。 我们建议使用这一方法，因为 PCL 选项可以最好地支持仅使用受所有目标平台支持的 .NET API，并且因为 Xamarin.Forms 能够让你跨平台共享 UI 代码。

 ![Android、iOS 和 Windows Phone 上的天气应用示例](../cross-platform/media/crossplat-xamarin-formsguide-1.png "CrossPlat Xamarin FormsGuide 1")

 你将执行以下操作来生成它：

- [设置你的解决方案](#solution)

- [编写共享的数据服务代码](#dataservice)

- [开始编写共享的 UI 代码](#uicode)

- [使用适用于 Android 的 Visual Studio 仿真程序测试你的应用。](#test)

- [跨平台完成具有本机外观的 UI](#finish)

> [!TIP]
> 可以在 [xamarin-forms-samples repository on GitHub](https://github.com/xamarin/xamarin-forms-samples/tree/master/Weather)（GitHub 上的 xamarin-forms-samples 存储库）中找到此项目完整的源代码。

## <a name="solution"></a> 设置你的解决方案
 这些步骤创建 Xamarin.Forms 解决方案，该方案包含共享代码的 PCL 和两个添加的 NuGet 包。

1. 在 Visual Studio 中，创建新的“空白应用（Xamarin.Forms 可移植）” 解决方案，并将其命名为 **WeatherApp**。 通过在搜索字段中输入 **Xamarin.Forms** 可以非常方便地找到此模板。

     如果不存在，则可能需要安装 Xamarin 或启用 Visual Studio 2015 功能，请参阅[设置和安装](../cross-platform/setup-and-install.md)。

     ![创建新的空白应用&#40;Xamarin。窗体&#41;可移植项目](../cross-platform/media/crossplat-xamarin-formsguide-2.png "CrossPlat Xamarin FormsGuide 2")

2. 单击“确定”以创建解决方案后，将会得到多个单独项目：

    - **Weatherapp（可移植）** ：PCL，你将在其中编写跨平台共享的代码，包括与 Xamarin.Forms 结合使用的常见业务逻辑和 UI 代码。

    - **WeatherApp.Droid**：包含本机 Android 代码的项目。 这将设置为默认启动项目。

    - **WeatherApp.iOS**：包含本机 iOS 代码的项目。

    - **WeatherApp.UWP**：包含 Windows 10 UWP 代码的项目。

    - **WeatherApp.Windows (Windows 8.1)** ：包含本机 Windows 8.1 代码的项目。

    - **WeatherApp.WinPhone (Windows Phone 8.1)** ：包含本机 Windows Phone 代码的项目。

    > [!NOTE]
    > 可随意删除你不准备面向的目标平台的任何项目。 出于本演练的目的，我们将参考 Android、iOS 和 Windows Phone 8.1 项目 处理 UWP 和 Windows 8.1 项目与处理 Windows Phone 8.1 项目非常相似。

     在每个本机项目中，你有权访问相应平台的本机设计器，并且可以根据需要实现特定于平台的屏幕和功能。

3. 将解决方案中的 Xamarin.Forms NuGet 包升级到最新稳定版本，如下所示。 我们建议每次创建新 Xamarin 解决方案时执行此操作：

    - 选择“工具”>“NuGet 包管理器”>“管理解决方案的 NuGet 包”。

    - 在“更新” 选项卡下，选中 **Xamarin.Forms** 更新并选中以解决方案中的所有项目。 （注意：不要选中 Xamarin.Android.Support 的任何更新。）

    - 将“版本” 字段更新为可用的“最新稳定” 版本。

    - 单击“更新”。

         ![更新 Xamarin NuGet 包](../cross-platform/media/crossplat-xamarin-formsguide-4.png "CrossPlat Xamarin FormsGuide 4")

4. 将 **Newtonsoft.Json** 和 NuGet 包添加到 PCL 项目中，其将用于处理从天气数据服务中检索的信息：

    - 在 NuGet 包管理器中（从步骤 3 开始仍处于打开状态），选择“浏览” 选项卡，然后搜索 **Newtonsoft**。

    - 选择 **Newtonsoft.Json**。

    - 检查 **weatherapp** 项目（这是唯一需要安装包的项目）。

    - 确保“版本” 字段设置为“最新稳定” 版本。

    - 单击“安装”。

    - ![查找并安装 Newtonsoft.json NuGet 包](../cross-platform/media/crossplat-xamarin-formsguide-5.png "CrossPlat Xamarin FormsGuide 5")

5. 重复步骤 4 以查找并安装 **Microsoft.Net.Http** 包。

6. 生成解决方案并验证没有生成错误。

## <a name="dataservice"></a>编写共享的数据服务代码
 **WeatherApp（可移植）** 项目是将在其中编写可移植类库 (PCL) 的代码的项目，该代码在所有平台之间共享。 PCL 自动包含在 iOS、Android 和 Windows Phone 项目生成的应用包中。

 要运行此示例，必须先在 [http://openweathermap.org/appid](https://openweathermap.org/appid) 注册免费 API 密钥。

 然后，以下步骤会将代码添加到 PCL，以访问和存储天气服务的数据：

1. 右键单击“WeatherApp”项目，然后选择“添加”>“类…”。 在“添加新项” 对话框中，将文件命名为 **Weather.cs**。 将使用此类来存储天气数据服务的数据。

2. 将 **Weather.cs** 的全部内容替换为以下内容：

    ```csharp
    namespace WeatherApp
    {
        public class Weather
        {
            public string Title { get; set; }
            public string Temperature { get; set; }
            public string Wind { get; set; }
            public string Humidity { get; set; }
            public string Visibility { get; set; }
            public string Sunrise { get; set; }
            public string Sunset { get; set; }

            public Weather()
            {
                //Because labels bind to these values, set them to an empty string to
                //ensure that the label appears on all platforms by default.
                this.Title = " ";
                this.Temperature = " ";
                this.Wind = " ";
                this.Humidity = " ";
                this.Visibility = " ";
                this.Sunrise = " ";
                this.Sunset = " ";
            }
        }
    }
    ```

3. 将另一个类添加到名为 **DataService.cs** 的 PCL 项目中，该类用于在该项目中处理天气数据服务的 JSON 数据。

4. 将 **DataService.cs** 的全部内容替换为以下代码：

    ```csharp
    using System.Threading.Tasks;
    using Newtonsoft.Json;
    using System.Net.Http;

    namespace WeatherApp
    {
        public class DataService
        {
            public static async Task<dynamic> getDataFromService(string queryString)
            {
                HttpClient client = new HttpClient();
                var response = await client.GetAsync(queryString);

                dynamic data = null;
                if (response != null)
                {
                    string json = response.Content.ReadAsStringAsync().Result;
                    data = JsonConvert.DeserializeObject(json);
                }

                return data;
            }
        }
    }
    ```

5. 将第三个类添加到名为 **核心** 的 PCL，你将在此 PCL 中放置共享业务逻辑，例如通过使用邮编形成查询字符串、调用天气数据服务以及填充 **天气** 类的实例的逻辑。

6. 将 **Core.cs** 的内容替换为以下内容：

    ```csharp
    using System;
    using System.Threading.Tasks;

    namespace WeatherApp
    {
        public class Core
        {
            public static async Task<Weather> GetWeather(string zipCode)
            {
                //Sign up for a free API key at http://openweathermap.org/appid
                string key = "YOUR KEY HERE";
                string queryString = "http://api.openweathermap.org/data/2.5/weather?zip="
                    + zipCode + ",us&appid=" + key + "&units=imperial";

                dynamic results = await DataService.getDataFromService(queryString).ConfigureAwait(false);

                if (results["weather"] != null)
                {
                    Weather weather = new Weather();
                    weather.Title = (string)results["name"];
                    weather.Temperature = (string)results["main"]["temp"] + " F";
                    weather.Wind = (string)results["wind"]["speed"] + " mph";
                    weather.Humidity = (string)results["main"]["humidity"] + " %";
                    weather.Visibility = (string)results["weather"][0]["main"];

                    DateTime time = new System.DateTime(1970, 1, 1, 0, 0, 0, 0);
                    DateTime sunrise = time.AddSeconds((double)results["sys"]["sunrise"]);
                    DateTime sunset = time.AddSeconds((double)results["sys"]["sunset"]);
                    weather.Sunrise = sunrise.ToString() + " UTC";
                    weather.Sunset = sunset.ToString() + " UTC";
                    return weather;
                }
                else
                {
                    return null;
                }
            }
        }
    }
    ```

7. 生成 **weatherapp** PCL 项目，以确保代码正确无误。

## <a name="uicode"></a> 开始编写共享的 UI 代码
 Xamarin.Forms 使你可以在 PCL 中实现共享的 UI 代码。 在这些步骤中，将向 PCL 添加一个带有按钮的屏幕，该按钮使用由前一部分中添加的天气数据服务代码返回的数据更新其文本：

1. 右键单击 " **WeatherApp** " 项目，然后选择 "**添加 > 新项 ...** "，添加名为 " **WeatherPage.cs** " 的**窗体 Xaml 页面**。在 "**添加新项**" 对话框中，搜索 "窗体"，选择**窗体 Xaml 页**，并将其命名为**WeatherPage.cs**。

     Xamarin.Forms 基于 XAML，因此，此步骤创建 **WeatherPage.xaml** 文件和嵌套的代码隐藏文件 **WeatherPage.xaml.cs**。 这使你可以通过 XAML 或代码生成 UI。 在此演练中，你将同时执行两者中的各一部分。

     ![添加新的 Xamarin. Forms XAML 页](../cross-platform/media/crossplat-xamarin-formsguide-6.png "CrossPlat Xamarin FormsGuide 6")

2. 要向 WeatherPage 屏幕中添加一个按钮，请将 WeatherPage.xaml 的内容替换为以下内容：

    ```xaml
    <?xml version="1.0" encoding="utf-8" ?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
           xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
           x:Class="WeatherApp.WeatherPage">
      <Button x:Name="getWeatherBtn" Text="Get Weather"/>
    </ContentPage>
    ```

     请注意，必须使用 **X:name** 特性定义按钮名称，以便可以从代码隐藏文件内部通过名称引用此按钮。

3. 若要为按钮的 **已单击** 事件添加事件处理程序以更新按钮文本，请用以下代码替换 **WeatherPage.xaml.cs** 的内容。 （可自由将“60601”更改为其他邮政编码。）

    ```csharp
    using System;
    using Xamarin.Forms;

    namespace WeatherApp
    {
        public partial class WeatherPage: ContentPage
        {
            public WeatherPage()
            {
                InitializeComponent();
                this.Title = "Sample Weather App";
                getWeatherBtn.Clicked += GetWeatherBtn_Clicked;

                //Set the default binding to a default object for now
                this.BindingContext = new Weather();
            }

            private async void GetWeatherBtn_Clicked(object sender, EventArgs e)
            {
                Weather weather = await Core.GetWeather("60601");
                getWeatherBtn.Text = weather.Title;
            }
        }
    }
    ```

4. 若要在应用启动时将 **WeatherPage** 作为第一个屏幕打开，请将 **App.cs** 中的默认构造函数替换为以下代码：

    ```csharp
    public App()
    {
        MainPage = new NavigationPage(new WeatherPage());
    }
    ```

5. 生成 WeatherApp PCL 项目，以确保代码正确无误。

## <a name="test"></a>使用适用于 Android 的 Microsoft Visual Studio 模拟器测试应用
 现在即可运行应用！ 让我们现在仅运行 Android 版本来验证该应用将从天气服务中获取数据。 稍后，待你添加更多 UI 元素后，还将可以运行 iOS 和 Windows Phone 版本。 （注意：如果要在 Windows 7 上运行 Visual Studio，你将遵循相同的步骤，但将改为使用 Xamarin 播放器。）

1. 通过右键单击“WeatherApp.Droid” 项目并选择“设为启动项目”，将其设置为启动项目。

2. 在 Visual Studio 工具栏上，你将看到 **WeatherApp.Droid** 列为目标项目。 选择一个 Android 仿真程序以进行调试，并点击“F5”。 我们建议使用其中一个“VS 仿真程序” 选项，它将运行适用于 Android 选项的 Visual Studio 仿真程序中的应用。

     ![选择 VS 仿真器调试目标](../cross-platform/media/crossplat-xamarin-formsguide-7.png "CrossPlat Xamarin FormsGuide 7")

3. 当应用在仿真程序中启动时，单击“获取天气信息” 按钮。 应可看到该按钮的文本更新为 **伊利诺伊州，芝加哥**，这是从天气服务检索的数据的 *Title* 属性。

     ![点击按钮前后的天气应用](../cross-platform/media/crossplat-xamarin-formsguide-8.png "CrossPlat Xamarin FormsGuide 8")

## <a name="finish"></a>跨平台完成具有本机外观的 UI
 Xamarin.Forms 会呈现每个平台的本机 UI 控件，以便你的应用会自动拥有本机外观。 若要更清晰地查看这一内容，我们可通过邮政编码的输入字段来完成 UI，然后显示从服务返回的天气数据。

1. 将 **WeatherPage.xaml** 的内容替换为以下代码。 请注意，使用之前介绍的 **X:name** 特性来命名每个元素，以便可以从代码中引用该元素。 Xamarin.Forms 还提供一系列 [布局选项](https://docs.microsoft.com/xamarin/xamarin-forms/user-interface/controls/layouts) (xamarin.com)；在此处，WeatherPage 使用 [StackLayout](https://docs.microsoft.com/dotnet/api/Xamarin.Forms.StackLayout?view=xamarin-forms) (xamarin.com)。

   ```xaml
   <?xml version="1.0" encoding="utf-8" ?>
   <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
          xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
          x:Class="WeatherApp.WeatherPage">

     <ContentPage.Resources>
       <ResourceDictionary>
         <Style x:Key="labelStyle" TargetType="Label">
           <Setter Property="TextColor" Value="#a8a8a8" />
           <Setter Property="FontSize" Value="Small" />
         </Style>
         <Style x:Key="fieldStyle" TargetType="Label">
           <Setter Property="TextColor">
             <OnPlatform x:TypeArguments="Color" iOS="Black" Android="White" WinPhone="White" />
           </Setter>
           <Setter Property="FontSize" Value="Medium" />
         </Style>
         <Style x:Key="fieldView" TargetType="ContentView">
           <Setter Property="Padding" Value="10,0,0,0" />
         </Style>
       </ResourceDictionary>
     </ContentPage.Resources>

     <ContentPage.Content>
       <ScrollView>
         <StackLayout>
           <StackLayout Orientation="Horizontal" HorizontalOptions="FillAndExpand"
                 BackgroundColor="#545454">
             <StackLayout Padding="10,10,10,10" HorizontalOptions="Start">
               <Label Text="Search by Zip Code" TextColor="White" FontAttributes="Bold"
                   FontSize="Medium" />
               <Label x:Name="zipCodeLabel" Text="Zip Code" Style="{StaticResource labelStyle}" />
               <Entry x:Name="zipCodeEntry" />
             </StackLayout>
             <StackLayout Padding="0,0,0,10" VerticalOptions="End">
               <Button x:Name="getWeatherBtn" Text="Get Weather" WidthRequest="185" BorderWidth="1" >
                 <!-- Set iOS colors; use defaults on other platforms -->
                 <Button.TextColor>
                   <OnPlatform x:TypeArguments="Color" iOS="White"/>
                 </Button.TextColor>
                 <Button.BorderColor>
                   <OnPlatform x:TypeArguments="Color" iOS="White"/>
                 </Button.BorderColor>
               </Button>
             </StackLayout>
           </StackLayout>
           <StackLayout Padding="10,10,10,10" HorizontalOptions="Start">
             <Label Text="Location" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label Text="{Binding Title}" Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Temperature" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="tempLabel" Text="{Binding Temperature}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Wind Speed" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="windLabel" Text="{Binding Wind}" Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Humidity" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="humidityLabel" Text="{Binding Humidity}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Visibility" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="visibilitylabel" Text="{Binding Visibility}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Time of Sunrise" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="sunriseLabel" Text="{Binding Sunrise}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Time of Sunset" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="sunsetLabel" Text="{Binding Sunset}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
           </StackLayout>
         </StackLayout>
       </ScrollView>
     </ContentPage.Content>
   </ContentPage>
   ```

    请注意，Xamarin.Forms 中 **OnPlatform** 标记的使用。 **OnPlatform** 选择特定于运行该应用的当前平台的属性值（请参阅 [外部 XAML 语法](https://docs.microsoft.com/xamarin/xamarin-forms/xaml/xaml-basics/essential-xaml-syntax) (xamarin.com)）。 在这里我们将使用它设置数据字段的不同文本颜色：Android 和 Windows Phone 上为白色，iOS 上则为黑色。 你可以将 **OnPlatform** 用于任何属性和任何数据类型，从而在 XAML 中的任意位置进行特定于平台的调整。 在代码隐藏文件中，你可以将 [Device.OnPlatform API](https://docs.microsoft.com/xamarin/xamarin-forms/platform/device) 用于同一目的。

2. 在 **WeatherPage.xaml.cs**中，将 **GetWeatherBtn_Clicked** 事件处理程序替换为以下代码。 此代码验证输入字段中存在邮政编码，为该邮政编码检索数据，将整个屏幕的绑定上下文设置为生成的天气实例，然后将按钮文本设置为"再次搜索”。 请注意，UI 中的每个标签将绑定到天气类的一个属性，因此将屏幕的绑定上下文设置为 **天气** 实例时，这些标签会自动更新。

   ```csharp
   private async void GetWeatherBtn_Clicked(object sender, EventArgs e)
   {
       if (!String.IsNullOrEmpty(zipCodeEntry.Text))
       {
           Weather weather = await Core.GetWeather(zipCodeEntry.Text);
           this.BindingContext = weather;
           getWeatherBtn.Text = "Search Again";
       }
   }
   ```

3. 通过右键单击相应的项目，选择“设置为启动项目”，并在设备上或仿真程序或模拟器中启动该应用，在所有三个平台上运行该应用 — Android、iOS 和 Windows Phone。 如下所示，输入有效的美国邮编（如 60601），然后按“获取天气信息”按钮以显示该地区的天气数据。 当然，在 iOS 项目的网络上，需要具有连接 Mac OS X 计算机的 Visual Studio。

    ![Android、iOS 和 Windows Phone 上的天气应用示例](../cross-platform/media/crossplat-xamarin-formsguide-1.png "CrossPlat Xamarin FormsGuide 1")

   此项目完整的源代码位于 [xamarin-forms-samples repository on GitHub](https://github.com/xamarin/xamarin-forms-samples/tree/master/Weather)（GitHub 上的 xamarin-forms-samples 存储库）中。
