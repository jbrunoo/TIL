강의 들으며 적어둔 내용

- - - 
안드로이드 권장 dp는 8의 배수 / 작으면 4의 배수

surface 안에 속성 값 처럼 modifier까지 찾아보기

sample code + 결과물

modifider : composable의 크기, 동작, 모양을 변경하거나 사용자의 입력을 처리
(클릭, 스크롤 등)할 수 있도록 만드는 변수

column은 총 4가지 변수를 인자로 받는다.

modifier

verticalArrangement(Arrangement.Vertical 타입) : 수직 배치(Arraygement)를 설정하는 변수

horizontalAlignment(Alignment.Horizontal 타입) : 수평 정렬(Alignment)을 설정하는 변수

content : Layout 안에 들어갈 위젯을 설정하는 변수


Button 형식

Button(onClick = { /*TODO*/ }) {    }

Button 속성

onClick: () -> Unit,

modifier: Modifier = Modifier,

enabled: Boolean = true,

shape: Shape = ButtonDefaults.shape,

colors: ButtonColors = ButtonDefaults.buttonColors(),

elevation: ButtonElevation? = ButtonDefaults.buttonElevation(),

border: BorderStroke? = null,

contentPadding: PaddingValues = ButtonDefaults.ContentPadding,

interactionSource: MutableInteractionSource = remember { MutableInteractionSource() },

content: @Composable RowScope.() -> Unit

interaction은 on click 외에도 버튼을 드래그, 더블클릭 등 역할을 수행할 때 사용

- - -


@composable - 아래 함수는 일반 함수가 아닌 compose를 위한 함수다 의미

state
변수를 선언하기 위함. 전역변수 개념은 compose와 상충됨. 쓰지 않음. 없음. 더 상위 함수에 적용된 변수를 가져오는 느낌.

remember를 이용하지 않으면 setContent{}블록을 첨부터 끝까지 실행하는 Recompose가 다시 수행된다. remember를 통해 Recompose 전 State를 저장하고 Recompose 일어났을 때 복구하는 것이 필요.

fun MyButton(name: String, size: Int) {

//composable에서 변수명 적을 때 state // alt+enter -> import 2번 1번째는 remember 2번째는 get, set을 위해
var count by remember { mutableStateOf(0) }
//value 값 : 문자, 숫자, type 다 들어갈 수 있음.

}

A : Textfield, Surface
textfield https://www.jetpackcompose.net/textfield-in-jetpack-compose

B : @Composable(재사용)
C : state
D : Scrolling(Column, Row)

- - -

gradle scripts -> manifests -> android

안드로이드 화면 전환 방법 많음(자주쓰는 4가지)

activity 화면 전환

activity 위에 fragment 구성해 fragment로 전환 (화면 tab 느낌)

androidx nevigation (위 발전)

navigation compose 활용 - https://developer.android.com/codelabs/basic-android-kotlin-compose-navigation?hl=ko#0

qr앱은 웹뷰를 띄운 것.

keyword

intent startactivity

코드작성시 컴파일 버그(디버깅)

이외에 logcat


activity 개념

https://developer.android.com/guide/components/activities/intro-activitieshttps://7942yongdae.tistory.com/176

activity Lifecycle

하기 전 콜백 메소드 https://onlyfor-me-blog.tistory.com/47

// 아래 2개는 activity 간 데이터 주고받을 때 사용하는 개념 keyword

intent extra data

https://8iggy.tistory.com/256

activity Result

apply, with, let, also, run

[https://medium.com/@limgyumin/코틀린-의-apply-with-let-also-run-은-언제-사용하는가-4a517292df29](https://medium.com/@limgyumin/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%9D%98-apply-with-let-also-run-%EC%9D%80-%EC%96%B8%EC%A0%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%EA%B0%80-4a517292df29)

http://batmask.net/index.php/2021/12/10/286/

1) 객체를 ‘it’으로 쓰느냐, ‘this’를 쓰느냐, 2) 리턴값이 lambda result이냐, context object이냐에 따라 나뉜다. 4개면 되는데? extension function 형식외에 argument로 context object를 받는 ‘with’가 추가로 하나 존재한다.

- - - 

list는 sorted, reversed() 함수 사용. mutableList는 .sort(), reverse() 바로 적용 sorted()도 가능

sorted 함수(+ by with 등)
https://notepad96.tistory.com/19

Button, https://smashandroid.tistory.com/89

padding / offset, https://kotlinworld.com/194

