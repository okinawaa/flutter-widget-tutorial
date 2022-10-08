# FutureBuilder

### Inheritance

Object > DiagnosticableTree > Widget > StatefulWidget > FutureBuilder

### Description

FutureBuilder를 사용하는 이유는 서버로부터 원하는 데이터를 받아오기 전에 데이터가 없는 상태에서 사용자에게 보여줄 UI를 그리기 위함이다. 사용자에게 로딩중이거나, 에러가 발생했거나를 알려주는 UI는 UX증진에 있어서 매우 중요한 요소이다.

일반적으로 생각을한다면 데이터를 호출하고, 아직 호출결과값이 오기 전이라면 setState()를 통해서 로딩화면을 보여줄 수 있다.<br> 이러한 일련의 작업을 개발자가 쉽게 할 수 있도록 도와주는것이 FutureBuilder 위젯이다.

FutureBuilder는 네트워크 통신 및 비동기 통신에 사용된다.

어렵게 생각하지 말고 쉬운 언어로 풀이하면 아직 사용자에게 보여줄 정보가 서버로부터 가져오지 않았을때 그리고 비로소 데이터가 도착했을때! 각 상태별로 처리할 수 있는 것이다.

### Example

예제 코드는 [FutureBuilder docs](https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html) 로 부터 가져왔습니다.

```dart

import 'package:flutter/material.dart';

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
  final Future<String> _calculation = Future<String>.delayed(
    const Duration(seconds: 2),
    () => 'Data Loaded',
  );

  @override
  Widget build(BuildContext context) {
    return DefaultTextStyle(
      style: Theme.of(context).textTheme.headline2!,
      textAlign: TextAlign.center,
      child: FutureBuilder<String>(
        future: _calculation, // a previously-obtained Future<String> or null
        builder: (BuildContext context, AsyncSnapshot<String> snapshot) {
          List<Widget> children;
          if (snapshot.hasData) {
            children = <Widget>[
              const Icon(
                Icons.check_circle_outline,
                color: Colors.green,
                size: 60,
              ),
              Padding(
                padding: const EdgeInsets.only(top: 16),
                child: Text('Result: ${snapshot.data}'),
              ),
            ];
          } else if (snapshot.hasError) {
            children = <Widget>[
              const Icon(
                Icons.error_outline,
                color: Colors.red,
                size: 60,
              ),
              Padding(
                padding: const EdgeInsets.only(top: 16),
                child: Text('Error: ${snapshot.error}'),
              ),
            ];
          } else {
            children = const <Widget>[
              SizedBox(
                width: 60,
                height: 60,
                child: CircularProgressIndicator(),
              ),
              Padding(
                padding: EdgeInsets.only(top: 16),
                child: Text('Awaiting result...'),
              ),
            ];
          }
          return Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: children,
            ),
          );
        },
      ),
    );
  }
}

```

위 코드는 \_calculation 이라는 Future를 반환하는 함수가 있습니다. 2초후에 Data Loaded라는 String을 반환해줍니다.
저 String이 우리가 서버로부터 받아야할 정보라고 생각하면 이해하기 쉽습니다.

FutureBuilder를 사용한 부분을 보면
future라는 속성에 Future를 반환하는 실행함수를 넣어줍니다.
builder라는 속성에는 BuildContext와 AsyncSnapshot을 받는 함수를 사용합니다.
AsyncSnapshot에는 hasData라는 메소드가 있고, 이것을 통해서 우리는 정보가 도착했는지 안했는지 판단할 수 있습니다.
위 코드를 실행시켜보면 초기 2초는 최하단 else구문을 실행시켜서 Awaiting result 라는 글자가 보이고 2초후에는 Future 함수가 String을 반환하여 Result Data Loaded라는 글자가 보일것입니다.<br>

예제나 다른 블로그를 찾아보면 위 예제처럼 스냅샷의 hasData로 분기처리를 하는 경우가 많은데, 저의 생각에는 비직관적이라고 생각합니다. 데이터가 들어왔는지 안들어왔는지보다
AsyncSnapshot 에서 제공해주는 connectionState 변수를 활용해서 분기를 하는것이 더 직관적이라고 생각합니다. connectionState는 현재 데이터 전송이 끝났는지? 아직 진행중인지 여러가지 상황을 제공해줍니다.

![image](https://user-images.githubusercontent.com/69495129/194713139-d1d36ea8-2043-4dd8-a4f1-db78f4e4b097.png)

사진 출처: [인코덤님 블로그](http://www.incodom.kr/Flutter/FutureBuilder)

많은 분들도 자신이 편하게 생각할 수 있는 변수를 사용하여 분기처리를 해서 사용자에게 더 좋은 UI를 보여줬으면 좋겠습니다.

---

### Primary Properties

- `future` => Future<T>?

Future값을 반환해주는 함수를 설정합니다. 데이터를 요구하고 Future로 반환하는 함수가 들어간다고 생각하면 이해하기 쉽습니다.

- `builder` => AsyncWidgetBuilder<T>?
  이 속성에는 BuildContext와 AsyncSnapshot을 받는 함수를 사용합니다. 비동기 처리시 사용할 수 있는 많은 정보들이 AsyncSnapshot에 존재하고 있으므로 많이 사용하며 익숙해지는것이 좋을 것 같습니다.

- `initialData` => T?
  비동기 함수가 끝나기 전까지 snapshots 으로 사용될 데이터를 정해줄 수 있습니다. 더미데이터를 미리 보여주는것과 같이 UX를 증진시키기 위해서 사용되어질 수 있습니다.

---

`최종 수정일 : 22/10/08`
