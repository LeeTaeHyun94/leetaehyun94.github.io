---
layout: post
title:  "Android Setting"
date:   2018-12-30 00:15:00
categories: Android
comments: true
---
! 이 포스팅에서는 React Native App 개발을 위해서 Command Line Tool을 이용하여 Package 설치와 AVD Emulator 세팅까지만 기록되어 있습니다.

! JDK 설치 먼저 하고 봐주시면 감사하겠습니다.

--- 
## 1.  안드로이드 설치
Android 개발 환경설정은 Android Studio를 설치해서 GUI를 이용하여 편하게 할 수 있지만 단지 SDK와 AVD Manager 역할만을 위해서 Android Studio를 깔고 싶지 않은 사람들을 위한 방법입니다.

저는 이미 Intellij를 설치해서 편하게 할 수 있지만 Command Line을 이용해서 해보고 싶었기 때문에...ㅎㅎ

[https://developer.android.com/studio/?hl=ko](https://developer.android.com/studio/?hl=ko)

1. Android Studio 사이트에 들어갑니다.
2. '명령줄 도구만 해당' 탭으로 가서 플랫폼에 맞게 SDK 도구 패키지를 다운받습니다.
    - ![Android SDK tools 설치](./../../assets/Android/1.PNG)
3. 다운받은 압축 폴더를 압축을 해제합니다.
4. 이제 해당 Android SDK 폴더를 원하는 경로에 저장합니다. (앞으로 모든 Android 관련 경로 지정은 그곳으로 해주면 됩니다.)
5. CMD에서 명령어를 편하게 사용하기 위한 환경 변수 설정
    - 시스템 변수 추가 : 이름은 ANDROID_HOME, 값은 Android SDK 폴더로 지정
    - 사용자 변수 or 시스템 변수 Path에 %ANDROID_HOME%\tools\bin, %ANDROID_HOME%\emulator 추가

---
## 2. 원하는 Package 설치
- sdkmanager --list : 설치된 패키지와 설치 가능한 패키지의 목록을 확인
- sdkmanager [패키지명] : 해당 패키지를 설치
- sdkmanager --uninstall [패키지명] : 설치된 해당 패키지를 삭제

저는 React Native App을 실행시킬 수 있도록 필요한 27.0.0 버전의 패키지들을 설치해 주었습니다.

### * Example
```
sdkmanager platform-tools
sdkmanager emulator
sdkmanager extras;intel;Hardware_Accelerated_Execution_Manager
sdkmanager build-tools;27.0.0
sdkmanager platforms;android-27
sdkmanager system-images;android-27;default;x86_64
```
---
## 3. AVD 설정
- avdmanager create avd -n [디바이스 이름] -k "[디바이스에 사용될 안드로이드 버전 패키지]" --device "[디바이스 종류]" : AVD 생성
- avdmanager delete avd -n [디바이스 이름] : 해당 AVD 삭제

저는 안드로이드 버전은 27.0.0(8.0 Oreo), 디바이스 종류는 Nexus 5X, test라는 이름으로 AVD를 생성해 주었습니다.
### * Example
```
avdmanager create avd -n test -k "system-images;android-27;default;x86_64" --device "Nexus 5X"
avdmanager delete avd -n test
```
---
## 4. AVD Emulator 실행
- emulator -list-avds : 현재 사용 가능한 AVD 목록 조회
- emulater -avd [디바이스 이름] : 해당 AVD Emulator 가동

---
## 5. Enable Keyboard
이 포스팅에 나온대로 Android Emulator Setting을 하게 되면 Keyboard로 입력이 불가능하기 때문에 설정을 추가해줘야 한다.

C:\Users\[사용자명]\\.android\avd\[디바이스 이름]\config.ini

위 경로의 파일에 hw.keyboard=yes 추가해주면 Keyboard로 입력이 가능하다!
(만약 이미 있다면 no -> yes 바꿔주기만 하면 된다.)