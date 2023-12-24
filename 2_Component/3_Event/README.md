# Event

리액트 네이티브는 사용자의 행동에 따라 상호 작용하는 이벤트를 다양하게 제공한다. 정말 많은 이벤트가 있으며 컴포넌트가 하는 역할에 따라 제공되는 이벤트도 약간씩 차이가 있다.

## 목차

### [1. Press Event](#1-press-event)

### [2. Change Event](#)

### [3. Pressable Event](#)


## 1. Press Event

웹 프로그래밍에서 가장 많이 사용하는 이벤트 중 하나는 사용자가 특정 `DOM`을 클릭했을 때 호출되는 `onClick` 이벤트 일 것이다. 리액트 네이티브에서 `onClick` 이벤트와 가장 비슷한 이벤트는 `press` 이벤트이다. 

버튼을 만들 때 사용하는 `TouchableOpacity` 컴포넌트에서 설정할 수 있는 `Press` 이벤트의 종류는 총 4가지다.

* onPressIn : 터치가 시작될 때 항상 호출
* onPressOut : 터치가 해제될 때 항상 호출
* onPress : 터치가 해제될 때 onPressOut 이후 호출
* onLongPress : 터치가 일정 시간 이상 지속되면 호출

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/d4c0cacb-f282-4445-9675-b9b21ea5df1c)

### EventButton.js

```
import React from 'react';
import { TouchableOpacity, Text } from 'react-native';

const EventButton = function() {
    // 이벤트 동작 정의
    const _onPressIn = function() {
        console.log('Press In !!!\n')
    }
    const _onPressOut = function() {
        console.log('onPressOut !!!\n')
    }
    const _onPress = function() {
        console.log('onPress !!!\n')
    }
    const _onLongPress = function() {
        console.log('onLongPress !!!\n')
    }

    return (
        <TouchableOpacity
            style={
                {
                    backgroundColor: '#f1c40f',
                    padding: 16,
                    margin: 10,
                    borderRadius: 8
                }
            }
            // 이벤트 감지 시 동작 등록
            onPressIn={_onPressIn}

            // 버튼을 3초 이상 눌렀을 경우에 onLongPress 이벤트가 동작하도록
            delayLongPress={3000}
            onLongPress={_onLongPress}
            onPressOut={_onPressOut}
            onPress={_onPress}
        >
            <Text style={
                {
                    color: 'white',
                    fontSize: 24
                }  
            }
            >
                Press
            </Text>
        </TouchableOpacity>
    )
}

export default EventButton;
```

### App.js
```
···
import EventButton from './src/components/EventButton';

const App = function() {
    return (
        <View
            ···
        >
            <EventButton />
        </View>
    );
};
···
```

## 2. Change Event

변화를 감지하는 `change` 이벤트는 값을 입력하는 `TextInput` 컴포넌트에서 많이 사용된다. 


### TextInput.js

```
import React, {useState} from "react";
import {View, Text, TextInput} from 'react-native';

const EventInput = function() {
    const [text, setText] = useState('');

    const _onChage = function(event) {
        setText(event.nativeEvent.text);
    }

    return (
        <View>
            <Text 
                style={
                    {
                        margin: 10,
                        fontSize: 30
                    }
                }
            >
                text: {text}
            </Text>
            <TextInput
                style={
                    {
                        borderWidth: 1,
                        padding: 10,
                        fontSize: 20
                    }
                }
                placeholder="Enter a Text..."
                onChange={_onChage}
            />
        </View>
    )
}

export default EventInput;
```

`TextInput`에 데이터를 입력하면 `Text`에 동일한 데이터가 출력되도록 코드를 구성했다.

### App.js

```
···
import TextInput from './src/components/TextInput'

const App = function() {
    return (
        <View
            ···
        >
            <TextInput />
        </View>
    );
};
···
```

`TextInput` 컴포넌트에 있는 `onChange` 속성은 `TextInput` 컴포넌트에 입력된 텍스트가 변경될 때 호출된다. 그리고 호출되는 함수에 다음과 같은 형태로 인자를 전달한다.

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/db1ea910-3804-453c-9443-bfd975f04a04)

