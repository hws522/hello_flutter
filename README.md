# hello-flutter

<br>
<br>

## 2.3 Hello World

- 모든 것은 위젯이다. 블록처럼 위젯에 위젯을 쌓아가며 앱을 만드는 것.

- 위젯은 외우지 말고 찾아보며 사용하자. https://docs.flutter.dev/development/ui/widgets

- 모든 위젯은 build 메서드를 사용해야한다.(build 또한 자동 완성 가능)

- 앱의 root Widget 은 두 개의 옵션 중 하나를 return 해야 한다.

  CupertinoApp(애플의 디자인 시스템) 혹은 MaterialApp(구글의 디자인 시스템) 중에 선택해야 한다.

  이는 우리가 어떤 family style 을 사용할 지 flutter 에게 말해주는 것이다.

  내가 구글이나 애플의 디자인을 따라하지 않고 새로운 나만의 디자인을 하고 싶다 하더라도, app 의 root 이자 시작점이기에 기본 UI 설정과 같은 재료들을 선택해 줘야만 한다.

  flutter 는 구글이 만들었기 때문에 MaterialApp 이 훨씬 보기 좋으니 MaterialApp 을 쓰자.

- 모든 화면은 Scaffold(구조)를 가져야 한다.

<br>

## 2.4 Recap

EVERYTHING IS WIDGET

**`모든 것이 위젯`** 이다.

전부 위젯에 관한 내용이고 완전 선언형이다.

클래스를 위젯으로 바꿔주기 위해 flutter 의 core widget 중 하나인 StatelessWidget 을 상속받았다.

아주 기초적인 위젯이고 화면에 뭔가를 띄워주는 것 말고는 하는 일이 없다.

위젯이 된다는 건 계약을 맺는 것이다. 그 계약은 바로 build 메소드를 구현해야 한다는 것이다.

앱을 시작할 때 뜨는 첫번째 widget 은 앱의 root 라고 할 수 있다.

앱의 root 는 material 혹은 Cupertino 디자인 중 하나를 선택해서 리턴해야 한다.

모든 것이 위젯이라고 하지만, 그저 dart 의 class 를 사용하고 있다는 걸 알아야 한다.

<br>

## 2.5 Classes Recap

flutter 는 완전 객체지향 프레임워크다.

모든 게 다 class 라는 뜻이고 모든 widget 은 class 다.

어떤 widget 이건, 마우스를 올리면 constructor 를 볼 수 있고, 이 것들을 읽을 줄 알아야 한다.

우리는 widget 을 사용할 때마다 class 를 인스턴스화 하고 있다.

dart 는 `new` 를 써줄 필요가 없다. 쓰던 안쓰던 똑같기 때문이다.

`new` 를 다 쓴다면, 아래와 같다.

```dart
void main() {
  runApp(new App());
}

class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Hello Flutter!'),
        ),
        body: new Center(
          child: new Text('Hello World!'),
        ),
      ),
    );
  }
}
```

우리가 사용하는 Text class 같은 데서 볼 수 있는 constructor(생성자) 가 아래와 같다.

positional parameter 라고 한다. argument 의 위치가 중요하다.

```dart
class Player {
  String name;
  Player(this.name);
}

void main() {
  var testPlayer = Player('test');
  // testPlayer.name => test
  runApp(App());
}
```

다른 종류의 constructor 는 named parameter 라는 것이다.

home, appBar, title 등이 이와 같다.

파라미터가 많을 땐 순서를 잊어버리기 쉽기에 위의 방법과 같이 하지 않는다.

대신 이름에 기반하여 사용한다.

```dart
class Player {
  String name;
  Player({required this.name});
}

void main() {
  var testPlayer = Player(name: 'test');
  // testPlayer.name => test
  runApp(App());
}
```

`?` 를 추가하면 Player 가 name 을 가질 수도, 가지지 않을 수도 있다고 정의한다.

```dart
class Player {
  String? name;
  Player();
}
```

<br>

## 3.0 Header

```dart
class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
          backgroundColor: Color(0xff181818),
          body: Padding(
            padding: EdgeInsets.symmetric(horizontal: 40),
            child: Column(
              children: [
                SizedBox(
                  height: 80,
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.end,
                  children: [
                    Column(
                      crossAxisAlignment: CrossAxisAlignment.end,
                      children: [
                        Text(
                          'Hey, Selena',
                          style: TextStyle(
                            color: Colors.white,
                            fontSize: 28,
                            fontWeight: FontWeight.w700,
                          ),
                        ),
                        Text(
                          'Welcome back',
                          style: TextStyle(
                            color: Colors.white.withOpacity(0.8),
                            fontSize: 18,
                          ),
                        ),
                      ],
                    )
                  ],
                )
              ],
            ),
          )),
    );
  }
}

```

하나의 함수 안에 모두 다 넣을 수 있지만, 코드가 굉장히 더럽다.

가독성이 매우 떨어진다.

이대로는 점점 더 길어지고 복잡해져서 작업하기 힘들 것이다.

<br>

## 3.1 Developer Tools

제목은 `Developer Tools` 라고 되어 있지만

`Column` 과 `Row` 라는 두가지 Widget 을 배웠던 것을 다시금 정리했다.

(여기서는 `Column` 과 `Row` 를 내가 알던 개념의 반대로 설명해주고 있다.

서로 **상-하로 놓고 싶을 때는 Column** 을 사용하고, **좌-우로 놓고 싶을 때는 Row** 를 사용한다고 한다.

무튼 이 부분이 내가 알던 개념이랑 달라서 적어놔야겠다 싶어서 이렇게 따로 써놓는다. 굳이 따지지 않고 넘어가려고 한다.)

`Row` 와 `Column` 은 `MainAxis` 와 `CrossAxis` 를 가지고 있다.

Row 의 MainAxis 는 수평(가로)방향이다.

Row 의 CrossAxis sms 수직(세로)방향이다.

Column 의 MainAxis 는 수직(세로)방향이다.

Column 의 CrossAxis 는 수평(가로)방향이다.

=> `Row` 에서는 `가로`가 Main, `Column` 에서는 `세로`가 Main 이다.

`space(간격)` 를 주기 위해서는 `SizedBox` 를 사용해야 한다.

색상을 주기 위해서는 `Colors` 를 사용해야 한다. 직접 외부에서 가져온 색을 입력해 넣을 수도 있고, 팔레트에 있는 색상을 사용할 수도 있다.

`Layout` 이 헷갈린다면, 개발자 도구를 사용하면 된다.

내부에 어떤 위젯이 있는지, 어떻게 설정되어 있는지 쉽게 알 수 있다.

<br>

## 3.2 Buttons Section

`Container` 라는 Widget 을 사용한다.

`Container` 는 `<div>` 같은 것이다. child 를 가지고 있는 단순한 box.

앞으로 자주 사용할 것이다.

```dart
...
Row(
  children: [
    Container(
      decoration: BoxDecoration(
          color: Colors.amber,
          borderRadius: BorderRadius.circular(
            45,
          )),
      child: Padding(
          padding: EdgeInsets.symmetric(
            vertical: 20,
            horizontal: 50,
          ),
          child: Text(
            'Transfer',
            style: TextStyle(
              fontSize: 20,
            ),
          )),
    )
  ],
)
...
```

<br>

## 3.3 VSCode Settings

vscode 에서 작업을 하다보면, 파란색 줄로 경고문이 나타나는것을 확인할 수 있다.

