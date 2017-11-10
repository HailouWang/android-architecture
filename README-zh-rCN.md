# todo-mvp

这个版本的应用叫做todo-mvp ， 并为项目中的其他实例提供依据。这个实例旨在：
* 在不使用任何其他框架的前提下，提供一个基本的[Model-View-Presenter](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter) (MVP)架构。
* 作为与本项目中其他项目比较、对照的参考依据。


**备注：** 本项目中所有分支代码库，使用如下命名惯例，来区分View 对象以及MVP 视图。

* "Android View" 是指：[android.view.View](https://developer.android.com/reference/android/view/View.html)包下面的类实现。
* 从MVP中的presenter中接收指令的view，被称为 "view"。

### 准备工作

在浏览本示例之前，熟悉以下示例会对你很有帮助：
* [project README](https://github.com/googlesamples/android-architecture/tree/master)
* [MVP](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter) 架构

todo-mvp 示例 使用了如下的依赖项：
* [Common Android support libraries](https://developer.android.com/topic/libraries/support-library/index.html) -  在com.android.support.* 命名空间下的包提供向下兼容以及其他功能特性。
* [Android Testing Support Library](https://developer.android.com/topic/libraries/testing-support-library/index.html) -  用于支持UI测试的框架，同时使用：Espresso和AndroidJUnitRunner。
* [Mockito](http://site.mockito.org/) - 一个模拟框架，用于实现单元测试。
* [Guava](https://github.com/google/guava) - 一套Google常用的Java核心库，常用在Android应用程序中。

### 应用程序设计
每一个版本的Android Blueprints应用程序都包含一个常见的代办事项功能。应用程序有如下四个UI界面组成：
* Tasks - 用于管理任务结合。
* TaskDetail - 用于读取任务详情。
* AddEditTask - 用于添加或者编译任务。
* Statistics - 展示任务相关的统计。


在这个版本的应用程序中，以及基于它的其他版本，每一个界面都是使用如下类和接口来实现的：

* 契约（Contract）类。定义了view和presenter之间的连接。
* [Activity](https://developer.android.com/reference/android/app/Activity.html) 。在该页面，创建了Fragments以及Presenters。
* [Fragment](https://developer.android.com/reference/android/app/Fragment.html)。该实例实现了view 的接口。
* presenter。实现了相应契约（Contract）类中presenter接口。

presenter通常托管特定功能的业务逻辑，同时相应的view用来处理 Android UI 线程工作。view中几乎不含有任何逻辑；view会将presenter的指令转化为UI操作，并监听用户操作，然后将这些操作指令传递给presenter。

### 应用程序实现

应用程序的不同版本都使用不同的方法来实现相同的功能，以展示和对比各种不同的架构设计。例如：这个版本使用如下的方式解决常见的实现问题：

* 示例，在编译时使用[product flavors](https://developer.android.com/studio/build/build-variants.html) 来替换modules，为手动和自动测试提供模拟数据。
* 这个版本使用回调来解决异步任务。

另外：在下面的插图中，这个版本的应用程序使用Fragment，有如下两个原因：

* 同时使用[activities](https://developer.android.com/guide/components/activities/index.html) 和 [fragments](https://developer.android.com/guide/components/fragments.html) 考量点在于这样能够更好的进行分离，补充了MVP的实现。在这个版本的应用程序中，Activity作为一个整体的连接器，创建、连接着views和presenters。
* 使用framgments可以支持tablet布局以及多个views的UI屏幕。

<img src="https://github.com/googlesamples/android-architecture/wiki/images/mvp.png" alt="Illustration of the MVP architechture for this version of the app."/>

这个版本的应用程序包含一系列的单元测试，包括：presenters、repositories还有data sources。示例同样包含基于模拟数据的UI测试，使用依赖注入来使用模拟模块。有关更多使用依赖注入来进行测试的信息，请参阅：[Leveraging product flavors in Android Studio for hermetic testing](https://android-developers.googleblog.com/2015/12/leveraging-product-flavors-in-android.html).

### 应用程序维护

示例包含了类文件以及接口文件，例如：presenters和contracts，与不适用特定体系架构的传统项目相比，MVP这种方式增加代码行数。

下面的表格总结了使用当前版本架构的应用程序的代码量。你可以将其用作与本工程其他实例所提供的类似表格比较、对比的基础依据。

| Language      | Number of files | Blank lines | Comment lines | Lines of code |
| ------------- | --------------- | ----------- | ------------- | ------------- |
| **Java**      |               46|         1075|           1451|           3451|
| **XML**       |               34|           97|            337|            601|
| **Total**     |               80|         1172|           1788|           4052|