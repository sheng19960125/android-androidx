# android-androidx
##  簡易介紹AndroidX  
AndroidX 是 Google 2018 IO 大會推出的新擴展庫，主要是對 Android支持庫做了重大改進。與支持庫一樣，AndroidX 與 Android 作業系統分開提供，並與各個 Android 版本向後兼容，可以說 AndroidX 就是為了替換 Android 支持庫而設計的。

##  甚麼是AndroidX?
* AndroidX 是 Android 團隊用於在Jetpack中開發、測試、打包和發布庫以及對其進行版本控制的開源項目。    
* AndroidX 完全取代了支持庫，不僅提供同等的功能，而且提供了新的庫。
* AndroidX內置原始支持庫API軟體包映射到androidx命名空間。只有軟體包和Maven工件名稱發生了變化；類，方法和欄位名稱沒有改變。
* 與支持庫不同，AndroidX 軟體包會單獨維護和更新。androidx 軟體包使用嚴格的語義版本控制，從版本 1.0.0 開始，可以單獨更新項目中的 AndroidX 庫。
* 所有新支持庫的開發工作都將在 AndroidX 庫中進行，這包括維護原始支持庫工件和引入新的 Jetpack 組件。

##  什麼是Jetpack?
Google 为了帮助 Android 开发者更快更好地开发 App，推出了一系列组件，这些组件被打包成了一个整体，称作Android Jetpack，它包含的组件如下图所示：

老的`support`包被整合進了`Jetpack`，例如上圖`Foundation Model`的AppCompat，整合進去之後，包名做了一下修改，全部以`androidx`為開頭。AndroidStudio提供的遷移工具`（Refactor > Migrate to AndroidX）`可以將源碼中的舊包名替換成新的，但是如果Maven依賴的生成物不再遷移到`AndroidX`的話，還需要配置一個工具-`Jetifier`，只需要在build.gradle中加上兩行配置即可: 
```
android.useAndroidX=true
android.enableJetifier=true
```
而添加後，`Jetfier`會在編譯階段直接修改依赖產物的字節碼，簡易粗暴。

### Jetpack架構簡易說明
Jetpack其實不屬於Android Framework，不是Android開發中所必要的，他只屬於一種應用層面的開發副助工具。幫我們解決一些在相較之前版本裡面會容易出現的問題，例如：版本兼容性、生命週期管理、API應用等等，其中Architecture部分組件，(Android Architecture Components，簡稱 AAC)，组合起來形成了一套完整的架構解决方案。

##  為什麼要遷移 AndroidX？
以官方文黨為例如下：
```
Existing packages, such as the Android Support Library, are being refactored into AndroidX.
Although Support Library versions 27 and lower are still available on Google Maven,
all new development will be included in only AndroidX versions 1.0.0 and higher.
```
簡易來說，存在現有的andorid支持庫，正在被重建為androidx，新開發將只包含於Androidx 1.0.0以及更高版本中，簡易來說以前得版本依樣可以坐使用，相較作為普遍狀況來說是好友善的。

##  AndroidX 遷移步驟?
1.在更新前有前提必須遵守：    
* Android studio 升級到 3.2 及以上    
* Gradle 插件版本改為 4.6 及以上
* compileSdkVersion 版本升級到 28 及以上
* buildToolsVersion 版本改為 28.0.2 及以上       
    
2.配置方法：
* 在`gradle.properties`文件里添加如下配置：
```
android.useAndroidX=true      //  表示當前項目啟用 androidx
android.enableJetifier=true   // 表示將依賴包也遷移到androidx
```     
    
3.修改依賴庫銘：
以基礎為例，如下：
```
before: implementation 'com.android.support:appcompat-v7:28.0.2'
after : mplementation 'androidx.appcompat:appcompat:1.0.0'

before: implementation 'com.android.support:design:28.0.2'
after : implementation 'com.google.android.material:material:1.0.0'

before: implementation 'com.android.support.constraint:constraint-layout:1.1.2'
after : implementation 'androidx.constraintlayout:constraintlayout:1.1.2'
```
此三種為最基礎的依賴庫映射
    
4.依賴類重新導包：
將原來 import 的 android.** 包刪除，重新 import 新的 androidx.** 包
```
before : import android.support.v7.app.AppCompatActivity; 
after  : import androidx.appcompat.app.AppCompatActivity;
```
##  整合庫
```
<android.support.v4.widget.NestedScrollView/>	 ->   <androidx.core.widget.NestedScrollView/>
```

##  支持庫的用途