마우스를 올려보면, 이런 경고가 나타난다.

```
Use 'const' with the constructor to improve performance.
Try adding the 'const' keyword to the constructor invocation.dart(prefer_const_constructors)
```

Dart 는 constant(상수) 개념을 지원한다.

constant(상수)로 값을 지정하게 되면, 컴파일전에 그 value(값)을 알 수 있기 때문에 컴파일러는 변수를 위한 메모리 공간을 만드는 대신, 상수를 계산해서 대체하게된다.

이는 훨씬 더 나은 코드를 만들어 준다.

경고문처럼 실제로 값이 바뀌지 않을 예정이라면 constant 로 만드는 것이 더 나을 수도 있다. const 를 추가하게되면 바로 파란색 줄이 사라지게 된다.

런타임 대신 컴파일러가 컴파일 중에 값을 산정할 수 있으므로 app 이 동작하는데 더 쉽다.

하지만 어떤 것은 상수가 될 수 있고, 어떤 것은 될 수 없는지 기억하고 있는 것은 쉽지 않기 때문에 vscode 설정을 통해 해결하도록 한다.

```json
...
"editor.codeActionsOnSave": {
    "source.fixAll": true
  }
...
```

<br>

## 3.4 Code Actions

`Code Actions` 는 코드를 매우 간단한 방법으로 리팩토링하게 해준다.

예를 들어 기존코드에서 Text 를 padding 안에 넣는다던지, Row 안에 Text 를 넣는다던지, Row 나 Col 을 감싸는 상위에 padding 을 추가하는 등의 작업을 할 때 Container 를 만들고 child 에 붙여넣기하는 식의 수동으로 코드를 수정한다.

이 과정이 귀찮고 실수를 하기 쉽기 때문에, 코드 우측에 보이는 전구를 누르면 보이는 Code Actions 를 이용한다.

마우스로 전구를 직접 클릭해도 되지만, 마우스 호버시 보이는 단축키를 이용할 수도 있다.(command + .)

<br>

## 3.5 Reusable Widgets

반복 사용되는 위젯을 재사용이 가능하도록 만들 수 있다.

main 이 아닌 widget 폴더에 위젯으로 사용할 버튼을 클래스로 생성한다.

모든 위젯은 각자 나름대로의 build 메소드를 실행시켜야만 한다.

배경 색상, 텍스트 색상, 텍스트 내용을 전송해서 재사용하기 위해 아래처럼 코드를 작성한다.

```dart
// button.dart
import 'package:flutter/material.dart';

class Button extends StatelessWidget {
  final String text;
  final Color bgColor;
  final Color textColor;

  const Button({
    super.key,
    required this.text,
    required this.bgColor,
    required this.textColor,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: BoxDecoration(
          color: bgColor,
          borderRadius: BorderRadius.circular(
            45,
          )),
      child: Padding(
          padding: const EdgeInsets.symmetric(
            vertical: 20,
            horizontal: 50,
          ),
          child: Text(
            text,
            style: TextStyle(
              color: textColor,
              fontSize: 20,
            ),
          )),
    );
  }
}
```

위의 위젯도 클래스일 뿐이다.

Dart 에서 만든 클래스처럼 프로퍼티들을 추가해주는 작업을 했다.

타입을 설정한 후, 생성자 함수에 넣기만 하면 된다.

<br>

## 3.6 Cards

```dart
...
Container(
  decoration: BoxDecoration(
    color: const Color(0xff1f2123),
    borderRadius: BorderRadius.circular(25),
  ),
  child: Padding(
    padding: const EdgeInsets.all(30),
    child: Row(
      children: [
        Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text(
              'Euro',
              style: TextStyle(
                color: Colors.white,
                fontSize: 32,
                fontWeight: FontWeight.w600,
              ),
            ),
            const SizedBox(
              height: 10,
            ),
            Row(
              children: [
                const Text(
                  '6 428',
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 20,
                  ),
                ),
                const SizedBox(
                  width: 5,
                ),
                Text(
                  'EUR',
                  style: TextStyle(
                    color: Colors.white.withOpacity(0.8),
                    fontSize: 20,
                  ),
                ),
              ],
            )
          ],
        )
      ],
    ),
  ))
```

<br>

## 3.7 Icons and Transforms

`Transform` 을 이용하면, `Transform` 내부 child 의 크기나 위치를 변경할 수 있다.

아이콘의 크기를 직접 키우게 되면, 해당 아이콘을 감싸는 카드의 크기가 같이 커져서 원하는 이미지를 만들 수 없다.

`Transform` 을 이용해서 아이콘의 크기만을 키운 후, 상위 컨테이너의 `clipBehavior` 속성을 이용하면 하위 위젯들의 크기가 커졌을 경우 보이지 않도록 할 수 있다.

```dart
...
Container(
  clipBehavior: Clip.hardEdge,
...
  Transform.scale(
    scale: 2.2,
    child: Transform.translate(
      offset: const Offset(-5, 12),
      child: const Icon(
        Icons.euro_rounded,
        color: Colors.white,
        size: 88,
      ),
  ))
)
```

<br>

## 3.8 Reusable Cards

하단에 위치하는 카드들을 재사용 가능한 위젯을 이용하기 위해 위젯을 생성한다.

생성과 동시에 재사용할 때 필요할만한 데이터들을 정하고 해당 데이터들을 property 로 만든다.

그리고 code action 이나 직접 생성자를 만든다.

색상반전을 표현하기 위해 반전을 체크하는 임의의 property(isInverted) 를 만든다.

그 후 하드코딩된, 재사용 시 property 가 들어갈 자리에 property 로 값을 수정해준다.

반전 색상을 지정할 때 삼항연산자를 이용해 지정하는데 이때 색상을 그대로 복사붙여넣기 하는 것 보단 상위에서 변수로 색상을 지정하여 쓰면 깔끔하다. 이때 `_` 를 붙여서 private 하게 만들겠다는 것을 의미한다.

```dart
import 'package:flutter/material.dart';

class CurrencyCard extends StatelessWidget {
  final String name, code, amount;
  final IconData icon;
  final bool isInverted;

  final _blackColor = const Color(0xff1f2123);
  final _whiteColor = const Color(0xffffffff);

  const CurrencyCard({
    super.key,
    required this.name,
    required this.code,
    required this.amount,
    required this.icon,
    required this.isInverted,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
        clipBehavior: Clip.hardEdge,
        decoration: BoxDecoration(
          color: isInverted ? _whiteColor : _blackColor,
          borderRadius: BorderRadius.circular(25),
        ),
        child: Padding(
          padding: const EdgeInsets.all(30),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    name,
                    style: TextStyle(
                      color: isInverted ? _blackColor : _whiteColor,
                      fontSize: 32,
                      fontWeight: FontWeight.w600,
                    ),
                  ),
                  const SizedBox(
                    height: 10,
                  ),
                  Row(
                    children: [
                      Text(
                        amount,
                        style: TextStyle(
                          color: isInverted ? _blackColor : _whiteColor,
                          fontSize: 20,
                        ),
                      ),
                      const SizedBox(
                        width: 5,
                      ),
                      Text(
                        code,
                        style: TextStyle(
                          color: isInverted
                              ? _blackColor
                              : Colors.white.withOpacity(0.8),
                          fontSize: 20,
                        ),
                      ),
                    ],
                  )
                ],
              ),
              Transform.scale(
                  scale: 2.2,
                  child: Transform.translate(
                    offset: const Offset(-5, 12),
                    child: Icon(
                      icon,
                      color: isInverted ? _blackColor : _whiteColor,
                      size: 88,
                    ),
                  ))
            ],
          ),
        ));
  }
}
```

