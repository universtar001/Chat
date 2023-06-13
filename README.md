## Chat
sdufe Homework
chatgpt-kotlin

## 项目介绍

chatgpt-kotlin是一款基于Kotlin语言开发的安卓聊天应用。这款应用可以用于创建聊天记录，与chatgpt聊天，保存聊天记录等功能。应用的架构基于MVP模式开发，使用了Dagger2等常用的框架和库。应用的开发环境是Android Studio 4.2.2。

## 功能

chatgpt-kotlin应用的功能包括：

- 创建聊天记录：用户可以在应用中创建聊天记录，包括与chatgpt的聊天记录和用户与其他人的聊天记录。
- 保存聊天记录：应用可以自动保存聊天记录到本地，用户可以在本地查看聊天记录。
- 与chatgpt聊天：应用可以与chatgpt进行聊天，用户可以在应用中输入问题，应用可以自动与chatgpt进行聊天，获取答案。
- 用户聊天记录：用户可以查看与其他人的聊天记录，可以保存聊天记录，也可以与其他人进行聊天。

## 架构

chatgpt-kotlin应用的架构使用了MVP模式，使用了Dagger2等常用的框架和库。

应用的架构如下：

├── app
│ ├── build.gradle
│ ├── proguard-rules.pro
│ ├── src
│ │ ├── androidTest
│ │ ├── main
│ │ │ ├── java/com/chatgptlite/wanted
│ │ │ │ ├── constants
│ │ │ │ ├── data
│ │ │ │ │ ├── ChatRepository.kt
│ │ │ │ │ ├── ChatRepositoryImpl.kt
│ │ │ │ ├── di
│ │ │ │ ├── helpers
│ │ │ │ │ ├── App.kt
│ │ │ │ │ ├── ChatgptHelper.kt
│ │ │ │ ├── models
│ │ │ │ │ ├── Chat.kt
│ │ │ │ ├── ui
│ │ │ │ │ ├── chat
│ │ │ │ │ │ ├── ChatActivity.kt
│ │ │ │ │ │ ├── ChatPresenter.kt
│ │ │ │ │ │ ├── ChatView.kt
│ │ │ │ │ ├── message
│ │ │ │ │ │ ├── DbHelper.kt
│ │ │ │ ├── MainActivity.kt
│ │ │ │ └── MainViewModel.kt
│ │ ├── res
│ │ └── AndroidManifest.xml
│ │ ├── test
│ │ └── ...
├── build.gradle
├── gradle
│ └── wrapper
│ ├── gradle-wrapper.jar
│ └── gradle-wrapper.properties
├── gradle.properties
├── gradlew
├── gradlew.bat
└── settings.gradle

功能实现：

​			应用程序目录包含***应用程序***的所有源代码和资源。它包含一个build.gradle文件，用于配置应用程序的构建过程，以及一个 proguard-rules.pro 文件，其中包含ProGuard的规则，ProGuard是一种用于收缩和混淆代码的工具。

在 ***src*** 目录中，有两个子目录：androidTest 和 main。androidTest 目录包含 Android 上应用程序的集成测试。主目录包含应用程序的大部分源代码和资源，并进一步细分为子目录：

- `constants`：此目录包含整个应用程序中使用的常量值。
- `data`：此目录包含应用程序的数据层，包括存储库和数据源。
- `di`：此目录包含应用程序的依赖关系注入设置。
- `helpers`：此目录包含整个应用程序中使用的实用程序类。
- `models`：此目录包含整个应用程序中使用的数据模型。
- `ui`：此目录包含应用程序的用户界面组件，包括活动、片段和可组合项。
- `MainActivity.kt`：此文件包含应用程序主活动的实现。
- `MainViewModel.kt`：此文件包含应用程序主视图模型的实现。

该项目还包含根级别的其他文件和目录，包括用于配置整个项目的构建过程的build.gradle文件，包含与Gradle构建系统相关的文件的gradle目录，以及用于运行Gradle命令的gradlew和gradlew.bat脚本。gradle.properties 文件包含 Gradle 构建系统使用的属性，settings.gradle 文件用于配置项目的 Gradle 设置。

