# Row

### Inheritance

Object > DiagnosticableTree > Widget > RenderObjectWidget > MultiChildRenderObjectWidget > Flex > Row

---

### Description

여러 위젯들을 children 으로 하여, 수평(가로) 방향으로 나열하고 싶을 경우 사용합니다.

여러 자식중 몇몇의 자식들이 수평방향의 남는 공간을 다 차지하도록 설정하고 싶은 경우에 Expanded widget을 통하여 그 자식을 감싸주면 됩니다.<br>
자식의 높이가 Row 위젯의 width를 넘어선다면, 오버플로우 오류를 발생시킵니다. 그러한 경우에 Expanded를 통해서 너는 내 안에서 최대한 가질 수 있는 너비정도만 가져! 라고 할 수 있습니다.

Row 위젯은 위에서 기술한것과 같이 수평으로 자식을 정렬하지만, 수직으로 정렬하고 싶은경우 Column 위젯을 살펴보면 됩니다.

Row 위젯은 위에서 기술한것과 여러 위젯들을 나열할 수 있기 때문에 children 이라는 속성이 있습니다. MultiChildRenderObjectWidget을 상속받은것을 확인하면 또한 그렇습니다. 만약 하나의 자식을 화면 내에서 정렬하고 싶은 경우에는 Align혹은 Center 위젯을 사용하면 화면내에 특정 부분에 자식을 위치시킬 수 있습니다.

Row 위젯 내부에서 주축(main-axis)는 가로 방향이고, 서브축(cross-axis)은 세로 방향입니다. 당연히 Column 위젯은 이 반대입니다.

웹 개발에서의 Flex의 direction을 Row으로 한 뒤, flex-diretion을 설정하지 않았다면, default 로 가로방향이 주축이 됩니다. 이와 비슷한 양상을 띄고 있습니다.

---

### Example

![image](https://user-images.githubusercontent.com/69495129/194708584-4017e263-df55-4fe5-8659-165e244443b1.png)

```dart
Row(
        children: const <Widget>[
          Text('hello Im chanhyuk'),
          Text('26 years old'),
          Text('thanks for reading this md file'),
        ],
      )
```

예제는 여러 Text라는 위젯들을 가로로 위치시키고 싶었기 때문에 Row 위젯을 사용하였습니다.

---

![image](https://user-images.githubusercontent.com/69495129/194708660-54900af9-181a-469a-a7cc-e47f59042ba4.png)

```dart
Row(
        children: <Widget>[
          Container(
            color: Colors.red,
            width: 100,
            height: 50,
          ),
          Container(
            color: Colors.blue,
            width: 100,
            height: 30,
          ),
          Container(
            color: Colors.green,
            width: 100,
            height: 100,
          ),
        ],
      )
```

위와같이 서브축인 세로를 기준으로 가운데 정렬되어있습니다. 모두 세로축의 시작점을 맞추고 싶다면(시작위치를 위에서부터 같게하고싶다면)<br>
서브축을 컨트롤하기 때문에 CrossAxisAlignment 를 컨트롤해주면서 해결할 수 있습니다.

![image](https://user-images.githubusercontent.com/69495129/194708703-2c4bc314-5b4b-4bc8-a305-888dca435280.png)

```dart
Row(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          Container(
            color: Colors.red,
            width: 100,
            height: 50,
          ),
          Container(
            color: Colors.blue,
            width: 100,
            height: 30,
          ),
          Container(
            color: Colors.green,
            width: 100,
            height: 100,
          ),
        ],
      )
```

위 사실을 미뤄보았을때 crossAxisAlignment 의 기본값은 `CrossAxisAlignment.center` 입니다.

---

### Troubleshooting

**자식의 너비가 정해져 있지 않은 경우**

Row의 자식들 중 ListView 같은 위젯이 있고, 그 위젯의 정확한 너비가 지정되지 않아있다면 런타임 오류를 발생시킵니다.

```dart
Row(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          const Text('hello Im chanhyuk'),
          const Text('26 years old'),
          const Text('thanks for reading this md file'),
          ListView(
            children: [
              const Text('hello Im chanhyuk'),
              const Text('26 years old'),
              const Text('thanks for reading this md file'),
            ],
          )
        ],
      )
```

위 처럼 코드를 작성하게 되면 다음과 같은 오류를 발생시킵니다.

![image](https://user-images.githubusercontent.com/69495129/194704581-503b7672-6e29-4f7d-837e-00157c2bacba.png)

이는 ListView의 너비가 지정되어있지 않기 때문입니다. 위에서도 기술한 것과 같이 Row위젯은 자식의 높이를 제약하지 않습니다<br>
그러므로 ListView를 Expanded, Flexible과 같은 위젯으로 감싸준다면, Row의 나머지 영역만을 차지해! 라는 구문이 되므로 오류를 발생시키지 않습니다.

---

### Primary properties

- `children` => List<Widget>?

Row의 자식들을 나타냅니다. 이 리스트들은 수평으로 위치하게 됩니다.

- `crossAxisAlignment` => CrossAxisAlignment

Row의 서브축(세로방향)의 정렬을 나타냅니다. 위 아래 방향으로 어디에 요소를 붙힐지 정할 수 있습니다. 또한 다양한 선택사항도 존재합니다.

- `direction` => Axis

  이 속성은 공식문서에는 나와있지만, Row이 상속하고 있는 Flex에 사용되는 속성이다.
  Row의 구현체를 살펴보면 따로 축정렬은 할 수 없고 고정값으로 밖혀있다.
  이는 어쩌면 당연한 논리이다, Row의 축은 수평인것이 자명하기 때문이다. Column은 수직인것이 자명하기 때문이다. 이 속성이 왜 플러터 공식문서의 Row 속성에 있는지 궁금하다. 결론은 Row위젯 내에서 direction은 지정해줄 수 없다.

![image](https://user-images.githubusercontent.com/69495129/194704918-84baa573-dfe0-4238-b6a1-a4d73820f56b.png)

- `mainAxisAlignment` => MainAxisAlignment

Row의 자식들을 어떻게 수평축으로 정렬을 시킬지 정하는 옵션입니다.
처음부터 정렬하게 할지 중간으로 둘지 마지막으로 밀어버릴지, 약간의 간격을 두고 정렬할지 등 여러가지 옵션이 존재합니다. 자주 사용되므로 중요한 속성입니다.

- `textDirection` => TextDirection

Row의 자식들중에 Text 위젯이 있고 어떠한 글자가 쓰여져있다면, 그 글자의 시작을 왼쪽부터 할것인지 오른쪽부터 할것인지를 정할 수 있습니다. 아랍어와 같은 경우 글자를 오른쪽 부터 읽는 경우도 있다고 생각하면 이해하기 수월합니다.

- `verticalDirection` => VerticalDirection

Row은 일반적으로 주축의 방향으로 확장해서 자리를 차지합니다. <br>
이 속성은 기본값이 `VerticalDirection.down` 입니다. 즉 위에서 아래로 자식들을 정렬하겠다는 것입니다. 하지만 자식들을 아래서부터 위로 정렬하고 싶은 경우가 있습니다. 그때 이 값을 사용할 수 있습니다.

---

`최종 수정일 : 22/10/08`
