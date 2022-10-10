# AnimatedList

### Inheritance

Object > DiagnosticableTree > Widget > StatefulWidget > AnimatedList

---

### Description

모바일 서비스를 기획하다보면, 리스트 형태의 퍼블리싱을 할 기회가 많습니다. 물론 그 리스트들이 추가, 수정, 삭제 등 여러가지 동적인 액션도 취하곤 합니다.<br>
리스트가 추가, 삭제 될때마다 새로운 컴포넌트가 뚝 뚝 하고 추가되거나 삭제된다면 사용자의 경험은 과연 어떨까요?<br>
저라면 왜 내 애플리케이션은 뚝 뚝 끊기지? 부드럽지 않고 렉걸리는것 같아. 라고 생각할 것 같습니다<br>
물론 난잡하고 조잡한 애니메이션은 좋지 않지만 사용자가 이질감을 들지 않게 하기 위한 애니메이션은 선택이 아닌 필수라고 생각합니다.<br>
그것을 도와주기 위한 위젯이 `AnimatedList` 입니다.

이 위젯은 다른 위젯들과는 달리 사용법이 꽤나 복잡합니다. 리스트에 아이템이 추가될 때, 삭제될 때 애니메이션을 지정해줘야하기 떄문이죠, 다른 위젯처럼 속성에 값만 집어넣어서는 원하는데로 작동을 하지 않습니다! 이론적인 설명보다는 예제를 이용하여 설명하겠습니다.

---

### Example

주석을 상세하게 남겨두겠습니다.
주석을 따라가며 이 코드를 이해한다면 AnimatedList를 언제든 이용하실 수 있습니다.

---

![ezgif com-gif-maker (3)](https://user-images.githubusercontent.com/69495129/194873565-e5e94da0-f3e6-4fd3-b954-c923db212c09.gif)

---

```dart

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  static const String _title = 'Flutter Code Sample';

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: _title,
      home: MyStatefulWidget(),
    );
  }
}

class MyStatefulWidget extends StatefulWidget {
  const MyStatefulWidget({super.key});

  @override
  State<MyStatefulWidget> createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  // AnimatedList가 같고 있는 현재의 상태를 참조하기 위해 키를 선언합니다.
  final listKey = GlobalKey<AnimatedListState>();
  // listItems는 제가 정의한, 색상과 색상명을 갖고있는 리스트입니다. 불변을 지키기 위하여 List.from을 사용합니다.
  final List<ListItem> items = List.from(listItems);
  @override
  Widget build(BuildContext context) => Scaffold(
        appBar: AppBar(
          title: const Text("chanhyuk"),
        ),
        body: AnimatedList(
          // 위에서 선언한 키를 이 AnimatedList와 연동시켜줍니다.
          key: listKey,
          initialItemCount: items.length,
          /*
           ListItemWidget은 제가 정의한 하나의 Row card입니다.
           SizeTransition 위젯으로 감싸져있으며 그 안에 animation속성에
           여기서 넘겨준 animation 값을 주입하고 있습니다.
           그렇게 함으로써 사이즈가 변동될 때 애니메이션 효과가 일어납니다.
          */
          itemBuilder: ((context, index, animation) => ListItemWidget(
              item: items[index],
              animation: animation,

              /*
              ListItemWidget내부에서 우측 휴지통 아이콘을 클릭하면 리스트아이템이 삭제가 됩니다.
              그것을 핸들링 하기 위해서 위에서 이벤트 핸들러를 넘겨줍니다.
              */
              onClicked: () {
                removeItem(index);
              })),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: insertItem,
          child: const Icon(Icons.add),
        ),
      );

  void removeItem(int index) {
    final removedItem = items[index];
    // 나의 로컬 리스트를 변동시켜줍니다.
    items.removeAt(index);
    /*
     AnimatedList의 현재 상태를 변화시켜줌으로써 애니매이션 효과를 발생시킵니다.
     삭제되면서 어떤 애니메이션 효과를 취하고 싶어? 라고 이해하면 편합니다.
     바로 밑에 removeItem method는 AnimatedList 위젯 내부에서 구현된 함수입니다.
     이를 어떻게 우리가 사용할 수 있냐? 라고 한다면 우리가 GlobalKey를 통해서 AnimatedList와 연동시켜줬기 때문입니다.
    */

    listKey.currentState!.removeItem(
        index,
        (context, animation) => ListItemWidget(
            item: removedItem, animation: animation, onClicked: () {}),
        duration: const Duration(milliseconds: 600));
  }

  void insertItem() {
    const newIndex = 1;
    final newItem = (List.of(listItems)..shuffle()).first;

    // 나의 로컬 리스트를 변동시켜줍니다.
    items.insert(newIndex, newItem);

    /*
     AnimatedList의 현재 상태를 변화시켜줌으로써 애니매이션 효과를 발생시킵니다.
     추가되면서 어떤 애니메이션 효과를 취하고 싶어? 라고 이해하면 편합니다.
     바로 밑에 insertItem method는 AnimatedList 위젯 내부에서 구현된 함수입니다.
     이를 어떻게 우리가 사용할 수 있냐? 라고 한다면 우리가 GlobalKey를 통해서 AnimatedList와 연동시켜줬기 때문입니다.
    */
    listKey.currentState!
        .insertItem(newIndex, duration: const Duration(milliseconds: 600));
  }
}

```

### Primary properties

- `initialItemCount` => int

리스트 초기의 아이템 개수를 설정합니다.

- `itemBuilder` => AnimatedListItemBuilder

리스트 아이템 하나하나를 랜더링 할 수 있도록 도와주는 속성입니다.
아이템 위젯들을 빌드하도록 도와줍니다.
(context, index, animation) 를 인자로 받습니다.
index는 아이템의 order를 나타냅니다. animation을 받아서 내부에서 사용할 수 있습니다.

- `padding` => EdgeInsetsGeometry?

자식들을 패딩으로 감싸줍니다.

- `reverse` => bool

리스트의 방향을 설정합니다 기본적으로는 위에서부터 하나하나 쌓이면서 아래로 흘러가지만 이 값을 `true`로 설정하게 되면 아래에서부터 리스트가 시작됩니다.
그 후 위의 방향으로 아이템들이 쌓이게 됩니다. 우리가 흔히 사용하는 채팅 애플리케이션을 살펴보면 최신 채팅이 아래에 쌓이게 되는데 이 속성을 이용하여 구현할 수 있습니다.

---

`최종 수정일 : 22/10/10`