其中constants保存openai的api和一些链接

​	di目录下有网络组件，定义了一个 Dagger Hilt 的模块 `NetworkModule`，用于提供网络相关的依赖项。

Dagger Hilt 是一个基于 Dagger2 的依赖注入框架，用于简化 Android 应用程序中的依赖项注入。`@Module` 注解表示这是一个 Dagger Hilt 模块类，该类提供了一组相关的依赖项。`@InstallIn` 注解指定了依赖项应该在哪个组件中安装，这里是在 SingletonComponent 中安装，表示这些依赖项是全局单例的。

这个模块提供了三个方法：

1. `provideOkHttpClient()`：提供一个 OkHttpClient 实例，并添加一个网络拦截器，用于在请求头中添加 OpenAI API 的授权信息。
2. `provideRetrofit(okHttpClient: OkHttpClient)`：提供一个 Retrofit 实例，用于创建 OpenAI API 的服务实例。这里使用了 `baseUrlOpenAI` 常量作为基础 URL，`okHttpClient` 参数表示使用提供的 OkHttpClient 实例来处理网络请求。
3. `provideOpenAIService(retrofit: Retrofit)`：提供一个 OpenAIApi 实例，表示使用提供的 Retrofit 实例创建的 OpenAI 服务。这个方法使用了 `@Provides` 和 `@Singleton` 注解，表示这个实例是一个全局单例，并且由 Dagger Hilt 提供。

这个模块的作用是将网络相关的依赖项封装在一个模块中，使得其他组件可以方便地使用这些依赖项，同时也使得代码更加清晰和易于维护。

​		firebase模块是一个 Kotlin 文件，位于包 `com.chatgptlite.wanted.di` 下。它定义了一个 Dagger Hilt 的模块 `FirebaseModule`，用于提供 Firebase 相关的依赖项。

Dagger Hilt 是一个基于 Dagger2 的依赖注入框架，用于简化 Android 应用程序中的依赖项注入。`@Module` 注解表示这是一个 Dagger Hilt 模块类，该类提供了一组相关的依赖项。`@InstallIn` 注解指定了依赖项应该在哪个组件中安装，这里是在 SingletonComponent 中安装，表示这些依赖项是全局单例的。

此外 提供了一个方法：

1. `firestoreInstance()`：提供一个 Firebase Firestore 实例，表示使用 Firebase 的 Firestore 数据库服务。这个方法使用了 `@Provides` 和 `@Singleton` 注解，表示这个实例是一个全局单例，并且由 Dagger Hilt 提供。

这个模块的作用是将 Firebase 相关的依赖项封装在一个模块中，使得其他组件可以方便地使用这些依赖项，同时也使得代码更加清晰和易于维护。在使用这个模块提供的依赖项时，只需要在需要的地方注入相应的依赖项即可。

其中，`@Inject` 注解表示这个依赖项需要注入，`lateinit` 关键字表示这个属性是延迟初始化的。然后，在使用 `firestore` 属性时，就可以直接调用相应的方法

## 用户界面

chatgpt-kotlin应用的界面设计简单易用。应用包括以下界面：

- 主界面：应用的主界面包括一个聊天历史记录的列表，用户可以在列表中选择一个聊天历史记录，可以开始一场新的聊天。聊天历史记录包括chatgpt的聊天记录和用户与另一个用户的聊天记录。
- 聊天界面：应用的聊天界面包括一个聊天窗口，用户可以在聊天窗口中输入聊天内容，与chatgpt聊天或与另一个用户聊天。聊天窗口包括一个输入框和一个发送按钮，用户可以在输入框中输入聊天内容，点击发送按钮可以发送聊天内容。
- 聊天历史记录界面：应用的聊天历史记录界面包括一个聊天历史记录的列表，用户可以在列表中选择一个聊天历史记录，可以查看该聊天历史记录的聊天内容。

## 总结

chatgpt-kotlin是一款基于Kotlin的安卓聊天应用，可以用于创建聊天记录，与chatgpt聊天，保存聊天记录等功能。应用的架构基于MVP模式，使用了Dagger2等常用的框架和库。应用界面简单易用，适用于各种场合。