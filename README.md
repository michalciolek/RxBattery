<p align="center"><img src="logo.png" alt="RxBattery" height="150px"></p>

RxBattery [![Build Status](https://img.shields.io/travis/pwittchen/RxBattery.svg?branch=master&style=flat-square)](https://travis-ci.org/pwittchen/RxBiometric)  ![Maven Central](https://img.shields.io/maven-central/v/com.github.pwittchen/rxbattery.svg?style=flat-square)
=========
Android library monitoring battery state of the device with RxJava and RxKotlin

Contents
--------

- [Usage](#usage)
- [Examples](#examples)
- [Download](#download)
- [Tests](#tests)
- [Code style](#code-style)
- [Static code analysis](#static-code-analysis)
- [JavaDoc](#javadoc)
- [Changelog](#changelog)
- [Releasing](#releasing)
- [References](#references)
- [Credits](#credits)
- [License](#license)

Usage
-----

In the **Kotlin** application, you can use library as follows:

```kotlin
RxBattery
  .observe(context)
  .subscribeOn(Schedulers.io())
  .observeOn(AndroidSchedulers.mainThread())
  .subscribe { textView.text = it.toString() }
```

In the **Java** application, you can use library as follows:

```java
RxBattery
  .observe(context)
  .subscribeOn(Schedulers.io())
  .observeOn(AndroidSchedulers.mainThread())
  .subscribe(batteryState -> {
    textView.setText(batteryState.toString());
  });
```

`BatteryState` data class looks as follows:

```kotlin
data class BatteryState(
  val statusCode: Int,
  val pluggedCode: Int,
  val healthCode: Int,
  val level: Int,
  val temperature: Int,
  val voltage: Int,
) {
  fun status(): Status { ... }
  fun plugged(): Plugged { ... }
  fun health(): Health { ... }
}
```

All `Integer` values returned by `BatteryState` object are reflected in constants of [`BatteryManager`](https://developer.android.com/reference/android/os/BatteryManager) class from the Android SDK. Enums `Status`, `Plugged` and `Health` represents battery state translated from integer codes from `BatteryManager` class.

Examples
--------

Exemplary Kotlin application is located in `app-kotlin` directory.

Download
--------

You can depend on the library through Gradle:

```groovy
dependencies {
  implementation 'com.github.pwittchen:rxbattery:0.1.0'
}
```

Tests
-----

Tests are available in `library/src/test/kotlin/` directory and can be executed on JVM without any emulator or Android device from Android Studio or CLI with the following command:

```
./gradlew test
```

Code style
----------

Code style used in the project is called `SquareAndroid` from Java Code Styles repository by Square available at: https://github.com/square/java-code-styles.

Static code analysis
--------------------

Static code analysis runs Checkstyle, FindBugs, PMD, Lint, KtLint and Detekt. It can be executed with command:

```
./gradlew check
```

Reports from analysis are generated in `library/build/reports/` directory.

JavaDoc
-------

Documentation can be generated as follows:

```
./gradlew dokka
```

Output will be generated in `library/build/javadoc`

JavaDoc can be viewed on-line at https://pwittchen.github.io/RxBattery/library/

Changelog
---------

See [CHANGELOG.md](https://github.com/pwittchen/RxBattery/blob/master/CHANGELOG.md) file.

Releasing
---------

See [RELEASING.md](https://github.com/pwittchen/RxBattery/blob/master/RELEASING.md) file.

References
----------
- https://developer.android.com/training/monitoring-device-state/index.html
- https://developer.android.com/training/monitoring-device-state/battery-monitoring.html
- https://developer.android.com/reference/android/os/BatteryManager
- https://developer.android.com/studio/profile/battery-historian.html
- https://stackoverflow.com/questions/3291655/get-battery-level-and-state-in-android
- https://stackoverflow.com/questions/25932677/proper-optimized-way-to-monitor-battery-level-in-android
- https://stackoverflow.com/questions/32608505/broadcast-receiver-monitoring-the-battery-level-and-charging-state
- https://github.com/jaredsburrows/android-gradle-kotlin-app-template
- http://wittchen.io/2018/08/19/writing-my-first-library-in-kotlin/

Credits
-------

Logo of the project was created by [@Yasujizr](https://github.com/Yasujizr).

License
-------

    Copyright 2018 Piotr Wittchen

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