compose keyword

Icon

DropDownMenu

1. Container

2. Navigation icon (optional)
 
4. Title (optional) --- 세개
 

5. Action items (optional)

6. Overflow menu (optional) ...세개


- - - 

data storage

앱별 저장소

공유 저장소

환경설정 preference

-비공개 데이터를 키 - 값 형태로 저장(ex) 로그인, 설정화면 등)

데이터베이스

Room 라이브러리를 활용하여 구조화된 데이터를 비공개 형태로 저장

(7년 전 나옴, java 그전엔 SQLite쓰다가 안정성을 위해 안드로이드는 room 권장)

공유저장소 제외하고 앱에서만 접근

앱 삭제하면 다 날라감(공유저장소가?)

prefrence

SharedPreference VS DataStore

SharedPreference

key - value형태 저장소 소규모 단순 데이터 관리용

고전적 사용, 간편

DataStore(3년됨)

Kotlin 코루틴, Flow를 사용해 비동기 방식으로 데이터 저장

SharedPreference 단점들을 개선해 현재 새로 추가되어 권장되는 방법

deprecated 된 코드는 쓰지말자 취소선 그어진 것

getSharedPreferences 대신

getPreferences로 할 예정(환경설정 파일이 하나만 필요해서)

apply()는 비동기적, commit은 동기적 - ui렌더링 시 일시정지될 수 있음 주의(기본 스레드에서 호출하는 것을 피해야 함)

val activity = LocalContext.current as? Activity // as는 형변환 activity context 상속 관계라 문제없음

val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE) // nullable하지 않지만 as뒤에 ? 붙여 null check 윗줄에 activity로 형변환시 실패하면 null 값 될 수 있음

- - -

android room

https://developer.android.com/training/data-storage/room?hl=ko

dependencies

괄호 없는 경우 groovy - gradle에 쓰는 groovy

괄호 있는 경우 kotlin - gradle에 쓰는 것도 kotlin으로 바뀌어 가는중

상단 sync now

kapt / ksp 둘 다 최신 기술, ksp만 씀

https://developer.android.com/studio/build/migrate-to-ksp?hl=ko

버전 x.x.x

major.minor.patch

사소한거 수정 patch up, 기능 추가 minor up, 큰 변화 major up

release note


데이터 뽑아올 때 query문 학습하기

데이터베이스를 class 정의

클래스에는 데이터베이스와 연결된 데이터 항목을 모두 나열하는 entities 배열이 포함된 @Database 주석이 달려야 합니다.

클래스는 RoomDatabase를 확장하는 추상 클래스여야 합니다.

(추상 클래스인데 roomdatabase를 상속받는다는 소리)

데이터베이스와 연결된 각 DAO 클래스에서 데이터베이스 클래스는 인수(파라미터 의미)가 0개이고 DAO 클래스의 인스턴스를 반환하는 추상 메서드를 정의해야 합니다.

@Database를 위해 ksp 라이브러리를 넣은 이유

데이터베이스 사용 (main activity 에서)
```
val context = LocalContext.current
val db = remember {
Room.databaseBuilder(
context,
AppDatabase::class.java, "contacts.db"
).build()
}
```

onclick 부분
```
val newUser = User(
uid = 0,
name = userName // 본인의 value 값.. var userName by remember {mutableStateOf ("")} 부분
)
db.userDao().insertAll(newUser) 추가
```

compose는 화면 바뀔 때마다 계속 check해야되서 remember이면 값이 변경 안되면 체크 안해서 성능 up

Cannot access database on the main thread

즉, 비동기 기능 추가해야 함

화면 바뀌는건 main 스레드

화면 값? io 스레드

돌아서 그걸 구분해주는 코루틴

val scope = rememberCoroutineScope() 추가해주고

onclick안에 inserALL을 scope로 감싸주기
```
scope.launch([Dispatchers.IO](http://dispatchers.io/)) {
db.userDao().insertAll(newUser)
}
```

database 값 보는 법

직접 불러오거나, 간편한 방법 == view -> Tool Windows -> App Inspection

값을 가져오는건 getALL 함수 참고

객체 간 관계 정의 부분은 데이터베이스 relation 부분

마이그레이션 - 데이터베이스 이전

아이디와 이름만 받겠다고 해놓은 데이터베이스를 이메일 등 다른 정보를 받는다고 할 때, 이미 있던 정보를 어떻게 할지 -> 마이그레이션 한다.
