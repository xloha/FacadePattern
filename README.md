# Facade Pattern

**퍼사드는 복잡한 시스템은 뒤단으로 숨기고, 간단한 인터페이스를 제공하는 객체**

==> "쉽게 말해서 복잡한 내부구조는 알 필요 없다"



퍼사드 패턴은 복잡한 클래스 시스템에 대해서 간단한 인터페이스를 제공해주는 디자인패턴으로 많은 클래스를 포함하는 복잡한 서브 시스템을 사용하기 위해 간단한 인터페이스를 제공합니다.

> 서브시스템은 퍼사드의 존재를 알지 못해야 함, 서브 시스템에 직접 접근하는 대신 퍼사드를 사용함
>
> 작업을 수행하기 위해 서로 긴밀히 작동하는 여러 API가 있는 경우에 퍼사드 패턴을 사용하는 것을 고려해보자

장점 : 복잡한 하위 시스템을 직접 사용하여 확장할 수 있는 기능이 제한된 단순화된 인터페이스를 제공, 클라이언트가 필요로하는 기능만 제공하면서 다른 모든 기능은 숨김

1. 복잡한 하위 시스템에 간단한 인터페이스를 제공할 수 있음
2. 클라이언트 및 기타 하위 시스템에서 하위 시스템을 분리하기 위해서
   - 시스템에 많은 종속 하위시스템이 있을 경우 사용함, 구현 세부 사항을 분리함, 종속성을 줄이고 코드를 사용하여 이해, 유지관리 및 테스트하기 쉽게 만듬
3. 하위 시스템에 대한 진입점을 정의하기 위해서
   - 서브 시스템이 상호 의존적일 때 클라이언트를 라이브러리, 프레임워크 또는 클래스 및 해당 API세트에 노출하는 대신에 퍼사드 패턴은 단순한 통합 API만 노출하여, 서브 시스템은 퍼사드를 모르고 기능을 구현함, 그들은 시스템 내에서 서로 상호작용을 함, 따라서 서브 시스템의 구현 세부 사항은 Facade API에 영향을 주지 않고 변경될 수 있음
   - 퍼사드는 구현이 아닌, 인터페이스를 다루기 때문에 변경할 필요가 없음, 코드의 유용성, 가독성 및 아키텍쳐를 개선하기 위해 추상화 계층(진입점)을 추가함



단점 : 단점이라기 보다는 지켜야하는 것은 정말 관련있는 객체와만 관계를 맺어야합니다. 왜냐하면 다른 부분의 변경이 발생할 경우 영향을 받을 수 밖에 없기 때문에 의존성을 낮추어서 관리를 용이하게 해줘야하는 것이 핵심이 됩니다.

facade객체가 모든 클래스와 결합되어서 god object가 될 수 있음

> 하나의 모듈이 다른 모듈의 내부 데이터를 직접 접근할 경우, 다른 모듈의 데이터를 수정할 수 있다는 것으로 모듈의 내부 데이터가 변경이 되면 그것에 따라 의존적인 모듈 역시 변경될 가능성이 높아진다.

예시 : 

1. DB에 접근할 수 있도록 도와주는 라이브러리 같은 것들
   1. 우리는 그 안에 라이브러리가 구현이 어떻게 되어있는지는 알 필요없고, dbConnect가 어떻게 연결하는지,,제공해주는 인터페이스만 가져다가 쓰면 되는 것임

> 어댑터 패턴과의 비교: facade는 기존 개체에 대해서 새로운 인터페이스를 정의하는 반면에 어댑터 패턴은 기존 인터페이스를 사용이 가능하도록 만드는 것으로, 어댑터는 일반적으로 하나의 객체만 wrapping하고 facade는 개체의 전체 하위 시스템과 함께 작동



>  어댑터 패턴 : 한 클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 변환함. 어댑터를 이용하면 인터페이스의 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있음
>
> ```swift
> protocol Duck {
>   func quak()
>   func fly()
> }
> 
> protocol Turkey {
>   func gobble()
>   func fly()
> }
> 
> class MallardDuck: Duck {
>   func quak() {
>     print("꽦")
>   }
>   
>   func fly() {
>     print("푸드덕")
>   }
> }
> 
> class WildTurkey: Turkey {
>   func gooble() {
>     print("고블 고블")
>   }
>   func fly() {
>     print("포닥")
>   }
> }
> 
> class TurkeyAdapter: Duck {
>   var turkey: Turkey
>   
>   init(turkey:Turkey) {
>     self.turkey = turkey
>   }
>   
>   func quak() {
>     turkey.gooble()
>   }
>   
>   func fly() {
>     turkey.fly()
>   }
> }
> 
> class DuckDrive {
>   var duck: MallardDuck
>   var turykey: WildTurkey
>   var turykeyAdapter: TurkeyAdapter = TurkeyAdapter(turkey)
>   
>   turkeyAdapter.quak() //gooble할꺼임
>   turkeyAdapter.fly() //포닥 할꺼임
> }
> ```
>
> 



디자인 패턴은 코드 재사용을 장려 할뿐만 아니라 코드를 일관되고 읽기 쉽고 느슨하게 결합되어 유지 관리 및 확장 가능하게 만들 수 있습니다. 앱에서 반복되고 일반화 된 기능을 식별 할 때 디자인 패턴 기반 코드 [를 프레임 워크에 넣어](http://iosbrain.com/blog/2018/01/13/building-swift-4-frameworks-and-including-them-in-your-apps-xcode-9/) 한 번 작성하고 더 많이 사용하는 것이 좋습니다