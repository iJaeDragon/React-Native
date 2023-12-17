# Expo 

Expo는 완성된 프로젝트를 쉽게 배포 및 관리할 수 있도록 다양한 기능을 제공함 아이폰과 안드로이드 폰이 있으면 Xcode, Android Studio 없이도 해당 플랫폼의 테스트를 진행할 수 있음.

대표적인 단점은 Expo에서 제공하는 API만 사용할 수 있으며 필요한 기능이 제공되지 않을 경우 네이티브 모듈을 추가로 만들어서 사용하는 것이 불가능함.

· Expo : https://expo.io

![Alt text](image-2.png)

## Expo 설치와 프로젝트 생성

Expo를 이용하려면 npm을 이용해서 expo-cli를 설치해야 한다.
npm 도구는 NodeJS 설치 시 기본적으로 포함되며 버전은 5.5.1로 받는다.
이후 출시된 6.0.0 부터 Expo CLI용 웹 UI를 지원하지 않는다.
참고 : https://blog.expo.dev/sunsetting-the-web-ui-for-expo-cli-ab12936d2206

웹 UI 사용을 추천하지는 않는 것 같다.

```
npm install --global expo-cli@5.5.1
```

설치가 완료되면 다음 명령어로 Expo 프로젝트를 실행
```
expo init my-first-expo
```
![Alt text](image-3.png)
blank 선택

## Expo 프로젝트 실행

```
cd my-first-expo
```

```
npm start
```
혹은 webui를 보기 위해선 아래 커맨드를 입력한다.
```
expo start
```

