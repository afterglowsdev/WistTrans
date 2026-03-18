# WristTrans

WristTrans is a Wear OS translation app focused on fast wrist-based text input and clean Material Design 3 presentation.

Current package name: `work.czzzz.wristtrans`  
Current version: `v1.01`  
Version code: `101`

## Features

- Wear OS UI built with `AppScaffold` and `ScalingLazyColumn`
- Large MD3-style input card for entering text
- System keyboard input via `RemoteInputIntentHelper`
- Quick language switching between English and Chinese
- Translation history rendered as card-based list items
- Retrofit-based API integration for remote translation requests
- GitHub Actions workflow for signed release builds

## UI Structure

- Top: input area with translation result preview
- Middle: source / target language switcher
- Bottom: translation history list

The current UI follows a Material 3 direction and uses Wear Compose components such as `OutlinedCard`, `Button`, `OutlinedButton`, and `TitleCard`.

## Translation API

Base URL:

```text
https://api.urlf.eu.org/
```

Request:

- Method: `GET`
- Endpoint: `/`
- Query params:
  - `q`: text to translate
  - `to`: target language, default `zh-CN`
  - `from`: source language, default `auto`

Example response:

```json
{
  "status": "success",
  "original": "Hello",
  "translated": "你好",
  "from": "en"
}
```

Relevant source files:

- [Translation response model](/D:/translatorapp/WristTrans/app/src/main/java/work/czzzz/wristtrans/data/model/TranslationModels.kt)
- [Retrofit service](/D:/translatorapp/WristTrans/app/src/main/java/work/czzzz/wristtrans/data/network/TranslationService.kt)
- [Retrofit builder](/D:/translatorapp/WristTrans/app/src/main/java/work/czzzz/wristtrans/data/network/TranslationApi.kt)

## Tech Stack

- Kotlin
- Android Gradle Plugin `8.6.1`
- Kotlin Gradle Plugin `1.9.25`
- Jetpack Compose for Wear OS
- Wear Compose Material 3
- AndroidX Lifecycle
- Retrofit 2
- OkHttp
- Coroutines

## Project Structure

```text
WristTrans/
├─ app/
│  ├─ src/main/java/work/czzzz/wristtrans/
│  │  ├─ MainActivity.kt
│  │  ├─ data/
│  │  └─ ui/
│  └─ src/main/res/
├─ .github/workflows/
└─ build.gradle.kts
```

## Build Requirements

- JDK 17
- Android compile SDK 35
- Wear OS compatible Android toolchain

This repository currently includes Gradle build scripts and a GitHub Actions workflow, but if you want to build locally you should also ensure a Gradle wrapper is present in the repository or use a compatible local Gradle installation.

## GitHub Actions Release Build

The repository includes a workflow at:

- [.github/workflows/android-release.yml](/D:/translatorapp/WristTrans/.github/workflows/android-release.yml)

It performs:

- checkout
- JDK setup
- Android SDK setup
- keystore decode from repository secrets
- signed `assembleRelease`
- signed `bundleRelease`
- artifact upload for `APK` and `AAB`

## Required GitHub Secrets

Add these secrets in:

`Repository Settings -> Secrets and variables -> Actions`

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

The workflow decodes the keystore during CI and uses environment variables to configure release signing.

## Local Signing

Release signing is enabled when these environment variables are available:

- `KEYSTORE_PATH`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

If they are not set, the release build configuration remains unsigned.

## Current Status

Implemented:

- core Wear OS UI scaffold
- translation request models and service
- basic ViewModel-driven state flow
- GitHub Actions release packaging and signing flow

Not yet included:

- persistent local database for history
- voice input
- advanced language selection list
- offline translation support
- tests

## License

No license file has been added yet. If this repository is intended to be open source, add a license before publishing wider reuse terms.


# WristTrans.cn

WristTrans 是一个面向 Wear OS 的手表翻译应用，重点是快速输入、清晰展示，以及符合 Material Design 3 风格的腕上交互体验。

当前包名：`work.czzzz.wristtrans`  
当前版本：`v1.01`  
版本号：`101`

## 项目简介

这个项目目前已经完成一版可打包的核心骨架，包含：

