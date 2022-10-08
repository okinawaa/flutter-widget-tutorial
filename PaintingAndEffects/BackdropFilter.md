# BackdropFilter

### Inheritance

Object > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > BackdropFilter

---

### Description

기존에 그려진 된 부분에 필터를 적용한 뒤에! 나의 자식을 그리는 위젯입니다<br>
필터는 상위 또는 상위 위젯의 클립 내의 모든 영역에 적용됩니다. 클립이 없으면 필터가 전체 화면에 적용되기 때문에 내가 원하는 영역만 클립으로 설정해주는 것이 중요합니다.

이미지들을 블러로 처리해줄 수도 있습니다. 또한 각도나 4차원각도도 조절해줄 수 있습니다.

쉽게 생각하면 나의 child를 블러처리하는것이 아니라, 나의 child를 이용하여 뒷 배경을 블러처리해줄 수 있는 것입니다.

---

### Example

![image](https://user-images.githubusercontent.com/69495129/194709840-896a7301-434b-4930-8d59-fd72d8a7e49d.png)

```dart
Stack(
          children: <Widget>[
            Text('0' * 10000),
            Center(
              child: ClipRect(
                // <-- clips to the 200x200 [Container] below
                child: BackdropFilter(
                  filter: ImageFilter.blur(
                    sigmaX: 5.0,
                    sigmaY: 5.0,
                  ),
                  child: Container(
                    alignment: Alignment.center,
                    width: 200.0,
                    height: 200.0,
                    child: const Text('Hello World'),
                  ),
                ),
              ),
            ),
          ],
        )
```

위와 같이 Hello World라는 글자부분은 블러처리가 되어있지않습니다. 뒤 배경에 이미 Text로 글자가 쓰여져 있고,
그 부분을 200x200 블러처리 하기위해서 BackdropFilter를 사용해줬습니다.

---

> BackdropFilter는 너무나 많은 효과를 낼 수 있습니다. 그러므로 상대적으로 플러터에서 비싼 연산을 사용합니다.
> 단순히 하나의 위젯만 필터를 적용하고 싶다면 ImageFiltered라는 위젯을 사용하는것이 연산에서 더 좋습니다. 더 가볍습니다.
> ImageFiltered는 자신의 child위젯 자체를 블러처리하므로 더 직관적이여서 저는 더 선호합니다.

---

### Primary properties

- `child` => Widget?

뒷 배경을 블러로 처리하면서 내가 보이게끔 하고 싶은 위젯을 설정해줄 수 있는 속성입니다.

- `filter` => ImageFilter

필터를 어떠한 방식으로 진행할지 명시해주는 속성입니다. 매우 다양한 옵션들이 있습니다.

---

`최종 수정일 : 22/10/08`