카드 위젯을 여러개 넣다보면 에러가 발생한다. 화면을 벗어나기 때문이다.

화면을 넘쳐흐르는 UI 를 만들 때 화면을 스크롤링할 수 있도록 만들 수 있다.

app 을 감싸는 body 에 `SingleChildScrollView` 위젯을 사용하면 스크롤이 가능하다.

```dart
Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
          backgroundColor: const Color(0xff181818),
          body: SingleChildScrollView(
            child: Padding(
              ...
            )
            ...
          )
          ...
        )
      ...
    )
  ...
}
```

카드가 겹쳐있는듯한 느낌을 주려면 Transform.translate 위젯을 이용하면 된다.

```dart
...
  Transform.translate(
    offset: const Offset(0, -30),
    child: const CurrencyCard(
      name: 'Bitcoin',
      code: 'BTC',
      amount: '9 785',
      icon: Icons.currency_bitcoin,
      isInverted: true,
    ),
  ),
...
```

<br>

## 4.0 State

**Stateful Widget**

지금까지는 `Stateless Widget` 을 사용했다.

`Stateless Widget` 은 매우 간단하다.

build 메서드를 통해 그저 UI 를 출력할 뿐이다.

`Stateful Widget` 은 상태를 가지고 있어서 Stateful 로 불린다.

Stateful widget 은 두 파트로 나뉜다.

첫번째는 상태가 없는 위젯 그 자체다.

두번째는 위젯의 상태(state)로, 위젯의 state 는 데이터와 UI 를 가지고 있는 부분이다.

그리고 Stateful Widget 의 데이터는 dart class property 일 뿐이다.

아래는 간단히 클릭한 횟수를 화면에 그려주는 state 를 구현한 코드이다.

```dart
class App extends StatefulWidget {
  @override
  State<App> createState() => _AppState();
}

class _AppState extends State<App> {
  int counter = 0;

  void onClicked() {
    counter = counter + 1;
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: const Color(0xFFF4EDDB),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              const Text(
                'Click Count',
                style: TextStyle(fontSize: 30),
              ),
              Text(
                '$counter',
                style: const TextStyle(fontSize: 30),
              ),
              IconButton(
                iconSize: 40,
                onPressed: onClicked,
                icon: const Icon(
                  Icons.add_box_rounded,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

<br>

## 4.1 setState

State 를 가지고 있는 `StatefulWidget` 을 만들었다.

```dart
class App extends StatefulWidget {
  @override
  State<App> createState() => _AppState();
}

class _AppState extends State<App> {
  ...
}
```

그리고 State 에 UI 를 넣고 데이터도 넣었다.

```dart
class _AppState extends State<App> {
  int counter = 0;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      ...
    );
  }
}
```

데이터도 수정했다.

```dart
...
void onClicked() {
    counter = counter + 1;
  }
...
```

하지만 `setState` 함수를 호출하지 않는다면, `build` 메서드는 다시 실행되지 않는다. 플러터는 게으르기 때문이다.

`setState` 함수는 State 클래스에게 데이터가 변경되었다고 알리는 함수다.

```dart
int counter = 0;

void onClicked() {
  setState(() {
    counter = counter + 1;
  });
}
```

위처럼 setState 함수를 이용해 flutter 의 위젯에게 새로운 데이터가 있다고 알려주는 것이다.

그러면 flutter 는 build 메서드를 다시 실행한다.

setState 는 기본적으로 새로운 데이터와 함께 build 메서드를 한 번 더 호출하는 것이다.

데이터의 변화를 무조건 setState 내부에 넣을 필요는 없지만, 가독성이 더 좋기 때문에 권장된다.

<br>

## 4.2 Recap

setState 함수를 이용해 flutter 는 build 메서드를 다시 실행한다.

setState 함수를 사용하지 않으면, onClicked 함수 내부에 console.log 로 확인 시 counter 값은 업데이트 되는 것이 확인 되지만 화면은 업데이트 되지 않는다.

데이터의 업데이트가 build 메서드를 다시 실행하지는 않기 때문이다.

react 와는 다르게, 더 좋은 위젯들을 사용할 것이기 때문에 state 를 자주 사용하지는 않는다.

<br>

## 4.3 BuildContext

`BuildContext` 를 이용하면 색상, 크기, 글자 굵기 등 app 의 모든 스타일적인 요소를 한곳에서 지정할 수 있다.

`theme: ThemData` 를 이용해서 원하는 스타일을 지정한다.

theme 를 만들면, 해당 theme 은 애플리케이션 위젯의 state 에 있다는 것을 알 수 있다.

그리고 그 애플리케이션 위젯의 state 는 MyLargeTitle 이라는 자식을 가지고 있다.

MyLargeTitle 에서 theme 값에 접근 하려면, BuildContext 를 이용한다.

부모에게 직접 접근하는 것이다.

위젯 트리에 대해 알아야하는데, flutter 가 어떻게 렌더링 되는지 알 수 있다.

위젯 트리 상으로 MyLargeTitle 은 아래로 5단계를 내려가야 한다.

context 는 Text 이전에 있는 모든 상위 요소들에 대한 정보다.

context 는 MyLargeTitle Text 의 부모 요소들의 모든 정보를 담고 있다.

즉 context 는 위젯 트리에 대한 정보가 담겨있고, 매우 먼 요소의 데이터를 가져올 수 있기 때문에 유용하다.

context 를 이용해서 해당 위젯이 어떤 위젯이고, 부모 요소는 무엇인지 알 수 있고 그 상위 부모 요소에도 접근할 수 있다.

아래처럼 `Theme.of(context).textTheme.titleLarge` 이런 식으로 불러온다.

```dart
...
class _AppState extends State<App> {
  ...
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        textTheme: const TextTheme(
          titleLarge: TextStyle(
            color: Colors.red,
          ),
        ),
      ),
      ...
    );
  }
}

class MyLargeTitle extends StatelessWidget {
  ...
  @override
  Widget build(BuildContext context) {
    return Text(
      'My Large Title',
      style: TextStyle(
        fontSize: 30,
        color: Theme.of(context).textTheme.titleLarge?.color,
      ),
    );
  }
}
```

정리하면, BuildContext 는 위젯 트리에서 위젯의 위치를 제공하고 이를 통해 상위 요소 데이터에 접근할 수 있다.

<br>

## 4.4 Widget Lifecycle

`StatefulWidget` 은 살아있다.

이게 무슨말이냐하면, react 처럼 `생명주기(Lifecycle)`를 가지고 있다는 것이다.

생명주기는 여러 메서드들에 반응하는데, 그 중 가장 중요한 건 `initState`, `dispose`, `build` 다.

build 는 위젯에서 UI 를 만든다.

initState 는 build 이전에 호출되며, 변수를 초기화하며 api update 구독 등을 할 수 있게 해준다. 그 후 build 가 호출된다.

dispose 는 위젯이 위젯 트리에서 제거될 때 실행된다. 여기서는 이벤트 리스너 같은 것들을 구독 취소하는 것이다.

외울필요는 없고, 그저 이러한 것들이 widget life cycle 이라는 것을 알아야한다는 것 뿐이다.

```dart
...
class MyLargeTitle extends StatefulWidget {
  const MyLargeTitle({
    super.key,
  });

