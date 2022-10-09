# AnimatedContainer

### Inheritance

Object > DiagnosticableTree > Widget > StatefulWidget > ImplicitlyAnimatedWidget > AnimatedContainer

### Description

이 위젯은 css처럼 하나하나 애니메이션의 형태를 지정해줘야하는것이 아닙니다.<br>
어떤 상태일때 어떠한 값을 가져라 Container야! 이런식으로 명령형으로 애니메이션을 구현할 수 있습니다.<br>
예를들어 토글버튼을 상상해보겠습니다. selected 라는 상태로 토글의 상태가 관리된다면 selected에 따라서 Container의 색상, 크기등, 그림자, 패딩, 정렬, 그래디언트 등 여러가지를 변화시켜줄 수 있습니다.<br>
Duration을 통해서 애니메이션이 작동할 시간을 정해준다면, 부드럽게 선형 보간법을 이용하여 사용자에게 좋은 UI를 선사해줄 수 있도록 도와주는 위젯입니다.

일반 Container 위젯에서 시간에 따라서 점진적으로 애니메이션을 할 수 있는 위젯입니다.

AnimatedContainer는 속성값으로 받은 curve와 duration값에 따라서 예전값과 새로운값 사이를 부드럽게 변화시켜줍니다.

AnimatedContainer는 간단한 변화를 구현할 수 있습니다. 조금더 복잡한 애니메이션을 구현하고 싶다면, 이 위젯이 상속하고 있는 AnimatedWidget을 살펴보시는걸 추천드립니다!

### Example

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/69495129/194749270-ba3665fa-7786-4ee3-b2a1-c9b0ead5dfd2.gif)

```dart
AnimatedContainer(
          width: selected ? 200.0 : 100.0,
          height: selected ? 100.0 : 200.0,
          color: selected ? Colors.red : Colors.blue,
          alignment:
              selected ? Alignment.center : AlignmentDirectional.topCenter,
          duration: const Duration(seconds: 2),
          curve: Curves.fastOutSlowIn,
          child: const FlutterLogo(size: 75),
        )
```

사용자가 클릭할때마다 selected 변수를 변화시켜주고, 그 변화된 값을 통해서 AnimatedContainer의 속성값을 동적으로 변화시켜줍니다.

### Primary Properties

- `alignment` => AlignmentGeometry?

컨테이너 내부에서 child를 어느 방향으로 정렬시킬지 정해줍니다.

- `child` => Widget?

컨테이너 내부에 child로 사용될 위젯을 정해줍니다.

- `clipBehavior` => Clip?

AnimatedContainer.decoration 이 null 이 아닌 경우에 child를 어떠한 방식으로 자를지 정합니다.

- `constraints` => BoxConstraints?

자식에게 **추가적인** 제약을 가합니다.<br>
중요한것은 **추가적인** 입니다. 부모가 일반적으로 가하는 제약에 이 속성의 제약까지 더한다는 것입니다.

- `decoration` => Decoration?

자식의 뒤에 데코레이션을 정해줄 수 있습니다.

- `duration` => Duration

애니메이션이 작동할 시간을 정해줍니다. 이 시간에 걸쳐서 선형 보간법이 적용된 애니메이션이 적용됩니다.

- `margin` => EdgeInsetsGeometry?

decoration과 child 주변에 마진값을 설정할 수 있습니다.

- `onEnd` => VoidCallback?

애니메이션이 끝날때 실행될 콜백함수를 선언합니다

- `padding` => EdgeInsetsGeometry?

decoration 내부에 패딩공간을 확보합니다. 그 안에 child가 위치합니다.

---

`최종 수정일 : 22/10/09`
