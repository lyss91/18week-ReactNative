# React Native

- 앱 개발시 선택하는 방법
- Native (Java, Kotlin, Object-C, Swift) 말고 선택시
- Flutter 또는 React Native 입니다.
- React Native 는 개발 도구로 Expo, React Native Cli 제공
- React Native Cli 환경설정이 까다롭다.
- iOS, Android 개발이 가능한데, iOS 는 반드시 맥필요.

## 환경설정

- https://velog.io/@it-ju/React-native-cli-개발환경-세팅하기
- https://reactnative.dev/docs/0.72/environment-setup

### 1. choco 설치 및 환경 확인

- Power Shell 을 관리자 모드로 실행
- https://chocolatey.org/install 접속
  - 아래 문장을 입력 후 엔터

```bash
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

- Power Shell 에 `choco` 입력 후 버전 출력되는지 확인

```bash
Chocolatey v2.2.2
Please run 'choco -?' or 'choco <command> -?' for help menu.
```

- Power Shell 관리자 모드에서 choco 를 이용해서 설치 필요

```bash
choco install -y nodejs-lts microsoft-openjdk17
```

### 2. Android Studio 설치

- https://developer.android.com/studio?hl=ko

#### 2.1. 시작화면에서 > More Action 에서 셋팅 가능

#### 2.2. File > settings... 메뉴 > Laguage & Framework > Android SDK

#### 2.3. Android SDK 세팅

- Android API 35("VanillaIceCream")

```
  Android SDK Platform 35
  ARM 64 v8a System Image
  Intel x86_64 Atom System Image
  Google APIs ARM 64 v8a System Image
  Google APIs Intel x86_64 Atom System Image
  Google Play ARM 64 v8a System Image
  Google Play Intel x86_64 Atom System Image
```

- Android 14.0("UpsideDownCake")

```
Android SDK Platform 34
Source for Android 34
ARM 64 v8a System Image
Intel x86_64 Atom System Image
Google APIs ARM 64 v8a System Image
Google APIs Intel x86_64 Atom System Image
Google Play ARM 64 v8a System Image
Google Play Intel x86_64 Atom System Image
```

- Android 13.0("Tiramisu")

```
Android SDK Platform 33
ARM 64 v8a System Image
Intel x86_64 Atom System Image
Google APIs ARM 64 v8a System Image
Google APIs Intel x86_64 Atom System Image
Google Play ARM 64 v8a System Image
Google Play Intel x86_64 Atom System Image
```

#### 2.4. SDK Tools 세팅

- Android SDK Buil-Tools 36-rc5
- NDK
- CMake
- Android Emulator
- Android Emulator hypervisor driver
- Android SDK Platform-Tools
- Google Play Service

#### 2.5. Android SDK Location 을 복사해 주세요.

```
C:\Users\Administrator\AppData\Local\Android\Sdk
```

#### 2.6. Android Virtual Device

- 시작화면에서 > More Action 에서 > Virtual Machine Manager 실행 후 추가
- 또는 우축 화면 상단의 Device Manager 에서 추가
- `Pixcel 7' 으로 생성하자.

### 3. Path 설정

- 윈도우 하단 툴바의 검색창에서 `시스템 환경 변수` 검색 후 진입
  - `환경 변수 버튼` 클릭
- 새로 만들기
  - 변수 명 : `ANDROID_HOME`
  - 변수 값 : `C:\Users\Administrator\AppData\Local\Android\Sdk`
- 수정 및 추가
- `path` 항목 더블클릭
- 항목 추가 : `%ANDROID_HOME%\platform-tools`

### 4. Path 설정 실행 확인(Power Shell 관리자 모드)

- `Get-ChildItem -Path Env:\` 엔터
- `adb --version` 엔터
- 결과가 안나오면 PC 를 껏다가 켜보자.

## 프로젝트 생성

- 절대로 한글 폴더에 생성하시면 안됩니다.
- 특수기호가 포함된 앱이름은 배제하자.
- `npx react-native@0.72.6 init 앱이름 --version 0.72.6`

### 프로젝트 실행전 반드시 준비해 두자.

- Android Studio 실행 > Device Virtual Machine 을 실행해 놓고 진행

### 만약 실행이 안되면 해 보아야 하는 것

- `cd android` 로 anodroid 폴더로 이동
- 터미널에 `./gradlew clean` 으로 프로젝트 다시 초기화
- 완료 후 `cd ..` 상위폴더 이동
- 다시 `npm run start` 실행 후 결과 확인
- 그래도 안되면 `npx react-native doctor` 명령으로 현재 상태 확인 후 조치

# 추후 브랜치

- webview
- splash screen
- icon
- back 키
- apk 생성
- webview 와 js 연동

# Webview 적용하기

- https://www.npmjs.com/package/react-native-webview
- `npm i react-native-webview`

```tsx
import React from 'react';
import {SafeAreaView, StyleSheet} from 'react-native';
import WebView from 'react-native-webview';

const App = (): JSX.Element => {
  const webViewUrl = 'https://app-fish-y3pa.vercel.app';
  return (
    <SafeAreaView style={styles.container}>
      <WebView source={{uri: webViewUrl}} style={styles.webview} />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000',
  },
  webview: {
    flex: 1,
  },
});
export default App;
```