  @override
  State<MyLargeTitle> createState() => _MyLargeTitleState();
}

class _MyLargeTitleState extends State<MyLargeTitle> {
  int count = 0;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    print('initState!');
  }

  @override
  void dispose() {
    // TODO: implement dispose
    super.dispose();
    print('dispose!');
  }

  @override
  Widget build(BuildContext context) {
    return Text(
      'My Large Title',
      style: TextStyle(
        fontSize: 30,
        color: Theme.of(context).textTheme.titleLarge?.color,
      ),
    );
  }
}

```

<br>

## 5.0 User Interface

`POMODORO APP` 을 만들어본다.

`Scaffold` body 에 Column 을 넣고 children 배열을 `Flexible` 로 구성한다.

`Flexible` 은 UI 를 하드코딩이 아닌, `비율에 기반`에서 더 유연하게 만들 수 있도록 해준다.

아래처럼 `Flexible` 은 상위 박스 내부의 박스들 중, 하나의 박스가 얼마나 공간을 차지할 지 비율을 정할 수 있다.

```dart
class _HomeScreenState extends State<HomeScreen> {

 @override
 Widget build(BuildContext context) {
   return Scaffold(
     body: Column(
       children: [
         Flexible(
           flex: 1,
           child: Container(
             ...
           ),
         ),
         Flexible(
           flex: 2,
           child: Container(
             ...
           ),
         ),
         Flexible(
           flex: 1,
           child: Container(
             ...
           ),
         ),
       ]
     ),
   );
 }
}
```

`Expanded` 을 이용하면 하위 `child` 에 들어가는 `container` 를 끝까지 확장시켜서 사용할 수 있다.

```dart
Flexible(
  flex: 1,
  child: Row(
    children: [
      Expanded(
        child: Container(
        ...
        )
      ),
    ],
  ),
)
```

<br>

## 5.1 Timer

카운트를 시작할 함수를 만든다.

해당 함수는 `Timer` 를 만드는데, `Timer` 는 Dart 의 표준 라이브러리에 포함되어 있다.

아래처럼 `Timer` 를 바로 초기화하지 않고, 사용자가 버튼을 누를 때만 타이머가 생성되도록 하기 위해 `late` 라는 `variable modifier` 를 사용한다.

`late` 는 이 property 를 당장 초기화하지 않아도 된다는 뜻이지만, 반드시 사용하기전에 초기화한다고 약속하는 것이다.

```dart
class _HomeScreenState extends State<HomeScreen> {
  int totalSeconds = 1500;
  late Timer timer;


  void onTick(Timer timer) {
    setState(() {
      totalSeconds--;
    });
  }

// Timer 를 초기화하는 method
// 매 초 마다 onTick 함수를 실행한다.
  void onStartPressed() {
    timer = Timer.periodic(
      const Duration(seconds: 1),
      onTick,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      ...
    )
  }
}
```

<br>

## 5.2 Pause Play

일시정지 기능을 만들기 위해, isRunning 이라는 `boolean property` 를 만든다.

타이머의 작동상태에 따라 다른 아이콘을 보여주기 위해 삼항연산자로 처리한다.

```dart
...
Flexible(
  flex: 3,
  child: Center(
    child: IconButton(
      ...
      icon: Icon(isRunning
          ? Icons.pause_circle_outline
          : Icons.play_circle_outline),
    ),
  ),
),
```

이전에 만든 타이머 시작 함수안에 `setState` 로 `isRunning` 을 `true` 로 업데이트 한다.

일시정지 상태일 때 버튼을 누르면 카운트를 시작하고 작동 중일 때 버튼을 누르면 일시정지하기 위해 새로운 `method` 를 만들어준다.

`onPausePressed` 라는 새로운 `method` 는 일시정지 기능을 하는 함수로서 `timer.cancel()` 을 통해 타이머를 멈추고 `setState` 에서 `isRunning` 을 `false` 로 업데이트 한다.

```dart
void onPausePressed() {
  timer.cancel();
  setState(() {
    isRunning = false;
  });
}
```

`onPressed` 를 작동 상태에 따라 만들었던 `method` 를 삼항연산자로 처리한다.

```dart
Flexible(
  flex: 3,
  child: Center(
    child: IconButton(
     ...
      onPressed: isRunning ? onPausePressed : onStartPressed,
      ...
    ),
  ),
),
```

<br>

## 5.3 Date Format

몇 번을 완료했는지 확인하기 위한 `totalPomodoros` 라는 새로운 `property` 를 추가한다.

매 초 마다 실행되는 `onTick method` 에 조건을 걸어 `totalSeconds` 가 0 일 경우 타이머를 중지하고 `totalPomodoros` 를 증가시키고 다시 1500 부터 시작하도록 만든다.

1500 을 `static const` 변수 `twentyFiveMinutes` 로 만들어 실수를 줄인다.

```dart
...
void onTick(Timer timer) {
    setState(() {
      totalSeconds = totalSeconds - 1;
    });
    if (totalSeconds == 0) {
      setState(() {
        totalPomodoros = totalPomodoros + 1;
        isRunning = false;
        totalSeconds = twentyFiveMinutes;
      });
      timer.cancel();
    } else {
      setState(() {
        totalSeconds = totalSeconds - 1;
      });
    }
  }
...
```

1500 처럼 초 단위를 분 단위로 보여주도록 하기 위해 format 이라는 새로운 method 를 만든다.

해당 method 는 숫자를 입력받아 문자열로 반환한다.

`Duration` 을 이용해 기본값으로 변경되는 `format` 을 보고 내가 원하는 모양으로 바꾸기 위해, `split` 을 기준으로 나누고 필요없는 문자열을 잘라 `format` 을 바꿔 return 한다.

```dart
...
 String format(int seconds) {
  var duration = Duration(seconds: seconds);
  return duration.toString().split(".").first.substring(2, 7);
}
...
```

<br>

## 6.1 AppBar

```dart
class App extends StatelessWidget {
  const App({super.key}); // 이 위젯의 key 를 stateless widget 이라는 슈퍼클래스에 보낸 것.

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: HomeScreen(),
    );
  }
}
```

위젯은 key 라는 걸 가지고 있고, ID 처럼 쓰인다. 그리고 flutter 는 위젯을 식별하기 위해서 ID 를 쓴다.

home_screen_6.dart 의 Stateless widget 은 `Scaffold` 를 반환하는데, `scaffold` 는 `screen 을 위한 기본적인 레이아웃과 설정을 제공`해준다.

여기에 appBar 를 렌더링 한다.

<br>

## 6.2 Data Fetching

lib 폴더안에 services 라는 새로운 폴더를 만들어주고 그 안에 `api_service.dart` 라는 파일을 만든다.

`api_service.dart` 안에는 flutter 위젯이나 클래스가 아닌 `평범한 Dart 클래스인 ApiService` 를 만든다.

```dart
class ApiService {
  final String baseUrl = "https://webtoon-crawler.nomadcoders.workers.dev";
  final String today = "today";
  ...
}

