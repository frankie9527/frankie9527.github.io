---
title: Android Test
description: >-
 写测试用例是程序员的必备技能，在国外的招聘要求中不论android，后端还是前端都会列出必须能写出测试用例。所以这篇
 文章通过阅读google 和code后的个人总结
author: cotes
date: 2024-04-1 16:05:00 +0800
categories: [ framework,  summary ]
tags: [  summary ]
render_with_liquid: false


---
## junit
创建android 项目时候，会有2个测试文件夹，一个是模拟android 运行环境测试，一个是本地的junit测试
#### 添加 junit 依赖
```
dependencies {
  // Required -- JUnit 4 framework
  testImplementation "junit:junit:$jUnitVersion"
  // Optional -- Robolectric environment
  testImplementation "androidx.test:core:$androidXTestVersion"
  // Optional -- Mockito framework
  testImplementation "org.mockito:mockito-core:$mockitoVersion"
  // Optional -- mockito-kotlin
  testImplementation "org.mockito.kotlin:mockito-kotlin:$mockitoKotlinVersion"
  // Optional -- Mockk framework
  testImplementation "io.mockk:mockk:$mockkVersion"
}
```
- 添加以后以后就可以进行junit 测试了，比如你有一个utils 是验证邮箱的。那么junit 伪代码如下

```
import org.junit.Assert.assertFalse
import org.junit.Assert.assertTrue
import org.junit.Test

class EmailValidatorTest {
  @Test fun emailValidator_CorrectEmailSimple_ReturnsTrue() {
    assertTrue(EmailValidator.isValidEmail("name@email.com"))
  }

}
```

#### 使用 mockito 进行本地测试
因为本地测试是没有android运行环境的，调用的一些方法也许fw的底层进行了移除，就是仅仅给了一个方法可以调用，所以测试的时候我们可以模拟环境，创建虚假对象。
如果我讲的不够明白，可以[点击](https://developer.android.com/training/testing/local-tests)阅读官方文档
[mock code](https://github.com/android/testing-samples/tree/main/unit/BasicSample)
[Android Testing Codelab](https://developer.android.com/codelabs/advanced-android-kotlin-training-testing-basics#0) android 代码实验室，看这个差不多就应该懂了

## 使用espresso 进行ui测试
这个是android 提出的一个ui测试框架，可以测试android ui相关
```
// runner、rules、espresso-core 作为base 基本都要依赖
androidTestImplementation 'androidx.test:runner:1.4.0'
androidTestImplementation 'androidx.test:rules:1.4.0'
androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
//  RecyclerView、DatePicker 和Drawer  相关的库
androidTestImplementation 'androidx.test.espresso:espresso-contrib:3.4.0'
// 测试intent
androidTestImplementation 'androidx.test.espresso:espresso-intents:3.4.0'
// 测试多进程
androidTestImplementation 'androidx.test.espresso:espresso-remote:3.4.0'
// 测试web
androidTestImplementation 'androidx.test.espresso:espresso-web:3.4.0'    
```

官方代码如下
```
// withId(R.id.my_view) is a ViewMatcher
// click() is a ViewAction
// matches(isDisplayed()) is a ViewAssertion
onView(withId(R.id.my_view))
.perform(click())
.check(matches(isDisplayed()))
// 翻译过来就是 id 为my_view 点击以后检查是否显示出来
```

我写的demo 代码如下 [code](https://github.com/frankie9527/AndroidDocumentProject/tree/main/AndroidTestPractice)
```
//检查editText hint 是否符合预期
@Test
   fun editText_hint_check() {
       ActivityScenario.launch<BaseUseActivity>(BaseUseActivity::class.java).use { scenario ->
         val appContext = InstrumentationRegistry.getInstrumentation().targetContext
         val hint = appContext.resources.getText(R.string.hint)
         onView(withId(R.id.ed)).check(matches(HintMatcher.withHint(hint.toString())))
    }
}
```
个人总结一点，espresso 还是相对简单的，并且有大量的demo 进行学习！主要不会写可以看看官方code 和doc 就可以很好掌握了

- [doc](https://developer.android.com/training/testing/espresso)   谷歌文档
- [code](https://github.com/android/testing-samples/tree/main/ui/espresso)  官方demo

## 使用hilt 依赖注入
查看国外招聘条件的时候，发现junit测试和hilt 依赖注入是基本项目。后来深入了解发现使用了hilt依赖注入后，写测试用例是真的简单。
#### 添加依赖
```
dependencies {
    // For Robolectric tests.
    testImplementation("com.google.dagger:hilt-android-testing:2.44")
    // ...with Kotlin.
    kaptTest("com.google.dagger:hilt-android-compiler:2.44")
    // ...with Java.
    testAnnotationProcessor("com.google.dagger:hilt-android-compiler:2.44")


    // For instrumented tests.
    androidTestImplementation("com.google.dagger:hilt-android-testing:2.44")
    // ...with Kotlin.
    kaptAndroidTest("com.google.dagger:hilt-android-compiler:2.44")
    // ...with Java.
    androidTestAnnotationProcessor("com.google.dagger:hilt-android-compiler:2.44")
}
```
#### 添加 HiltTestApplication
- 创建类如下
```
class HiltJUnitRunner : AndroidJUnitRunner() {
    override fun newApplication(
        cl: ClassLoader?,
        className: String?,
        context: Context?
    ): Application {
        return super.newApplication(cl, HiltTestApplication::class.java.name, context)
    }
}
```

- 在 build.gradle 添加  testInstrumentationRunner = "com.sixth.space.HiltJUnitRunner"
```
android {
    namespace = "com.sixth.space"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.sixth.space"
        minSdk = 24
        targetSdk = 34
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "com.sixth.space.HiltJUnitRunner"
    }
```

#### 实现测试功能
因为hilt 是依赖注入，所以在项目中你肯定依赖注入很多类，这些类就可以直接通过依赖注入直接获得，如下是我项目测试代码
```
@HiltAndroidTest  //类声明，这个是必须做的
class RetrofitTest {
    @get:Rule  //It manages the components' state and is used to perform injection on your test:
    val hiltRule = HiltAndroidRule(this)
    @Inject //
    lateinit var service: RetrofitService;
    @Before
    fun init(){
        hiltRule.inject()
    }
    @Test
    fun test_tiktok_net()= runBlocking {
        // 测试http 返回数据是否大于0
        val data=service.fetchTiktok("","");
        assertTrue(data.itemList.size>0)
    }
}
```
看了[我的代码](https://github.com/frankie9527/ArchitecturePractice) 是不是感觉很简单呀，如果还不懂可以看看[官方文档](https://developer.android.com/training/dependency-injection/hilt-testing)
