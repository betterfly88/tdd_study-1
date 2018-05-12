# Black Jack - OOP TDD적용 창천향로님 블로그참고

### 주제 - 블랙잭 게임을 개량해서 OOP와 TDD를 적용한 프로젝트 진행 

### 블랙젝 규칙
* 딜러와 게이머 단 2명만 존재
* 카드는 조커를 제외한 52장이다. (즉, 카드는 다이아몬드,하트,스페이드,클럽 무늬를 가진 A,2~10,K,Q,J 으로 이루어져있다.)
* 2~10은 숫자 그대로 점수를, K/Q/J는 10점으로, A는 1로 계산한다. (기존 규칙은 A는 1과 11 둘다 가능하지만 여기선 1만 허용하도록 스펙아웃)
* 딜러와 게이머는 순차적으로 카드를 하나씩 뽑아 각자 2개의 카드를 소지한다.
* 게이머는 얼마든지 카드를 추가로 뽑을 수 있다.
* 딜러는 2카드의 합계 점수가 16점 이하이면 반드시 1장을 추가로 뽑고, 17점 이상이면 추가할 수 없다.
* 양쪽다 추가 뽑기 없이, 카드를 오픈하면 딜러와 게이머 중 소유한 카드의 합이 21에 가장 가까운 쪽이 승리한다.
* 단 21을 초과하면 초과한 쪽이 진다.

### 설계원칙
* 클래스 우선이 아닌, 객체의 속성과 행위가 우선이다.
    * 클래스는 객체를 추상화하는 도구일 뿐이다.
* 데이터가 아닌 메세지(행위)를 중심으로 객체를 설계해라.
    * 객체는 혼자 있을 수 없다. 다른 객체와의 협력 안에서만 존재할 수 있다.
    * 메세지를 중심으로, 해당 메세지가 어떤 객체를 필요로 하는지를 생각하자.
* 하나하나 지시하지 말고 요청해라.
    * 예를들어, 판사가 증인에게 1) 목격했던 장면을 떠올리고, 2) 떠오르는 시간을 순서대로 구성하고, 3) 말로 간결하게 표현해라 라고 요청하지 않는다. 그냥 "증언하라" 라고 요청한다.
    * 마찬가지로 객체의 설계단계에서도 책임이 있는 객체에 요청만 하도록 설계한다.
* 하나의 메소드는 하나의 일만 해야한다.
* 처음부터 완벽한 설계는 없다.
    * 설계를 코드로 구현해가는 과정에서 수정이 필요하다면 설계를 수정한다.

### 테스트 케이스나 전체적인 구조는 설계시마다 달라질 수 있다...

TEST CASE
--

#### 카드
        1. 카드 생성시에 입력된 대로 생성되는가. ok
        
#### 카드덱
        1. 52개의 사이즈 카드가 생성 되는가? (cardDeck랜덤생성) ok
        2. 카드의 점수는 1점보다 작거나 10점보다 클 수 없다. ok
        3. 에이스는 1점으로, J,Q,K는 10점으로 인식하는가? ok
        4. 카드덱의 제일 위에 있는 카드는 idx가 true 인가 ok
        5. 딜러가 한 장의 카드를 뽑았을 때 카드덱 CardDeck에서는 삭제 되어야 한다.
        6. 유저가 한 장의 카드를 뽑았을 때 생성된 CardDeck에서는 삭제 되어야 한다.

#### 규칙
        1. 점수를 측정해주는가
        2. 턴 마다 딜러의 점수가 17점 보다 크면 stand로 가정 (딜러)
        3. 턴 마다 딜러의 점수가 17점 보다 작으면 한장 더 뽑을 수 있다. (딜러)
        4. 턴 마다 딜러의 점수가 21점 보다 크면 bust 로 가정 (딜러)
        5. 딜러가 bust면 게이머 승리
        6. 턴 마다 게이머의 점수를 확인해서 bust인지 확인(게이머)
        7. 턴 마다 게이머의 점수를 확인해서 bust가 아니면 hit 할 것인지 stand 할 것인지 확인
        8. 승패를 판단해주는가
#### 딜러
        1. 16점 이하일 때 1장을 받는가
        2. 17점 이상일 때 카드를 추가로 안받는지?
        3. 카드가 한장 이상일 때는 카드를 보여준다
#### 게이머
        1. 입력에 따라 카드를 뽑고 안뽑을 수 있는가.
        2. 카드가 한장 이상일 때는 카드를 보여준다.                      