```

내가 원하는 URL 에 요청을 보내기 위해서는 `http` 패키지가 필요하다.

Flutter 나 Dart 패키지를 찾고 싶으면 `pub.dev` 라는 공식 패키지 보관소로 가면 된다.

`http` 패키지를 설치 후, GET 요청을 보낼 준비를 한다.

```dart
class ApiService {
...
  void getTodaysToons() async {
    final url = Uri.parse('$baseUrl/$today');
    final response = await http.get(url);
    if (response.statusCode == 200) {
      print(response.body);
      return;
    }
    throw Error();
  }
}
```

api 에 요청을 할 경우, 해당 요청을 처리하는데 오랜 시간이 걸릴 수 있다.

기다리게 하지 않으면, Dart 는 api 를 호출한 뒤 결괏값을 기다리지 않고 바로 다음으로 넘어가기 때문에 해당 요청이 처리되어 응답을 반환할 때까지 기다리게 해야한다.

이때 `async - await` 키워드를 사용하면 된다.

`await` 와 `Future` 타입을 보통 같이 사용한다.

`http.get(URL))` 에 마우스를 올려보면 아래와 같이 나온다.

```dart
  Future<Response> get(Uri url, {Map<String, String>? headers})
```

`Future` 는 미래에 받을 값의 타입을 알려주기 때문에, 완료가 되었을 때 `Response` 라는 타입을 반환할 거라고 알려주는 것이다.

<br>

## 6.3 fromJson

서버로부터 받는 JSON 형식의 데이터를 Dart, Flutter 에서 쓸 수 있는 데이터 형식인 클래스로 바꿔야 한다.

현재 response.body 의 타입이 string 이기 때문에, JSON 으로 decode 해줘야 한다. 이때 `jsonDecode` 라는 함수를 사용한다.

jsonDecode 함수의 반환타입은 `dynamic` 이기 때문에, 직접 타입을 정해줘야한다.

response.body 는 여러 object 로 이루어진 리스트이기 때문에 `final List<dynamic> webtoons = jsonDecode(response.body)` 로 디코딩해준다.

`named constructor` 를 사용해 초기화한다.

```dart
class WebtoonModel {
  final String title, thumb, id;

  WebtoonModel.fromJson(Map<String, dynamic> json)
      : title = json['title'],
        thumb = json['thumb'],
        id = json['id'];
}
```

마지막으로 반복문을 통해 JSON 으로 변환한 데이터를 List 로 만든다.

```dart
class ApiService {
  ...
  Future<List<WebtoonModel>> getTodaysToons() async {
    List<WebtoonModel> webtoonInstances = [];
    ...
    if (response.statusCode == 200) {
      final List<dynamic> webtoons = jsonDecode(response.body);
      for (var webtoon in webtoons) {
        webtoonInstances.add(WebtoonModel.fromJson(webtoon));
      }
      return webtoonInstances;
    }
    throw Error();
  }
}
```

<br>

## 6.4 Recap

- `http.get` 은 `Future` 타입을 반환한다.

- `Future` 타입은 당장 완료될 수 있는 작업이 아니라는 걸 말한다.

- `Future` 타입을 기다리기위해 await 를 사용할 때는 async 를 같이 사용해줘야 한다.

- http.get 으로 받아오는 response 의 타입은 string 이라서 JSON 으로 변환시켜주기위해 `jsonDecode` 를 사용한다.

- 변환한 값은 dynamic 타입이기에 직접 지정을 해줘야하고, `List<dynamic>` 으로 지정해주긴 했지만 지워도 상관은 없다. 여기서는 다만 명시적으로 표현하기 위함일 뿐이다.

- 변환한 리스트의 데이터 하나당 fromJson 이라는 `named constructor` 를 이용해서 WebtoonModel 을 만들어준 뒤, 반복문으로 webtoonInstances 라는 리스트에 넣어 마지막에 반환한다.

<br>

## 6.5 waitForWebToons

ApiService 클래스의 모든 method 와 property 를 static 으로 바꾼다. 현재 클래스에는 state 가 없기 때문이다.

```dart
class ApiService {
  static const String baseUrl =
      "https://webtoon-crawler.nomadcoders.workers.dev";
  static const String today = "today";

  static Future<List<WebtoonModel>> getTodaysToons() async {
    ...
  }
}
```

api 를 통해 가져온 데이터가 필요한 곳이 `HomeScreen` 위젯이기 때문에 `HomeScreen` 에서 메서드를 호출한다.

`Future` 데이터를 불러와서 보여주는 방법은 두가지가 있지만, 기초적인 방법으로 적용한 후 나중에 발전된 방법을 사용한다.

`HomeScreen` 위젯을 `StatefulWidget` 으로 바꾼다.

그리고, `State` 가 가지는 데이터를 써준다.

`initState` 를 사용해서 api 를 호출하는 메서드를 불러오게 한다.

`setState` 를 통해 `StatefulWidget` 의 UI 가 새로고침될 수 있도록 한다.

```dart
class _HomeScreenState extends State<HomeScreen> {
  List<WebtoonModel> webtoons = [];
  bool isLoading = true;

  void waitForWebToons() async {
    webtoons = await ApiService.getTodaysToons();
    isLoading = false;
    setState(() {});
  }

  @override
  void initState() {
    super.initState();
    waitForWebToons();
  }
  ...
}
```

<br>

## 6.6 FutureBuilder

데이터를 fetch 하는 방법중 단순한 방법으로 `async - await` 를 사용하고, `State` 안에 결과를 넣은다음 `setState` 를 호출했다.

하지만 `State` 는 많이 쓰이지 않기 때문에 최대한 사용하지 않는 것이 좋다.

`State` 를 거의 쓰지 않거나, 전혀 쓰지 않는 좋은 `Widget` 과 `Framework` 가 많이 있다.

아래는 다른 방법으로 `StatelessWidget` 인 상태에서 fetch 할 수 있다.

HomeScreen 을 다시 `StatelessWidget` 으로 바꿔준다.

그리고 api 를 호출하는 함수를 불러온다.

```dart
class HomeScreen extends StatelessWidget {
  HomeScreen({super.key});

  Future<List<WebtoonModel>> webtoons = ApiService.getTodaysToons();
  ...
}
```

이전처럼` async - await` 를 사용하지 않았기 때문에, 기다리지 않는 것을 알 수 있다. 로딩상태도 업데이트되지 않는다.

이것을 해결하기위한 `Widget` 으로 `FutureBuilder` 가 있다.

아래처럼 `FutureBuilder` 는 `await` 를 쓸 필요없이 알아서 처리해준다.

`builder` 안의 `snapshot` 을 통해 `Future` 의 상태도 알 수 있다.

이를 통해 아래처럼 `Future` 를 기다릴 수 있고, 그동안의 로딩처리도 가능하다.

```dart
...
body: FutureBuilder(
        future: webtoons,
        builder: (context, snapshot) {
          if (snapshot.hasData) {
            return const Text("There is data!");
          }
          return const Text('Loading....');
        },
      ),
```

<br>

## 6.7 ListView

<br>

가져온 데이터를 보여주기 위해, `Text` 대신 `ListView` 를 사용한다.

많은 양의 데이터를 연속적으로 보여주고 싶을 때는 `Row - Col` 은 적절하지 않기 때문이다.

`ListView` 는 버전이 많은데 beginner 버전부터 사용해본다.

```dart
...
body: FutureBuilder(
        future: webtoons,
        builder: (context, snapshot) {
          if (snapshot.hasData) {
            return ListView(
              children: [
                for(var webtoon in snapshot.data!) Text(webtoon.title)
              ]
            )
          }
          ...
        },
      ),
