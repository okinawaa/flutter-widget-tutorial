# AppBar

### Inheritance

Object > DiagnosticableTree > Widget > StatefulWidget > AppBar

### Description

Material Design의 형태를 띄고 있는 AppBar 입니다.

AppBar는 여러가지 toolbar 위젯들을 사용할 수 있습니다.\
leading, title, actions 들을 사용할 수 있습니다.\
이들을 사용해 AppBar내에 특정위치에 타 위젯들을 위치시킬 수 있습니다.\
다양한 애플리케이션에서 공통적으로 사용됩니다.

비개발자분들에게는 앱 내의 상단바 라고 이해되고 있습니다.

<img width="445" alt="image" src="https://user-images.githubusercontent.com/69495129/194686531-0d1bb2d5-9144-4db1-8928-ab11b3761a5b.png">

출처: 구글 플러터 공식문서

`위 이미지를 보고 bottom 속성은 앱 최하단의 위치할 위젯이라고 착각했습니다. AppBar 내부에서 하단쪽에 위치할 위젯을 명시해주는 속성입니다.`

### Example

<img width="378" alt="image" src="https://user-images.githubusercontent.com/69495129/194686595-9116711f-32a1-476b-9fc2-7ede4f9a46bb.png">

```dart
 AppBar(
        title: const Text('AppBar Demo'),
        actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.add_alert),
            tooltip: 'Show Snackbar',
            onPressed: () {
              ScaffoldMessenger.of(context).showSnackBar(
                  const SnackBar(content: Text('This is a snackbar')));
            },
          ),
          IconButton(
            icon: const Icon(Icons.navigate_next),
            tooltip: 'Go to the next page',
            onPressed: () {
              Navigator.push(context, MaterialPageRoute<void>(
                builder: (BuildContext context) {
                  return Scaffold(
                    appBar: AppBar(
                      title: const Text('Next page'),
                    ),
                    body: const Center(
                      child: Text(
                        'This is the next page',
                        style: TextStyle(fontSize: 24),
                      ),
                    ),
                  );
                },
              ));
            },
          ),
        ],
      ),
```

AppBar는 주로 Scafold 위젯에서 appBar 속성으로 사용됩니다. 위 예제처럼 title을 이용하여, AppBar내에 표시될 글자를 나타낼 수 있습니다.
actions 라는 속성을 사용하면, 위젯의 배열을 받을 수 있습니다. AppBar내의 우측에 나타낼 위젯들을 삽입할 수 있습니다. 현재는 IconButton들을 배열 형태로 받고 있기 때문에 우측에 종 이미지를 확인할 수 있습니다.

### Primary properties

- `actions` => List<Widget>?

앱 내의 title 속성 다음에 위치할 위젯들의 리스트를 명시합니다. 일반적으로 AppBar내의 우측에 나타낼 위젯들을 리스트업합니다. 주로 아이콘 요소들을 위치시킵니다.

- `actionsIconTheme` => IconThemeData?

actions 속성에 사용되는 아이콘들의 공통적인 테마 속성을 정의합니다. 색상, 투명도, 크기들을 이 속성을 이용하여 지정해줄 수 있습니다.

- `backgroundColor` => Color?

AppBar 의 배경 색상을 정의합니다.

- `bottom` => PreferredSizeWidget?

앱 스크린 내의 최하단에 위치할 위젯이 아닌, AppBar 내부에서도 아래 부분에 위치할 위젯을 명시합니다.

- `bottomOpacity` => double

bottom 속성에 위치하는 위젯들의 투명도를 설정할 수 있습니다.

- `centerTitle` => bool?

title 속성에 준 Widget을 AppBar내의 중간에 위치시킬지 말지를 결정합니다.

- `elevation` => double?

AppBar 가 떠있을 정도를 지정합니다. 하단에 생기는 그림자를 보시면 이해하기 쉽습니다. 0 값을주면 그림자가 사라지는것을 확인할 수 있습니다.

- `foregroundColor` => Color?

AppBar 내부에 존재하는 Text나, Icons 의 기본 색상입니다.

- `iconTheme` => IconThemeData?

AppBar내에 사용되는 아이콘들의 공통적인 테마 속성을 정의합니다. 색상, 투명도, 크기들을 이 속성을 이용하여 지정해줄 수 있습니다. \
actionsIconTheme과 적용 범위가 다릅니다.

- `leading` => Widget?

AppBar 내의 title 위젯의 쪽에 위치할 위젯입니다. AppBar를 이끈다! 라고 이해하면 기억하기 쉽습니다.

- `leadingWidth` => double?

leading에 사용되는 Widget의 너비를 지정할 수 있습니다.

- `preferredSize` => Size

AppBar에서 toolbarHeight 와 bottom 속성에 준 위젯의 합계의 높이를 선택합니다.

- `primary` => bool

AppBar가 스크린의 최상단에 위치시킬지를 결정하는 속성입니다. (z-index 개념입니다.)

- `shadowColor` => Color?

AppBar 하단의 그림자의 색상을 지정할 수 있습니다. (당연히 elevation이 0이라면 시각적으로 확인이 불가능합니다.)

- `shape` => ShapeBorder?

AppBar 의 형태를 변경할 수 있습니다. 둥글게 처리등 여러가지가 데코레이션이 가능합니다.

- `title` => Widget?

AppBar 의 제목을 작성할 수 있습니다. 텍스트가 될 수 있고 이미지가 될 수 있습니다. leading 과 actions의 사이에 위치합니다.

- `titleSpacing` => double?

수평축으로 title 위젯의 마진을 설정합니다. 0.0으로 설정한다면, 가능한 모든 공간을 title 위젯이 차지합니다.

- `titleTextStyle` => TextStyle?

AppBar의 title 위젯이 가질 기본 텍스트 스타일을 지정합니다. title에 Text위젯을 사용한다면, 거기서 style을 바로 지정할 수 있다고 이 속성이 불필요하다고 생각할 수 있습니다.\
하지만, title 내에서의 위젯이 children을 받는 위젯이고 그 안에 수많은 Text위젯이 있다면, 하나하나 스타일을 지정해주기 보다는 이 titleTextStyle을 통해서 일관되게 스타일링을 해줄 수 있습니다.

- `toolbarOpacity` => double

AppBar의 toolbar부분에 적용될 투명도를 설정해줍니다.

- `toolbarTextStyle` => TextStyle?

AppBar의 toolbar부분에 적용될 공통 스타일을 설정해줍니다.\
toolbar부분에는 leading, actions 위젯들이 포함됩니다.\
titleTextStyle 이 따로 있는것을 보고 아시겠지만, 이 속성은 title 위젯에는 영향을 주지 않습니다.

`최종 수정일 : 22/10/08`
