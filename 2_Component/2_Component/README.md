# Component

컴포넌트란 재사용이 가능한 조립 블록으로 화면에 나타나는 UI 요소이다.
컴포넌트는 단순히 UI 역할만 하는 것이 아니라 부모로부터 받은 속성(props)이나 자신의 상태(state)에 따라 표현이 달라지고 다양한 기능을 수행한다. 리액트 네이티브는 데이터와 UI 요소의 집합체라고 할 수 있는 컴포너늩를 이용하여 화면을 구성하게 된다.

## 목차

### 1. 내장 컴포넌트

리액트 네이티브에서는 다양한 내장 컴포넌트(Core Components)들이 제공된다.
 · 리액트 네이티브 컴포넌트 문서 : https://reactnative.dev/docs/components-and-apis
 
 ### Button 컴포넌트를 사용한 예제
 · 버튼 컴포넌트 문서 : https://reactnative.dev/docs/button

 `Button` 컴포넌트의 문서를 확인해보면 설명과 사용 예제가 있다. 그리고 설정할 수 있는 속성들의 목록과 각 속성들의 설명을 볼 수 있다. 다른 컴포넌트들에도 이와 같이 자세한 예제와 설정 가능한 속성에 대한 성명이 있으므로 컴포넌트 사용 시 참고하면 많은 도움이 될 것이다.

```
import React from 'react';
import {View, Text, Button} from 'react-native';

const App = function() {
    return (
        <View
            style={
                {
                    flex: 1,
                    backgroundColor: '#fff',
                    alignItems: 'center',
                    justifyContent: 'center',
                }
            }
        >
            <Text 
                style={
                    {
                        fontSize: 30,
                        marginBottom: 10
                    }
                }
            >
                Button Component
            </Text>
            <Button 
                title="Button" 
                onPress={
                    function() {
                        alert('Click Btn!!')
                    }
                }
            />
        </View>
    );
};


export default App;
```

버튼에 출력될 텍스트는 `title` 속성을 이용해서 `Button`이라고 지정했고, 버튼을 클릭했을 때 'Click Btn!!'이라는 확인 창이 나타나도록 `onPress` 속성에 함수를 지정했다.

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/383de594-2e1e-472d-9061-e1bbb90cc526)

이때 안드로이드와 iOS에서 확인한 Button 컴포넌트의 모습이 다른것을 확인할 수 있다.

`Button` 컴포넌트 문서에서 `color` 속성을 확인해보면 원인을 알 수 있다.
 · `Button` 컴포넌트 color 속성 : https://reactnative.dev/docs/button#color

`Button` 컴포넌트의 `color` 속성은, iOS에서는 텍스트 색을 나타내는 값이지만 안드로이드에서는 버튼의 바탕색을 나타내는 값이다. 이렇게 iOS와 안드로이드가 약간씩 다르게 표현되거나 특정 폴랫폼에만 적용되는 속성이 있다. 이러부분은 문서로 확인할 수 있지만 모든 컴포넌트의 속성을 외우고 사용할 수는 없으며, 컴포넌트를 사용할 때 미처 확인하지 못하고 지나칠 수도 있다. 

따라서 한 플랫폼만 테스트하는 것이 아니라 iOS와 안드로이드 모두 확인하면서 개발하는 습관을 들이는 것이 중요하다.

### 2. 커스텀 컴포넌트

앞에서 사용한 `Button` 컴포넌트는 iOS와 안드로이드에서 다른 모습으로 렌더링된다는 단점이 있었다. 
그 단점을 보완하기 위해 `TouchableOpacity` 컴포넌트와 `Text` 컴포넌트를 이용해서 `Button` 컴포넌트를 대체할 `MyButton` 컴포넌트 구현

#### MyButton.js
```
// 리액트를 불러와서 사용할 수 있게 해준다. 
// JSX는 React.createElement를 호출하는 코드로 컴파일되므로 컴포넌트를 작성할 때 반드시 작성해야 하는 코드다.
import React from 'react';

// 리액트 네이티브에서 제공하는 TouchableOpacity 컴포넌트와 Text 컴포넌트를 추가했다.
import { TouchableOpacity, Text } from 'react-native';

const MyButton = function() {
    return (
        // TouchableOpacity 컴포넌트를 사용해서 클릭에 대해 상호 작용할 수 있도록 했다.
        <TouchableOpacity
            style={
                {
                    backgroundColor: '#3498db',
                    padding: 16,
                    margin: 10,
                    borderRadius: 8,
                }
            }
            onPress={
                function() {
                    alert('Click !!!')
                }
            }
        >
            <Text 
                style={
                    {
                        color: 'white',
                        fontSize: 24
                    }
                }
            >
                My Button
            </Text>
        </TouchableOpacity>
    );
};

export default MyButton;
```

#### app.js
```
import React from 'react';
import {View, Text} from 'react-native';
import MyButton from './src/components/MyButton';

const App = function() {
    return (
        <View
            style={
                {
                    flex: 1,
                    backgroundColor: '#fff',
                    alignItems: 'center',
                    justifyContent: 'center',
                }
            }
        >
            <Text
                style={
                    {
                        fontSize: 30,
                        marginBottom: 10,
                    }
                }
            >
                My Button Component
            </Text>
            <MyButton /> 
        </View>
    );
};

export default App;
```