```

위처럼 코드를 짜면 비효율적이다. `ListView` 안에 넣기만 하면 나온다는 뜻으로 만든 코드이다.

최적화되지 않았기 때문에, 한번에 모든 아이템들을 로딩하고 있다.

무한 스크롤 같은 기능을 쓰면, 결국은 메모리가 죽고 말 것이다.

사용자가 보고있는 사진, 섹션만 로딩해야 한다.

그래서 다른 종류의 `ListView` 를 사용한다.

`ListView.builder` 는 좀 더 최적화 된 `ListView` 다.

`ListView.builder` 는 사용자가 보고 있는 아이템만 build 한다. 보고있지 않은 아이템은 메모리에서 삭제한다.

`ListView.builder` 는 한번에 모든 아이템을 만드는 대신, 만들려는 아이템에 `itemBuilder` 를 실행하고 필요할 때 아이템을 만든다.

페이지네이션처럼.

`itemBuilder` 에 로그를 넣으면, 스크롤할 때 새로운 아이템인덱스가 추가되는 걸 확인할 수 있다.

`ListView.separated` 는 필수 인자를 하나 더 가지는데, `separatorBuilder` 라는 widget 을 리턴해야하는 함수다.

해당 함수는 리스트 아이템 사이에 렌더링된다. 구분자처럼.

```dart
...
body: FutureBuilder(
        future: webtoons,
        builder: (context, snapshot) {
          if (snapshot.hasData) {
            return ListView.separated(
              scrollDirection: Axis.horizontal,
              itemCount: snapshot.data!.length,
              itemBuilder: (context, index) {
                var webtoon = snapshot.data![index];
                return Text(webtoon.title);
              },
              separatorBuilder: (context, index) => const SizedBox(width: 20),
            );
          }
          return const Text('Loading....');
        },
      ),
```

<br>

## 6.8 Webtoon Card

웹툰의 표지를 보여주는 이미지를 만들기 위해, `Column: children[]` 에 `sizedBox` 와 `ListView` 를 넣으면 에러가 발생한다.

`ListView` 에 높이값이 없기 때문인데, `Column` 이 `ListView` 의 높이를 알지못해 제한없는 높이값이 넘어왔다는 뜻이다.

이를 해결하기 위해 `ListView` 에 제한된 높이를 줘야하고, `Expanded` 로 감싸서 해결한다.

`Expanded` 는 화면의 남는 공간을 차지하는 widget 이다.

`Expanded` 안에 `ListView` 를 넣으면, ListView 가 남는 공간을 채우게 된다.

```dart
...
builder: (context, snapshot) {
  if (snapshot.hasData) {
    return Column(
      children: [
        const SizedBox(
          height: 50,
        ),
        Expanded(child: makeList(snapshot))
      ],
    );
  }
}
...
```

`Image.network` 를 이용해 URL 을 통한 이미지를 가져온다.

이미지의 크기를 조절하기 위해, `Container child` 로 `Image.network` 를 옮기고 `Container` 의 너비를 설정한다.

`SizedBox` 를 이용해 이미지와 텍스트 사이의 간격을 넓힌다.

`Container` 를 사용한 이유는 해당 박스를 꾸밀 것이기 때문에 `decoration` 을 이용해서 박스를 적절하게 꾸며준다.

`clipBehavior` 속성을 이용해 `BorderRadius` 가 적용될 수 있도록 한다.

```dart
ListView makeList(AsyncSnapshot<List<WebtoonModel>> snapshot) {
    return ListView.separated(
      scrollDirection: Axis.horizontal,
      itemCount: snapshot.data!.length,
      padding: const EdgeInsets.symmetric(vertical: 10, horizontal: 20),
      itemBuilder: (context, index) {
        var webtoon = snapshot.data![index];
        return Column(
          children: [
            Container(
              width: 250,
              clipBehavior: Clip.hardEdge,
              decoration: BoxDecoration(
                borderRadius: BorderRadius.circular(15),
                boxShadow: [
                  BoxShadow(
                    blurRadius: 15,
                    offset: const Offset(10, 10),
                    color: Colors.black.withOpacity(0.3),
                  )
                ],
              ),
              child: Image.network(webtoon.thumb),
            ),
            const SizedBox(
              height: 10,
            ),
            Text(
              webtoon.title,
              style: const TextStyle(
                fontSize: 22,
              ),
            ),
          ],
        );
      },
      separatorBuilder: (context, index) => const SizedBox(width: 40),
    );
  }
```

<br>

## 6.9 Detail Screen

이미지를 클릭하면 상세 페이지로 가게 하기 위한 작업을 한다.

탭 이벤트를 감지하기 위해, `GestureDetector` 위젯을 사용한다.

`GestureDetector` 는 대부분의 동작을 감지할 수 있는데, 그 중 onTap 옵션을 사용한다.

onTap 은 버튼을 탭했을 때 발생하는 이벤트로 유저가 버튼을 클릭했다는 것을 의미한다.

해당 옵션에 들어갈 함수로 호출할 새로운 화면을 만들기 위해 `detail_screen` 위젯을 새로 만든다.

`Navigator` 를 이용해 화면을 전환한다. `Navigator` 는 `route` 를 push 할 수 있다.

그리고 중요한 점은 `Navigator` 는 애니메이션을 이용해 유저가 다른 페이지로 왔다고 느끼게 해줄 수 있다. (사실 또 다른 `StatelessWidget` 을 렌더했을 뿐인데 말이다)

`MaterialPageRoute` 를 이용해 `route` 를 만들어 push 한다.

이 `route` 는 `StatelessWidget` 일 뿐인 `DetailScreen` 을 렌더링한다.

```dart
@override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => DetailScreen(
              title: title,
              thumb: thumb,
              id: id,
            ),
            fullscreenDialog: true,
          ),
        );
      },
      ...
    );
  }
```

`DetailScreen` 은 `HomeScreen` 을 떠나기 때문에, `scaffold` 를 렌더링해야한다.

다시 그려줘야한다는 의미다.

`HomeScreen` 과 거의 동일한 `Scaffold` 를 만들어주고, '오늘의 웹툰' 대신 선택한 웹툰의 제목을 보여주도록 한다.

body 에는 이미지를 보여줄 수 있도록 Column 과 Row 를 사용하여 UI를 맞춰준다.

```dart
...
final String title, thumb, id;
...
@override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(
        elevation: 2,
        backgroundColor: Colors.white,
        foregroundColor: Colors.green,
        title: Text(
          title,
          style: const TextStyle(
            fontSize: 24,
          ),
        ),
      ),
      body: Column(
        children: [
          const SizedBox(
            height: 50,
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Container(
                width: 250,
                clipBehavior: Clip.hardEdge,
                decoration: BoxDecoration(
                  borderRadius: BorderRadius.circular(15),
                  boxShadow: [
                    BoxShadow(
                      blurRadius: 15,
                      offset: const Offset(10, 10),
                      color: Colors.black.withOpacity(0.3),
                    )
                  ],
                ),
                child: Image.network(thumb),
              ),
            ],
          ),
        ],
      ),
    );
  }
```

<br>

## 6.10 Hero

`Hero` widget 은 화면을 전환할 때, 애니메이션을 제공해준다.

Hero widget 을 두 개의 화면에 각각 사용하고, 같은 tag 를 주기만 하면된다.

기존에 동일한 이미지를 사용하던 DetailScreen 의 Container 와 WebtoonWidget 의 Container 를 Hero 위젯으로 감싸준 뒤, tag 를 해당 웹툰의 id 로 맞춰준다.

```dart
//detail_screen.dart
...
Hero(
  tag: id,
  child: Container(
    width: 250,
    clipBehavior: Clip.hardEdge,
    decoration: BoxDecoration(
      borderRadius: BorderRadius.circular(15),
      boxShadow: [
        BoxShadow(
          blurRadius: 15,
          offset: const Offset(10, 10),
          color: Colors.black.withOpacity(0.3),
        )
      ],
    ),
    child: Image.network(thumb),
  ),
),