- Wear OS 主界面
- 系统键盘输入
- 中英快速切换
- 翻译历史记录展示
- Retrofit 翻译接口接入
- GitHub Actions 自动签名打包流程

## 功能特性

- 使用 `AppScaffold + ScalingLazyColumn` 构建手表主界面
- 顶部大号输入卡片，点击后调用系统标准软键盘
- 中部语言切换区域，适合手表屏幕的快速操作
- 底部历史记录卡片列表，便于查看最近翻译内容
- 使用 ViewModel + StateFlow 管理翻译状态
- 使用 Retrofit + OkHttp 请求远程翻译服务
- 支持通过 GitHub Actions 自动构建签名版 `APK` / `AAB`

## 界面结构

- 顶部：输入区域与翻译结果预览
- 中部：源语言 / 目标语言切换
- 底部：翻译历史记录

当前界面以 Wear Compose Material 3 为主，核心组件包括：

- `OutlinedCard`
- `OutlinedButton`
- `Button`
- `TitleCard`
- `ScalingLazyColumn`

## 翻译接口

基础地址：

```text
https://api.urlf.eu.org/
```

请求方式：

- 方法：`GET`
- 路径：`/`

请求参数：

- `q`：待翻译文本
- `to`：目标语言，默认 `zh-CN`
- `from`：源语言，默认 `auto`

返回示例：

```json
{
  "status": "success",
  "original": "Hello",
  "translated": "你好",
  "from": "en"
}
```

相关代码位置：

- [数据模型](/D:/translatorapp/WristTrans/app/src/main/java/work/czzzz/wristtrans/data/model/TranslationModels.kt)
- [Retrofit 接口](/D:/translatorapp/WristTrans/app/src/main/java/work/czzzz/wristtrans/data/network/TranslationService.kt)
- [Retrofit 配置](/D:/translatorapp/WristTrans/app/src/main/java/work/czzzz/wristtrans/data/network/TranslationApi.kt)

## 技术栈

- Kotlin
- Android Gradle Plugin `8.6.1`
- Kotlin `1.9.25`
- Jetpack Compose for Wear OS
- Wear Compose Material 3
- AndroidX Lifecycle
- Retrofit 2
- OkHttp
- Kotlin Coroutines

## 项目结构

```text
WristTrans/
├─ app/
│  ├─ src/main/java/work/czzzz/wristtrans/
│  │  ├─ MainActivity.kt
│  │  ├─ data/
│  │  └─ ui/
│  └─ src/main/res/
├─ .github/workflows/
├─ build.gradle.kts
├─ settings.gradle.kts
└─ gradle.properties
```

## 构建要求

- JDK 17
- Android Compile SDK 35
- 可用的 Android SDK / Build Tools

如果你要在本地构建，建议补充 Gradle Wrapper，或者使用兼容版本的本地 Gradle 环境。

## GitHub Actions 自动打包

仓库已包含工作流文件：

- [.github/workflows/android-release.yml](/D:/translatorapp/WristTrans/.github/workflows/android-release.yml)

该工作流会执行：

- 检出代码
- 配置 JDK 17
- 配置 Android SDK
- 从 GitHub Secrets 解码签名文件
- 构建签名版 `assembleRelease`
- 构建签名版 `bundleRelease`
- 上传 `APK` 与 `AAB` 产物

## GitHub Secrets 配置

请在以下位置添加 Secrets：

`Repository Settings -> Secrets and variables -> Actions`

需要的变量：

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

CI 中会自动解码 keystore 并用于 Release 签名。

## 本地签名环境变量

如果要在本地进行签名构建，需要提供以下环境变量：

- `KEYSTORE_PATH`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

未提供时，Release 配置不会绑定签名信息。

## 当前状态

已完成：

- 核心 Wear OS UI 骨架
- 翻译接口模型与 Service
- ViewModel 状态流
- GitHub Actions 自动签名打包

暂未实现：

- 历史记录持久化
- 语音输入
- 完整语言选择列表
- 离线翻译
- 自动化测试

## License

当前仓库还没有添加许可证文件。  
如果你准备公开发布这个项目，建议补一个明确的开源许可证。