#### Result

![image](https://github.com/iJaeDragon/React-Native/assets/66985977/88a85da5-6ce4-4187-8dd3-63e6075579ea)

### 3. props와 state

`props`와 `state`는 컴포넌트가 UI뿐만 아니라 당야한 기능을 담당할 수 있도록 하여 더욱 다양한 역할을 수행할 수 있도록 해준다.

`props`란 properties를 줄인 표현으로, 부모 컴포넌트로부터 전달된 속성값 혹은 상속받은 속성값을 말한다. 부모 컴포넌트가 자식 컴포넌트의 `props`를 설정하면 자식 컴포넌트에서는 해당 `props`를 사용할 수 있지만 변경하는 것은 불가능하다.

`props`의 변경이 필요할 경우 `props`를 설정 및 전달한 부모컴포넌트에서 변경해야 한다.

#### props 전달하고 사용하기

##### 전달
```
···
<MyButton title="test" />
···
```


##### 확인

```
···
const MyButton = function(props) {
    console.log(props);
    return null;
}
···
```


##### 결과

```
{"title": "test"}
```


##### 방법1. 전달받은 props를 활용하여 버튼 텍스트 설정
```
···
const MyButton = function(props) {
    return (
        <TouchableOpacity
            ···
        >
            <Text 
                style={
                    {
                        color: 'white',
                        fontSize: 24
                    }
                }
            >
                {props.title}
            </Text>
        </TouchableOpacity>
    );
};
···
```


##### 방법2. children을 이용하여 태그 사이에 있는 값으로 버튼 텍스트 설정

```
<MyButton title="title Text">Child Text</MyButton>
```

```
···
const MyButton = function(props) {
    return (
        <TouchableOpacity
           ···
        >
            <Text 
                style={
                    {
                        color: 'white',
                        fontSize: 24
                    }
                }
            >
                {props.children || props.title}
            </Text>
        </TouchableOpacity>
    );
};
···
```

`props`에 `children`이 있다면 `title`보다 우선시 되도록 작성됐다.


#### defaultProps

여러 사람과 함께 개발하다 보면 내가 만든 컴포넌트를 다른 사람이 사용하는 경우가 많다. 이런 상황에서 컴포넌트를 잘못 파악해 반드시 전달되어야 하는 중요한 값이 전달되지 않았을 때 사용할 기본값을 `defaultProps`로 지정하면 만약의 사태에 빈 값이 나타나는 상황을 방지할 수 있다.

```
···
<MyButton />
···
```

```
···
const MyButton = function(props) {
    ···
};

MyButton.defaultProps = {
    title: 'Button',
};
···
```


`title` 속성을 지정하지 않았을때 기본적으로 'Button'으로 지정되도록 설정하였다.


#### propTypes
프로젝트의 크기가 커지면서 컴포넌트에 `props`를 전달할 때 잘못된 타입을 전달하거나, 필수로 전달해야 하는 값을 전달하지 않아서 문제가 생길 수 있다. 이런 상황에서 잘못된 `props`가 전달되었다는 것을 경고 메시지를 통해 알리는 방법으로 `PropTypes`를 사용하는 방법이 있다.

`PropTypes`를 사용하려면 `prop-type` 라이브러리를 추가로 설치해야 한다.

```
npm install prop-types
```


```
import React from 'react';
import PropTypes from 'prop-types'

import { TouchableOpacity, Text } from 'react-native';

const MyButton = function(props) {
    return (
        <TouchableOpacity
           ···
        >
            <Text 
                ···
            >
                {props.title}
            </Text>
        </TouchableOpacity>
    );
};

MyButton.propTypes = {
    title: PropTypes.number,
}
···
```

`title` 속성에는 타입이 숫자(number)여야 한다고 지정했다.
만약 문자열(string)로 넘어오면 아래처럼 에러가 발생한다.

```
 ERROR  Warning: Failed prop type: Invalid prop `title` of type `string` supplied to `MyButton`, expected `number`.
```


필수 여부를 지정하기 위해서는 선언한 타입 뒤에 `isRequired`만 붙여주면 된다.

```
···
MyButton.propTypes = {
    title: PropTypes.number.isRequired,
}
···
```

필수 요소를 설정하지 않는다면 다음과 같은 에러가 발생한다.

```
Warning: Failed prop type: The prop `title` is marked as required in `MyButton`, but its value is `undefined`.
```

`PropTypes`에는 문자열이나 숫자 외에도 함수(func), 객체(object), 배열(array) 등의 다양한 타입을 지정할 수 있다.

##### 함수 전달

```
···
const App = function() {
    return (
        <View
            ···
        >
            ···
            <MyButton 
                title="Button" 
                onPress={
                    function() {
                        alert("Button Click!!")
                    }
                }
            />
        </View>
    );
};
···
```

```
···
const MyButton = function(props) {
    return (
        <TouchableOpacity
            style={
                ···
            }
            onPress={
                function() {
                    props.onPress()
                }
            }
        >
            <Text 
                ···
            >
                {props.title}
            </Text>
        </TouchableOpacity>
    );
};
···
```