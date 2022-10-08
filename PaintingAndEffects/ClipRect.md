# ClipRect

### Inheritance

Object > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > ClipRect

---

### Description

자식을 네모형태의 바운드 안에 가두고 싶을 경우 사용할 수 있습니다.<br>
200pixel 의 정사각형 이미지가 자식으로 있을 경우에 우측 하단 50pixel x 50pixel 의 이미지만 보여주고 싶은경우 사용할 수 있습니다.

주로 하기와 같은 위젯을 child 로 사용하는 경우가 많습니다.<br>
저는 개인적으로 Align과 Child위젯을 ClipRect의 child 위젯으로 많이 사용한 경험이 있습니다.

- CustomPaint
- CustomSingleChildLayout
- CustomMultiChildLayout
- Align
- Center
- OverflowBox
- SizedOverfloxBox

### Example

```dart
ClipRect(
          child: Align(
            // heightFactor: 0.5,
            // widthFactor: 0.5,
            child: Image.network("https://picsum.photos/400"),
          ),
        )
```

![image](https://user-images.githubusercontent.com/69495129/194711144-de557662-d01f-4dc8-949d-62f2e733dc99.png)

```dart
ClipRect(
          child: Align(
             heightFactor: 0.5,
             widthFactor: 0.5,
            child: Image.network("https://picsum.photos/400"),
          ),
        )
```

![image](https://user-images.githubusercontent.com/69495129/194711205-255baf29-2b2c-4e8e-b77b-c6ae8bf89384.png)

위 두 이미지를 비교해보면 크게만 보이던 첫 사진과 달리,
아래의 사진은 가로 기준 0.5배 세로 기준 0.5 배 각각 작아진 모습을 띄고 있습니다.
이는 ClipRect 위젯을 이용하여 이미지를 잘라냈기 떄문입니다.

---

```dart
class MyHomePage extends StatelessWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text("chanhyuk"),
        ),
        body: ClipRect(
          clipper: MyClipper(),
          child: Container(
            width: 3000,
            height: 3000,
            color: Colors.red,
          ),
        ));
  }
}

class MyClipper extends CustomClipper<Rect> {
  @override
  Rect getClip(Size size) {
    return const Rect.fromLTWH(30, 30, 80, 80);
  }

  @override
  bool shouldReclip(covariant CustomClipper<Rect> oldClipper) {
    return false;
  }
}

```

![image](https://user-images.githubusercontent.com/69495129/194711649-a2177646-b35d-42e6-912b-7a05e054b0fc.png)

위와 같은 방법으로 커스터마이징도 할 수 있습니다. <br>
왼쪽으로 부터 어느정도 위에서부터 어느정도 떨어진위치에서 시작하여 어느정도 너비 높이로 잘라내라라고 할 수도 있습니다.

---

### Primary properties

- `child` => Widget?

자식으로 사용될 위젯을 명시해줍니다.

- `clipper` => CustomClipper<Rect>?

나만의 커스텀 클리퍼 클래스입니다. 어떠한 방식으로 클립을 진행할지 등 여러가지를 커스터마이징 할 수 있습니다.

---

`최종 수정일 : 22/10/08`
