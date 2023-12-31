# Expo 

Expo는 완성된 프로젝트를 쉽게 배포 및 관리할 수 있도록 다양한 기능을 제공함 아이폰과 안드로이드 폰이 있으면 Xcode, Android Studio 없이도 해당 플랫폼의 테스트를 진행할 수 있음.

대표적인 단점은 Expo에서 제공하는 API만 사용할 수 있으며 필요한 기능이 제공되지 않을 경우 네이티브 모듈을 추가로 만들어서 사용하는 것이 불가능함.

· Expo : https://expo.io

![image-2](https://github.com/iJaeDragon/React-Native/assets/66985977/ec087a97-efe2-491d-b1f0-9e8bec6c712c)

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
![image-3](https://github.com/iJaeDragon/React-Native/assets/66985977/aff89dc9-5bbb-4df1-9b9a-d0b5206a00b9)

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

## 확인

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/5fb6081d-0499-4bd8-bc67-e72a1c6674d4)

### web ui
![image](https://github.com/iJaeDragon/React-Native/assets/66985977/f89b6032-043f-44ea-b99b-4280143e058d)

테스트 하려는 기기에서 구글 스토어 혹은 앱스토에서 Expo 애플리케이션을 다운받아 설치하고
화면에서는 보이는 qr코드를 Expo 애플리케이션을 통해 스캔하여 테스트를 진행한다.

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/5a66944f-7816-4653-97de-be6fd5a965ae)

## 내보내기

Expo 프로젝트의 장점을 수용하기 위해 Expo 프로젝트로 시작했지만, 프로젝트의 상황에 따라 네이티브 모듈을 건드리거나 기타 다른 이유 때문에 CLI 프로젝트로 변경해야 하는 상황이 발생할 수 있다. 이 경우 eject 명령어를 이용하면 해결 할 수 있다. 실행하면 Expo 프로젝트가 감추고 있던 것들이 드러나며, 리액트 네이티브 CLI 프로젝트로 시작한 것처럼 프로젝트가 변경되고 Expo 프로젝트에 있던 제약이 없어지지만 다시 Expo 프로젝트로 돌아올 수 없다.