```
···
const EventInput = function() {
    const [text, setText] = useState('');

    const _onChageText = function(text) {
        setText(text)
    }

    return (
        <View>
            <Text 
                ···
            >
                text: {text}
            </Text>
            <TextInput
                ···
                onChangeText={_onChageText}
            />
        </View>
    )
}
···
```

`onChage`를 통해 전달되는 내용 중 변회된 텍스트만 필요한 상황이라면
`onChageText`를 사용해서 더 깔끔하게 사용할 수 있다. `onChageText`는 컴포넌트의 텍스트가 변경됐을 때 변경된 텍스트의 문자열만 인수로 전달하며 호출된다.

## Pressable 컴포넌트

리액트 네이티브 0.63 버전부터 기존의 `TouchableOpacity` 컴포넌트를 대체하는 `Pressable` 컴포넌트가 추가되었다. 기존의 컴포넌트보다 더 다양한 기능을 제공하므로 리액트 네이티브 0.63 버전 이상을 사용해서 `Pressable` 컴포넌트를 사용할 수 있다면 `TouchableOpacity` 컴포넌트 대신 `Pressable` 컴포넌트 사용을 권장된다.

`Pressable` 컴포넌트는 `TouchableOpacity` 컴포넌트처럼 사용자의 터치에 상호 작용하는 컴포넌트이다. `press` 이벤트도 동일하게 존재하고 동작 방식도 같다. `Pressable` 컴포넌트에서 지원하는 기능 중 기존의 컴포넌트들과 다른 특징은 `HitRect`와 `PressRect`이다.

우리는 모바일이라는 작은 화면에서 버튼을 포함하여 다양한 요소들을 보여준다. 화면이 작은 만큼 버튼도 작아는데, 사람마다 손의 크기나 두께가 모두 다르기 때문에 누군가는 버튼을 정확하게 클릭하는 것 자체가 어려울 수 있다. 이런 상황을 해결하기 위해 많은 개발자들이 버튼 모양보다 약간 떨어진 부분까지 이벤트가 발생할 수 있도록 조치하고 있다. `Pressable` 컴포넌트에서는 `HitRect`를 이용해 이 설정을 쉽게 할 수 있다.

누구나 한번쯤 버튼을 클릭했을 때 해당 버튼이 동작하지 않게 하기 위해 버튼을 누른 상태에서 손가락을 이동시킨 경험이 있을 것이다. 그렇다면 얼마나 멀어져야 버튼을 누른 상태에서 벗어났다고 판할 수 있을까? `Pressable` 컴포넌트에서는 이 부분도 개발자가 조절하기 편하도록 `PressRect` 기능을 지원한다.

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/0892e9aa-dc99-45bd-8fb3-0c7bcfade6d7)


### PressableBtn.js

```
import React from "react";
import {View, Text, Pressable} from 'react-native';

const PressableBtn = function(props) {
    return (
        <Pressable
            style={
                {
                    padding: 10, backgroundColor: '#1abc9c'
                }
            }
            onPressIn={
                function() {
                    console.log('Press In')
                }
            }
            onPressOut={
                function() {
                    console.log('Press Out')
                }
            }
            onPress={
                function() {
                    console.log('Press')
                }
            }
            delayLongPress={3000}
            onLongPress={
                function() {
                    console.log('Long Press')
                }
            }

            // 터치를 cancle 시키기 위해 빠져 나가야할 범위
            pressRetentionOffset={
                {
                    bottom: 50,
                    left: 50,
                    right: 50,
                    top: 50
                }
            }

            // 버튼 주변 터치시 버튼 터치로 인정할 범위
            hitSlop={50}
        >
            <Text style={
                {
                    padding: 10,
                    fontSize: 30
                }
            }
            >
                {props.title}
            </Text>
        </Pressable>
    )
}

export default PressableBtn;
```

### App.js

```
···
import PressableBtn from './src/components/PressableBtn';

const App = function() {
    return (
        <View
            ···
        >
            <PressableBtn title="Pressable" />
        </View>
    );
};

export default App;
```