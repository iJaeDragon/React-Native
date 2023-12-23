# JSX

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/7a7402a9-11ff-44d0-aa82-988bf48e26b6)

자바스크립트 파일인데 HTML 코드가 포함되어 작성되어 있다.
이런 코드들을 JSX라고 부른다.

JSX는 객체 생성과 함수 호출을 위한 문법적 편의를 제공하기 위해 만들어진 확장 기능으로 리액트 프로젝트에서 사용된다.

JSX는 가독성이 높고 작성하기도 쉬울 뿐만 아니라, XML과 유사하다는 점에서 중첩된 구조를 잘 나타낼 수 있다는 장점이 있다.

## 목차

### [1. 하나의 부모](#1-하나의-부모)

### [2. 자바스크립트 변수](#2-자바스크립트-변수)

### [3. 자바스크립트 조건문](#3-자바스크립트-조건문)

### [4. null과 undefined](#4-null과-undefined)

### [5. 주석](#5-주석)

### [6. 스타일링](#6-스타일링)


## 1. 하나의 부모
```
···
const App = () => {
    return (
        <Text>Open up App.js to start working on your app!</Text>
        <StatusBar style="auto" />
    );
};
···
```

위 코드를 실행하면 아래 사진처럼 에러가 발생한다.

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/25927c5d-9347-4caf-bf1e-e7190261d721)

원인은 반횐되는 요소가 하나가 아니기 때문이다. JSX에서는 여러개의 교소를 반환하는 경우에는 아래 코드처럼 반드시 하나의 부모로 요소들을 감싸서 반환해야 한다.

```
···
const App = () => {
    return (
        <View style={styles.container}>
            <Text>Open up App.js to start working on your app!</Text>
            <StatusBar style="auto" />
        </View>
    );
};
···
```

이때 `View`는 UI를 구성하는 가장 기본적인 요소로 웹 프로그래밍에서는 `<div>`와 비슷한 역할을 하는 컴포넌트이다.

`View` 컴포넌트처럼 특정 역할을 하는 컴포넌트로 감싸지 않고 여러 개의 컴포넌트를 반환하고 싶은 경우 아래 코드 처럼 `Fragment` 컴포넌트를 사용한다.

```
···
const App = () => {
    return (
        <Fragment>
            <Text>Open up App.js to start working on your app!</Text>
            <StatusBar style="auto" />
        </Fragment>
    );
};
···
```

혹은 `Fragment` 컴포넌트의 단축 문법을 사용해도 된다.

```
···
const App = () => {
    return (
        <>
            <Text>Open up App.js to start working on your app!</Text>
            <StatusBar style="auto" />
        </>
    );
};
···
```

## 2. 자바스크립트 변수
JSX는 내부에서 자바스크립트의 변수를 전달하여 이용할 수 있다.

```
···
const App = () => {
    const name = "JaeDragon"
    return (
        <View style={styles.container}>
            <Text style={styles.text}>My name is {name}</Text>
            <StatusBar style="auto" />
        </View>
    );
};
···
```

위 코드처럼 선언한 변수를 대괄호를 묶어서 `{name}` 호출한다. 

## 3. 자바스크립트 조건문
JSX에서도 자바스크립트의 조건문을 이용하여 상황에 따라 다른 요소를 출력할 수 있다.
다만 제약이 약간 있기에 복잡한 조건인 경우 JSX 밖에서 조건에 따른 값을 설정하고 JSX 내에서 사용하는 조건문에서는 최대한 간단하게 작성하는 것이 코드를 조금 더 깔끔하게 작성할 수 있는 방법이다.

### if 조건문
JSX는 내부에서 if문을 사용할 수 있지만 if문을 즉시실행함수 형태로 작성해야 한다.
```
···
const App = function() {
    const name = 'JaeDragon'
    return (
        <View style={styles.container}>
            <Text style={styles.text}>
                {
                    (function() {
                        if(name == 'JaeDragon') {
                            return "His name is JaeDragon."
                        } else {
                            return "His name is not JaeDragon."
                        }
                    })()
                }
            </Text>
            <StatusBar style="auto" />
        </View>
    );
};
···
```

### 삼항 연산자

```
···
const App = function() {
    const name = 'JaeDragon'
    return (
        <View style={styles.container}>
            <Text style={styles.text}>
                    {name == 'JaeDragon' ? 'His name is JaeDragon.' : 'His name is not JaeDragon.'}
            </Text>
            <StatusBar style="auto" />
        </View>
    );
};
···
```

### AND 연산자와 OR 연산자

AND 연산자와 OR 연산자를 이용하면 특정 조건에 따라 컴포넌트의 렌더링 여부를 결정하도록 코드를 구성할 수 있다.

```
const App = function() {
    const name = 'JaeDragon'
    return (
        <View style={styles.container}>
            {name == "JaeDragon" && (
                <Text style={styles.text}>
                    His name is JaeDragon.
                </Text>
            )}
            {name != "JaeDragon" && (
                <Text style={styles.text}>
                    His name is not JaeDragon.
                </Text>
            )}
            <StatusBar style="auto" />
        </View>
    );
};
```

JSX에서 false는 렌더링되지 않기 때문에 AND 연산자 앞의 조건이 참일 때 뒤의 내용이 나타나고, 거짓인 경우 나타지 않는다.

OR 연산자는 AND 연산자와 반대로 앞의 조건이 거짓인 경우 내용이 나타나고, 조건이 참인 경우 나타나지 않는다.

## 4. null과 undefined

조건에 따라 출력하는 값을 변경하다 보면 컴포넌트가 null이나 undefined를 반환하는 경우가 있다. JSX의 경우 null은 허용하지만 undefined는 오류가 발생하기에 주의가 필요하다.

## 5. 주석

JSX에서의 주석은 자바스크립트에서의 주석과 약간 차이가 있다. JSX의 주석은 `/* */`를 이용하여 작성해야 한다. 단, 태그 안에서 주석을 사용할 때는 자바스크립트처럼 `//`나 `/* */` 주석을 사용할 수 있다.

```
const App = function() {
    /* const name = 'JaeDragon' */
    return (
        <View style={styles.container}>
            <Text 
                // style={styles.text}
                style={styles.text2}
            >
                안녕하세요
            </Text>
        </View>
    );
};
```

## 6. 스타일링

JSX에서는 HTML과 달리 style에 문자열로 입력하는 것이 아니라 객체 형태로 입력해야 한다.
또한 `background-color`처럼 하이픈으로 연결된 이름은 하이픈(-)을 제거하고 카멜 표기법(Camel case)으로 `backgroundColor`처럼 작성해야 한다.

```
const App = function() {
    return (
        <View 
            style={{
                flex: 1,
                justifyContent: 'center',
                alignItems: 'center',
                backgroundColor: '#ffffff',
            }}
        >
            <Text>안녕하세요</Text>
        </View>
    );
};
```