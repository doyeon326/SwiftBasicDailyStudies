# SwiftBasicDailyStudies
weekly study logs about ios using swift (ref. 꼼꼼한 재은씨의 Swift 기본편)

--------
# Chapter01 첫번째 ios앱 만들기
### 1.1 첫번째 앱, Hello World!  
   **뷰 컨트롤러(View Controller)** 는 원칙에 따라 하위에 있는 콘텐츠를 관리하고 보여주거나 숨기는 등의 구성을 조정하는 열활을 한다. 뷰 컨트롤러는 내부적으로 뷰를 포함하고 있으며 화면 전환이 발생할 때 다른 뷰 컨트롤러와 서로 통신하고 조정하는 일을 수행한다. iOS에서 뷰 컨드롤러가 하는 특별한 역활은 뷰와 리소스를 관리한다. 모든 뷰 컨트롤러는 이 역활을 해야하고 모든 뷰 컨트롤러는 UIViewController 클래스를 상속받아야 한다.   
   
   화면을 구성하고 있는 세가지 주요 객체 :  
   * UIScreen : 기기에 연결되는 물리적인 화면을 정의하는 객체
   * UIWindown : 화면 그리기 지원 도구를 제공하는 객체
   * UIView : 그리기를 수행할 객체 시트  
   "즉, 수 많은 UIView 객체가 모인 Window는 이들을 화면으로 구성하여 Screen객체에 보내고 Screen객체는 이를 물리적인 기기에 표시한다"  
   
   **스토리보드** 는 유저 인터페이스를 종합적으로 구현하는 역활을 한다. 기존의 nib나 안드로이드의 xml방식 화면 구성과 달리, 앱에 사용되는 여러 화면을 하나의 파일에 모아 설계할  수 있도록 지원하는 **UI설계용 파일 형식**이다. 스토리보드 방식은 서로 연결되는 여러 화면이 하나의 스토리보드 파일로 구성되는 방식이다.   
   > 스토리보드의 장점
   1. 전체 설계가 파일 하나에 모두 들어있기 때문에 앱의 화면 전체와 화면 사이 관계를 더 쉽고 한눈에 파악할수 있다. 
   2. 다양한 화면 전환을 세그웨이(Segueway)를 통해 손쉽고 더 짧은 코드로 다를수 있다. 
   3. 테이블 뷰를 작업할때 셀의 외형을 만드는 것이 매우 쉽다.
   4. 스토리보드 방식의 화면 설계가 개발 생산성을 매우 높여주는 중요한 기능이 될 수 있다.   
   
   **UIViewController**클래스는 UIKit 프레임워크에 정의되어 있는 클래스로서, 기본 뷰 컨트롤러를 구현하는 핵심 클래스이다. 뷰 컨트롤러를 정의하려면 반드시 이 클래스를 상속받거나 이 클래스를 상속받은 또 따른 클래스를 상속 받아야한다.   
   **viewDidLoad()** 는 부모클래스인 UIViewController클래스에 정의되어 있는 메소드로, 뷰의 로딩이 완료되었을 때 시스템에 의해 자동으로 호출**CallBack Method**된다. 따라서 리소스를 초기화 하거나 초기 화면을 구성하는 등, 처음 한번만 실행해야 하는 초기화 코드는 대부분 이 메소드 내부에 작성하면 된다. *super.viewDidLoad()* 는 부모 클래스에 정의된 viewDidLoad() 메소드의 내용도 모두 실행한다는 의미다. 
   
### 1.2 시작 화면 제어하기  
   **Launch Screen/Splash**는 단말기에서 앱이 처음 실행될 때 주요 데이터를 초기화할 수있는 시간을 벌어주는 초기 시작화면이다. 스토리보드 launchScreen.storyboard 에서 확인할수 있다. 만약, 시작 화면이 표시되는 시간을 수정 하고싶으면 Appelegate.swift파일에서 수정이 가능하다.   
   **AppDelegate클래스** 앱 전체의 실행 흐름을 컨트롤하는 객체로서 앱이 처음 실행되거나 종료될 때, 혹은 백그라운드 상태로 들어가거나포그라운드 상태로 활성화될 때 호출되는 메소드(함수)들로 구성이 되어 있다.   
   ```swift
   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey : Any]? = nil) -> Bool {
     sleep(5) //프로세스의 진행을 멈춰 시작 화면이 표시 되는 시간을 늘려주는 역활
     return true
   }
```
   **Auto Layout(자동 레이아웃)** 화면 사이즈가 달라지더라도 항상 일정한 비율로 간격이 유지 될 수 있도록 돕는 기준선 역활. 
   