//webtoon_widget.dart
...
Hero(
  tag: id,
  child: Container(
    width: 250,
    clipBehavior: Clip.hardEdge,
    decoration: BoxDecoration(
      borderRadius: BorderRadius.circular(15),
      boxShadow: [
        BoxShadow(
          blurRadius: 15,
          offset: const Offset(10, 10),
          color: Colors.black.withOpacity(0.3),
        )
      ],
    ),
    child: Image.network(thumb),
  ),
),
```

<br>

## 6.11 Recap

<br>

## 6.12 ApiService

새로운 URL 을 fetch 해본다. 여기서는 웹툰의 상세 정보를 가져온다.

이전과 같이 string 으로 받아온 데이터를 json 으로 바꾸기 위해, 새로운 model 을 생성한다.

```dart
// webtoon_detail_model
class WebtoonDetailModel {
  final String title, about, genre, age;

  WebtoonDetailModel.fromJson(Map<String, dynamic> json)
      : title = json['title'],
        about = json['about'],
        genre = json['genre'],
        age = json['age'];
}
...
// webtoon_episode_model
class WebtoonEpisodeModel {
  final String id, title, rating, date;

  WebtoonEpisodeModel.fromJson(Map<String, dynamic> json)
      : id = json['id'],
        title = json['title'],
        rating = json['rating'],
        date = json['date'];
}
```

`api_service` 에서 동일한 방식으로 api 를 호출하고 결괏값을 `jsonDecode` 으로 decode 한다.

그 후 위에서 만든 fromJson 으로 새로운 json 을 return 한다.

```dart
...
static Future<WebtoonDetailModel> getToonById(String id) async {
    final url = Uri.parse("$baseUrl/$id");
    final response = await http.get(url);
    if (response.statusCode == 200) {
      final webtoon = jsonDecode(response.body);
      return WebtoonDetailModel.fromJson(webtoon);
    }
    throw Error();
  }

static Future<List<WebtoonEpisodeModel>> getLatestEpisodesById(
    String id) async {
  List<WebtoonEpisodeModel> episodesInstances = [];
  final url = Uri.parse("$baseUrl/$id/episodes");
  final response = await http.get(url);
  if (response.statusCode == 200) {
    final episodes = jsonDecode(response.body);
    for (var episode in episodes) {
      episodesInstances.add(WebtoonEpisodeModel.fromJson(episode));
    }
    return episodesInstances;
  }
  throw Error();
}
```

<br>

## 6.13 Futures

`DetailScreen` 에서 새로 만든 `getToonById` 와 `getLatestEpisodesById` 을 사용할 때, id 값을 필요로 하기 때문에 `HomeScreen` 에서처럼 동일한 방법의 사용방식은 무리가 있다.

먼저 `DetailScreen` 을 `StatefulWidget` 으로 만든다.

그러면 아래에 `State` 의 `build method` 가 별개로 나뉘기 때문에, `State` 가 속한 `StatefulWidget` 의 data 를 받아올 때 `widget.data` 이런 형식으로 데이터를 받아온다.

`widget` 은 부모에게 가라는 의미다. 여기서 부모는 `DetailScreen`, `StatefulWidget` 이다.

초기화 하고 싶은 `property` 가 있지만 `constructor` 에서는 불가능하다.

이 때, `late` 타입으로 지정한뒤, `initState` 함수에서 초기화한다.

`initState` 에서는 `widget.id` 에 접근이 가능하다. 이를 활용해서 `Future` 를 초기화할 수 있다.

```dart
import 'package:flutter/material.dart';
import 'package:hello_flutter/models/webtoon_detail_model.dart';
import 'package:hello_flutter/models/webtoon_episode_model.dart';
import 'package:hello_flutter/services/api_service.dart';

class DetailScreen extends StatefulWidget {
  ...
}

class _DetailScreenState extends State<DetailScreen> {
  late Future<WebtoonDetailModel> webtoon;
  late Future<List<WebtoonEpisodeModel>> episodes;

  @override
  void initState() {
    super.initState();
    webtoon = ApiService.getToonById(widget.id);
    episodes = ApiService.getLatestEpisodesById(widget.id);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      ...
      appBar: AppBar(
        ...
        title: Text(
          widget.title,
          style: const TextStyle(
            fontSize: 24,
          ),
        ),
      ),
      ...
    );
  }
}
```

<br>

## 6.14 Detail Info

CSS 를 적용하는 것처럼, UI 를 만들어준다.

웹툰 이미지를 눌렀을 때 나타나는 상세 페이지의 간격과 크기를 조절해준다.

이 때 `SizedBox, Column, Row` 등을 이용한다.

데이터를 활용하기 위해 `FutureBuilder` 를 이용한다.

```dart
// detail_screen
...
const SizedBox(
  height: 25,
),
FutureBuilder(
  future: webtoon,
  builder: (context, snapshot) {
    if (snapshot.hasData) {
      return Padding(
        padding: const EdgeInsets.symmetric(
          horizontal: 50,
        ),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              snapshot.data!.about,
              style: const TextStyle(fontSize: 16),
            ),
            const SizedBox(
              height: 15,
            ),
            Text(
              '${snapshot.data!.genre} / ${snapshot.data!.age}',
              style: const TextStyle(fontSize: 16),
            ),
          ],
        ),
      );
    }
    return const Text("...");
  },
)
```

<br>

## 6.15 Episodes

이전 `DetailScreen` 위젯을 `Stateless` 에서 `Stateful` 위젯으로 바꾼 유일한 이유는 `initState` 메서드 때문이다.

그래야 선택한 웹툰의 id 를 인자로 받는 `getToonById` 와 `getLatestEpisodesById` 를 사용할 수 있기 때문이다.

이제 최신 에피소드들을 보여줄 새로운 `FutureBuilder` 를 만든다.

새로운 `FutureBuilder` 는 episodes 를 `future` 로 받고, `builder` 내부 함수에는 `snapshot.hasData` 가 참이면 UI 를 그리고, 거짓이면 아무것도 안그리기 위해 빈 컨테이너를 넣어준다.

`ListView` 나 `ListViewBuilder` 는 리스트가 엄청 길고 최적화가 중요한 곳에 사용하면 되고, 지금처럼 10개씩 가져오는 가벼운 경우에는 별 상관이 없다. `Column` 을 return 해주도록 한다.

가져온 데이터들을 `Column` 내부에서 뿌려준 후, 해당 데이터들을 컨테이너로 감싸서 꾸며줌과 동시에 회차로 이동할 수 있도록 버튼화 시킨다.

`body` 를 `SingleChildScrollView` 로 감싸서 화면을 벗어나는 부분을 스크롤화 시킨다.

```dart
// detail_screen
...
body: SingleChildScrollView(
  child: Padding(
    padding: const EdgeInsets.all(50),
    child: Column(
      children: [
        ...
        FutureBuilder(
          future: episodes,
          builder: (context, snapshot) {
            if (snapshot.hasData) {
              return Column(
                children: [
                  for (var episode in snapshot.data!)
                    Container(
                      margin: const EdgeInsets.only(bottom: 10),
                      decoration: BoxDecoration(
                        borderRadius: BorderRadius.circular(20),
                        color: Colors.green.shade400,
                        boxShadow: [
                          BoxShadow(
                            blurRadius: 5,
                            offset: const Offset(5, 5),
                            color: Colors.black.withOpacity(0.1),
                          ),
                        ],
                      ),
                      child: Padding(
                        padding: const EdgeInsets.symmetric(
                          vertical: 10,
                          horizontal: 20,
                        ),
                        child: Row(
                          mainAxisAlignment:
                              MainAxisAlignment.spaceBetween,
                          children: [
                            Text(
                              episode.title,
                              style: const TextStyle(
                                color: Colors.white,
                                fontSize: 16,
                              ),
                            ),
                            const Icon(
                              Icons.chevron_right_rounded,
                              color: Colors.white,
                            ),
                          ],
                        ),
                      ),
                    )
                ],
              );
            }
            return Container();
          },
        )
      ],
    ),
  ),
),
```

<br>

## 6.16 Url Launcher

사용자가 버튼을 클릭하면, 브라우저로 이동하도록 하는 기능을 구현한다.

그러기 위해 url_launcher 패키지를 설치한다.

설치 후에는 어떤 종류의 url 을 열 건지 명시해줘야한다.

http url 뿐만 아니라, sms, telephone url 도 가능하기 때문이다.

ios 의 경우, `ios/Runner/Info.plist` 경로로 가서 하단에 아래의 코드를 붙여넣기 해준다.

```plist
<key>LSApplicationQueriesSchemes</key>
<array>
  <!-- <string>sms</string> -->
  <!-- <string>tel</string> -->
  <string>https</string>