# Chapter02 iOS 앱의 구조와 코코아 터치 프레임워크
### 2.1 앱의 기본 구조  
  시스템프레임워크는 iOS기반의 앱이 실행되는 데에 필요한 기반 환경을 제공하고, 우리는 코드를 작성해 원하는 기능과 앱의 형태를 구현한다. 즉, 앱은 기본적으로 시스템 프레임워크에 정의된 원리에 따라 동작하지만, 이 영역을 제외한 너머지 범위에서는 커스텀 코드를 통해 원하는 기능과 유저 인터페이스를 구현 할 수 있다.     
  
**Entry Point, 시작진입점** 은 main()함수로부터 시작된다. 운영체제가 해당 애플리케이션 내부에 정의된 main()함수를 찾아 호출하면 안에 작성된 코드들이 연쇄적으로 실행된다. Object-C기반으로 Xcode를 생성하면 main()함수가 만들어지고 앱이 실행될 때 처리해야할 내용이 작성되어 있기 때문에 건드릴 필요가 없다. 이 main() 함수가 하는일은 실행 시 시스템으로부터 전달받은 두개의 인자값과 AppDelegate클래스를 이용하여 **UIApplicationMain()함수**를 호출하고, 그 **결과로 UIApplication 객체를 반환**한다. 생성된 UIApplication 객체는 UIKit프레임워크에 속해 있으므로 이후의 앱 제어권은 UIKit 프레임워크로 이관된다.   
**UIApplicationMain()함수**는 iOS앱에 속하는 부분의 엔트리 포인트라고 할 수있다. 이 함수는 앱의 핵심 객체를 생성하는 프로세스를 핸들링하고, 스토리보드 파일로부터 앱의 유저 인터페이스를 읽어들일뿐만 아니라 작성한 코드를 호출해 줌으로써 앱 생성 초기에 필요한 설정을 구현할수 있게 해준다.     

  여기서, 반환된 **UIApplication객체**는 앱의 본체라고 할 수 있는 객체로 작성한 코드나 객체, 앱의 기능이라고 생각하는 모든 것들은 다 여기에 속해있는 하위 객체라고 생각하면 된다. 역활은 이벤트 루프나 다른 높은 수준의 앱 동작을 관리할 뿐만 아니라 푸시 알림과 같은 특수한 이벤트를 커스텀 객체인 델리게이트에게 알려주기도 한다. 주로 다루기 어렵고 까다로워 서브클래싱 없이 그대로 사용한다. 그래서 **AppDelegate**이라는 대리 객체를 내세우고 커스텀 코드를 수행할수 있도록 약간의 권한을 부여한다. AppDelegate은 iOS 애플리케이션 내에서 오직 하나의 인스턴스만 생성되도록 시스템적으로 보장받고 앱에 처음 만들어질 때 객체가 생성되어 앱이 실행되는 동안 유지 되다가 종료되면 함께 소멸 하는 등 앱 전체의 생명 주기와 함께한다.  
  
전체 과정을 정리를 해보면,   
    * main() 함수가 실행된다  
    * main() 함수는 다시 UIApplicationMain()함수를 호출한다  
    * UIApplicationMain() 함수는 앱의 본체에 해당하는 UIApplication 객체를 생성한다  
    * UIApplication 객체는 Info.plist 파일을 바탕으로 앱에 필요한 데이터와 객체를 로드한다  
    * AppDelegate 객체를 생성하고 UIApplication 객체와 연결한다  
    * 이벤트 루프를 만드는 등 실행에 필요한 준비를 진행한다  
    * 실행 완료 직전 앱 델리게이트의 application(_: didFinishLaunchingWithOption:)메소드를 호출한다.    
    
반면 **Swift언어는** C기반의 언어가 아니기때문에 main.m 파일이 존재하지않으며 엔트리 포인트 역시 존재하지 않기때문에 위의 1~5번 과정을 어노테이션으로 대체한다. 
   ```swift
  import UIKit
  @UIApplicationMain
  class mainViewController: UIViewController{
  ... 
  }
```
    
### 2.2 iOS와 코코아 터치 프레임워크  
### 2.3 앱을 구성하는 핵심 객체들    