</array>
```

flutter 가 실행되는 config 파일이기 때문에 디버깅 중지 후 재실행시킨다.

메서드를 새로 만들어서 url launcher 를 사용하도록 한다.

launchUrl 은 Future 를 가져다 주는 함수이기 때문에 async - await 를 사용해야 한다.

혹은 launchUrlString 을 이용해서 url parse 과정 없이 바로 url 을 입력해줘도 된다.

```dart
onButtonTap() async {
    await launchUrlString(
        "https://comic.naver.com/webtoon/detail?titleId=$webtoonId&no=${episode.id}");
  }
```

버튼이 클릭되는 걸 감지하고 처리하기 위해, GestureDetector 를 추가한다.

episodes 를 담당하던 FutureBuilder 내부 Column 에, Container 로 버튼들이 묶여져있는 부분을 Episode widget 으로 분리한다.

```dart
// episode_widget.dart
import 'package:flutter/material.dart';
import 'package:hello_flutter/models/webtoon_episode_model.dart';
import 'package:url_launcher/url_launcher_string.dart';

class Episode extends StatelessWidget {
  const Episode({
    super.key,
    required this.episode,
  });

  final WebtoonEpisodeModel episode;

  onButtonTap() async {
    await launchUrlString('https://google.com');
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: onButtonTap,
      child: Container(
        ...
      ),
    );
  }
}
```

버튼을 눌렀을 때, `google.com` 으로 이동하는 것을 확인 후 `onButtonTap()` 내부 `launchUrlString` 경로를 웹툰으로 바꿔준다.

```dart
...
onButtonTap() async {
  await launchUrlString("https://comic.naver.com/webtoon/detail?titleId=$webtoonId&no=${episode.id}");
}
...
```

<br>

## 6.17 Favorites

좋아요 버튼을 만들어 본다.

사용자가 하트를 눌렀던 상태가 유지되도록 하기 위해 로컬스토리지 처럼 만들어본다.

`detail_screen` 에서 `scaffold` 내부 `appBar` 에 보면 `List<Widget> 인 actions` 를 만들 수 있다.

actions 배열 내부에 IconButton 을 만든다.

아이콘에는 조건을 걸어서 좋아요를 눌렀을 때와 누르지 않았을 때 다른 아이콘을 보여줄 수 있도록 한다.

`shared_preferences` 패키지를 이용해서 휴대폰 저장소에 데이터를 담는다.

좋아요 버튼의 로직은, 먼저 좋아요를 누른 모든 ID 의 리스트를 가져온다.

그 다음 화면이 그려지면 해당 widget 의 ID 가 사용자가 좋아요를 누른 ID 목록에 있는지 확인한다.

그 과정을 통해 버튼을 조건부로 보여준다.

사용자가 좋아요 버튼을 누를 경우, 기존에 있던 좋아요를 누른 ID 리스트에서 사용자의 ID 를 더하거나 빼준다.

이를 위해 새로운 class member 를 만든다.

`late SharedPreferences prefs;`

그리고 새로 만든 initPrefs() 메서드를 initState() 안에 넣는다.

initPrefs() 내부 `prefs = await SharedPreferences.getInstance();` 코드로, 사용자의 저장소에 connection 이 만들어진다.

사용자의 저장소 내부를 검색해서 string List 가 있는지 확인하기 위해 `likedToons` 라는 key 를 이용한다.

좋아요를 누른 것을 기억하고 조건 처리하기 위해, `state` 값으로 `isLiked` 를 만들어주고 `initPrefs()` 내에서 관리한다.

다시한번 정리하자면, `핸드폰 저장소에 액세스를 얻고 -> likedToons 라는 이름의 String List 가 있는지 살펴보고 -> 있다면 웹툰의 ID 를 가지고 있는지 확인`하는 것이다.

```dart
...
Future initPrefs() async {
  prefs = await SharedPreferences.getInstance();
  final likedToons = prefs.getStringList('likedToons');
  if (likedToons != null) {
    <!-- likedToons 안에 값이 있을 경우, 그 값들 중 widget 의 ID 와 맞는게 있는지 확인한다.  -->
    if (likedToons.contains(widget.id) == true) {
      <!-- 여기서 widget.id 를 사용하는 이유는 여기는 State 고 statefulWidget 인 DetailScreen 의 ID 를 가져오기 위함이다.-->
      setState(() {
        isLiked = true;
      });
    }
  } else {
    <!-- 사용자가 처음으로 앱을 실행하면 likedToons 는 존재하지 않을 것이기 때문에 조건처리를 해준다. -->
    await prefs.setStringList('likedToons', []);
  }
}

@override
void initState() {
  super.initState();
  webtoon = ApiService.getToonById(widget.id);
  episodes = ApiService.getLatestEpisodesById(widget.id);
  initPrefs();
}
...
```

이제 이 로직을 UI 에 반영해준다.

`isLiked` 에 따라 아이콘을 조건부로 출력해주고, 아이콘을 클릭했을 때 사용할 `onHeartTap` 이라는 method 를 만든다.

```dart
...
onHeartTap() async {
    <!-- 휴대폰 저장소에서 가져온다 -->
  final likedToons = prefs.getStringList('likedToons');
  if (likedToons != null) {
    if (isLiked) {
      likedToons.remove(widget.id);
    } else {
      likedToons.add(widget.id);
    }
    <!-- 휴대폰 저장소에 저장한다 -->
    await prefs.setStringList('likedToons', likedToons);
    setState(() {
      isLiked = !isLiked;
    });
  }
}
```

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(
        elevation: 2,
        backgroundColor: Colors.white,
        foregroundColor: Colors.green,
        actions: [
          IconButton(
            onPressed: onHeartTap,
            icon: Icon(
              isLiked ? Icons.favorite : Icons.favorite_outline,
            ),
          )
        ],
        ...
      ),
      ...
    );
  }
```
