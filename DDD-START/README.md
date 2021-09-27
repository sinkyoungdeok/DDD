
# [1.도메인 모델 시작](./1.도메인-모델-시작)

<details> <summary> 1. 도메인 </summary>

## 1. 도메인

- 개발자 입장에서 온라인 서점은 구현해야 할 소프트웨어의 대상이 된다. 온라인 서점 소프트웨어는 온라인으로 책을 판매하는데 필요한
상품 조회, 구매, 결제, 배송추적 등의 기능을 제공해야 한다. 이때 '온라인 서점' 은 소프트웨어로 해결하고자 하는 문제 영역
즉, 도메인(domain)에 해당된다.
- 한 도메인은 다시 하위 도메인으로 나눌 수 있다.
    ![image](https://user-images.githubusercontent.com/28394879/133535540-82934f28-1bd8-4764-b8f8-dd13e502ea58.png)
    - 위 그림은 '온라인서점' 도메인의 하위 도메인이다.
    - 카탈로그 하위 도메인: 고객에게 구매할 수 있는 상품 목록 제공
    - 주문 하위 도메인: 고객의 주문을 처리
    - 혜택 하위 도메인: 쿠폰이나 특별 할인과 같은 서비스 제공
    - 배송 하위 도메인: 고객에게 구매한 상품을 전달하는 일련의 과정을 처리
    - 한 하위 도메인은 다른 하위 도메인과 연동하여 완전한 기능을 제공 (ex) 고객이 물건을 구매하면 주문, 결제, 배송, 혜택 하위 도메인의 기능과 엮임 )

- 특정 도메인을 위한 소프트웨어라고 해서 도메인이 제공해야 할 모든 기능을 구현 하는 것은 아니다.
    - 많은 온라인 쇼핑몰이 자체적으로 배송 시스템을 구축하기보다 외부 배송 업체의 시스템을 사용하고 배송추적에 필요한 기능만 일부 연동한다.
    - ![image](https://user-images.githubusercontent.com/28394879/133536165-37ee1c0a-0873-49b3-b952-a7fb9ac073b4.png)
        - 배송 도메인의 일부 기능은 자체 시스템으로 구현, 일부 기능은 외부 업체의 시스템 사용
        - 결제는 대행 업체 이용해서 처리

- 도메인마다 고정된 하위 도메인이 존재하는 것은 아니다. (소규모 쇼핑몰은 엑셀과 같은 도구를 이용해서 수작업으로 정산을 처리)

- 하위 도메인을 어떻게 구성할지 여부는 상황에 따라 달라진다.
    - 기업 고객을 대상으로 대형 장비를 판매하는곳은 온라인으로 카탈로그를 제공하는 주문서를 받는 정도만 필요 ( 온라인 결제나 배송추적과 같은 기능은 필요 X )
    - 반면에 의류나 액세서리처럼 일반 고객을 대상으로 물건을 판매한다면 카탈로그, 리뷰, 주문, 결제, 배송, 회원 기능이 필요


</details>


<details> <summary> 2. 도메인 모델 </summary>

## 2. 도메인 모델

- 특정 도메인을 개념적으로 표현한 것
- 예) 주문도메인
    - 온라인 쇼핑몰에서 주문을 하려면 상품을 몇개 살지 선택하고 배송지를 입력
    - 선택한 상품 가격을 이용해서 총 지불 금액을 계산하고 금액 지불을 위한 결제 수단 선택
    - 주문한 뒤에도 배송 전이면 배송지 주소를 변경하거나 주문을 취소

### 객체 기반 주문 도메인 모델
![image](https://user-images.githubusercontent.com/28394879/133551841-5d704060-1b00-4638-a99d-ff894e6bab21.png)
- 주문은 주문번호(orderNumber)와 지불할 총금액(totalAmounts)가 있다.
- 배송정보(Shipping)를 변경(changeShipping)할 수 있다.
- 주문을 취소(cancel)할 수 있다.
- 즉, 도메인 모델을 사용하면 여러 관계자들이 동일한 모습으로 도메인을 이해하고 도메인 지식을 공유하는데 도움이 된다.
- 도메인을 이해하려면 도메인이 제공하는 기능과 도메인의 주요 데ㅣ터 구성을 파악해야 하는데, 이런 면에서 기능과 데이터를 함께 보여주는 객체 모델은 도메인을 모델링하기에 적합하다.

### 상태 다이어그램을 이용한 주문 상태 모델링
![image](https://user-images.githubusercontent.com/28394879/133552688-c2d3960b-1e6c-4918-b2d4-6f1438bd2294.png)
- 상품 준비중 상태에서 주문을 취소하면 결제 취소가 함께 이루어진다는 것을 알 수 있다.

- 도메인을 이해하는 데 도움이 된다면 표현 방식이 무엇인지는 중요하지 않다.
    - 도메인 모델을 표현할 때 클래스 다이어그램이나 상태 다이어그램과 같은 UML 표기법만 사용해야 하는 것은 아니다.
    - 관계가 중요한 도메인이라면 그래프를 이용해서 도메인을 모델링 할 수 있다.
    - 계산 규칙이 중요하다면 수학 공식을 활용해서 도메인 모델을 만들수도 있다.

- 도메인 모델은 기본적으로 도메인 자체를 이해하기 위한 개념 모델이다.
- 개념 모델을 이용해서 바로 코드를 작성할 수 있는 것은 아니기에 구현 기술에 맞는 구현 모델이 따로 필요하다.
- 개념 모델과 구현 모델은 서로 다른 것이지만 구현 모델이 개념 모델을 최대한 따르도록 할 수는 있다.
    - 예) 객체 기반 모델을 이용해서 도메인을 표현 했다면 객체 지향 언어를 이용해서 개념 모델에 가깝게 구현할 수 있다.
    - 예) 수학적인 모델을 사용한다면 함수를 이용해서 도메인 모델과 유사한 구현 모델을 만들 수 있다.

### 하위 도메인 모델
- 도메인은 다수의 하위 도메인으로 구성
- 하위 도메인이 다루는 영역은 서로 다르기 떄문에 같은 용어라도 하위 도메인마다 의미가 달라질 수 있다.
    - 예) 카탈로그 도메인의 상품이 상품 가격, 상세 내용을 담고 있는 정보를 의미한다면 배송 도메인의 상품은 고객에게 실제 배송되는 물리적인 상품을 의미한다.
- 도메인에 따라 용어의 의미가 결정되므로, 여러 하위 도메인을 하나의 다이어그램에 모델링하면 안 된다.
    - 카탈로그와 배송 도메인 모델을 구분하지 않고 하나의 다이어그램에 함께 표시 하게 될 경우
        - 다이어그램에 표시한 '상품'은 카탈로그의 상품과 배송의 상품 의미를 함께 제공하기에, 카탈로그 도메인에서의 상품을 제대로 이해하는데 방해가 된다.
- 모델의 각 구성요소는 특정 도메인을 한정할 대 비로소 의미가 완젆해지기 때문에, 각 하위 도메인마다 별도로 모델을 만들어야 한다. (카탈로그 하위 도메인 모델과 배송 하위 도메인 모델을 따로 만들어야 한다)

</details>

<details> <summary> 3. 도메인 모델 패턴 </summary>

## 3. 도메인 모델 패턴

### 일반적인 애플리케이션의 아키텍처
![image](https://user-images.githubusercontent.com/28394879/133555540-2886ce28-8f46-49ab-a204-1d38bce84105.png)

|계층(Layer)|설명|
|------|---|
|사용자 인터페이스(UI) 또는 표현(Presentation)|사용자의 요청을 처리하고 사용자에게 정보를 보여줌. 여기서 사용자는 소프트웨어를 사용하는 사람 뿐만 아니라 외부 시스템도 사용자가 될 수 있다.|
|응용(Application)|사용자가 요청한 기능을 실행한다. 업무 로직을 직접 구현하지 않으며 도메인 계층을 조합해서 기능을 실행|
|도메인| 시스템이 제공할 도메인의 규칙을 구현|
|인프라스트럭처(infrastructure)|데이터베이스나 메시징 시스템과 같은 외부 시스템과의 연동을 처리|

- 도메인 모델은 아키텍처상의 도메인 계층을 객체 지향 기법으로 구현하는 패턴을 말한다.
- 도메인 계층은 도메인의 핵심 규칙을 구현한다.
    - 예) 주문 도메인에서의 도메인 계층
    - '출고 전에 배송지를 변경할 수 있다'는 규칙
    - '주문 취소는 배송 전에만 할 수 있다'는 규칙
- 도메인 규칙을 객체 지향 기법으로 구현하는 패턴이 도메인 모델 패턴이다.

```
public class Order {
    private OrderState state;
    private ShippingInfo shippingInfo;

    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        if (!state.isShippingChangeable()) {
            throw new illeagalStateException("can't change shipping in " + state);
        }
        this.shippingInfo = newShippingInfo;
    }
    public void changeShipped() {
        // 로직 검사
        this.state = OrderState.SHIPPED;
    }
    ...
}


public enum OrderState {
    PAYMENT_WAITING {
        public boolean isShippingChangeable() {
            return true;
        }
    },
    PREPARING {
        public boolean isShippingChangeable() {
            return true;
        }
    },
    SHIPPED, DELIVERING, DELIVERY_COMPLETED;

    public boolean isShippingChangeable() {
        return false;
    }
}
```

- 위 코드는 주문 도메인의 일부 기능을 도메인 모델 패턴으로 구현한 것이다.
- 주문 상태를 표현하는 OrderState는 배송지를 변경할 수 있는지 여부를 검사할 수 있는 isShippingChangeable() 메서드를 제공하고 있다.
- 주문 대기 중(PAYMENT_WAITING) 상태와 상품 준비 중(PREPARING) 상태의 isShippingChangeable() 메서즈는 true를 리턴한다.
- 즉, OrderState는 주문 대기 중이거나 상품 준비 중에는 배송지를 변경할 수 있다는 도메인 규칙을 구현하고 있다.
- 실제 배송지 정보를 변경하는 Order 클래스의 changeShippingInfo() 메서드는 OrderState의 isShippingChangeable() 메서드를 이용해서 변경 가능 여부를 확인
한 후 변경 가능한 경우에만 배송지를 변경한다.


```
public class Order {
    private OrderState state;
    private ShippingInfo shippingInfo;

    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        if (!state.isShippingChangeable()) {
            throw new illeagalStateException("can't change shipping in " + state);
        }
        this.shippingInfo = newShippingInfo;
    }
    public void changeShipped() {
        return state == OrderState.PAYMENT_WAITING ||
            state == OrderState.PREPARING;
    }
    ...
}


public enum OrderState {
    PAYMENT_WAITING, PREPARING, SHIPPED, DELIVERING, DELIVERY_COMPLETED;
}
```

- Order 클래스에서 changeShipped를 판단하도록 수정한 코드
- 배송지 변경이 가능한지 여부를 판단할 규칙이 주문 상태와 다른 정보를 함께 사용한다면 배송지 변경 가능 여부 판단을 OrderState만으로 할 수 없으므로
로직 구현을 Order에서 해야 할 것이다.
- 배송지 변경 가능 여부를 판단하는 기능이 Order에 있든, OrderState에 있든 중요한 점은 주문과 관련된 중요 업무 규칙을 주문 도메인 모델인 Order, OrderState에서 구현한다는 점이다.
- 핵심 규칙을 구현한 코드는 도메인 모델에만 위치하기 떄문에 규칙이 바뀌거나 규칙을 확장해야 할 때 다른 코드에 영향을 덜 주고 변경 내역을 모델에 반영할 수 있다.

> 노트
> '도메인 모델' 이란 용어는 도메인 자체를 표현하는 개념적인 모델을 의미하지만, 도메인 계층을 구현할 때
> 사용하는 객체 모델을 언급할 때에도 '도메인 모델'이란 용어를 사용한다.
> 여기에서도 도메인 계층의 객체 모델을 표현할 때 도메인 모델이라고 표현하고 있다.

### 개념 모델과 구현 모델
- 개념모델: 순수하게 문제를 분석한 결과물
- 개념모델: 데이터베이스, 트랜잭션 처리, 성능, 구현 기술과 같은 것들을 고려하고 있지 않기 떄문에 실제 코드를 작성할 때 개념 모델을 있는 그대로 사용할 수 없다.
- 그래서 개념 모델을 구현 가능한 형태의 모델로 전환하는 과정을 거치게 된다.
- 개념 모델을 만들 때 처음부터 완벽하게 도메인을 표현하는 모델을 만드는 시도를 할 수 있지만 실제로는 불가능에 가깝다.
- 프로젝트 초기에 완벽한 도메인 모델을 만들더라도 결국 도메인에 대한 새로운 지식이 쌓이면서 모델을 보완하거나 수정하는 일이 발생한다.
- 처음부터 완벽한 개념 모델을 만들기보다는 전반적인 개요를 알 수 있는 수준으로 개념 모델을 작성해야 한다.
- 프로젝트 초기에는 개요 수준의 개념 모델로 도메인에 대한 전체 윤곽을 이해하는 데 집중하고,
구현하는 과정에서 개념 모델을 구현 모델로 점진적으로 발전시켜 나가야 한다.

</details>

<details> <summary> 4. 도메인 모델 도출 </summary>

## 4. 도메인 모델 도출

- 도메인을 모델링 할때 기본이 되는 작업은 모델을 구성하는 핵심 구성요소, 규칙, 기능을 찾는 것이다.
- 이 과정은 요구사항에서 출발한다.

### 주문 도메인 요구사항
- 최소 한 종류 이상의 상품을 주문해야 한다.
- 한 상품을 한 개 이상 주문할 수 있다.
- 총 주문 금액은 각 상품의 구매 가격 합을 모두 더한 금액이다.
- 각 상품의 구매 가격 합은 상품 가격에 구매 개수를 곱한 값이다.
- 주문할 때 배송지 정보를 반드시 지정해야 한다.
- 배송지 정보는 받는 사람 이름, 전화번호, 주소로 구성된다.
- 출고를 하면 배송지 정볼르 변경 할 수 없다.
- 출고 전에 주문을 취소할 수 있다.
- 고객이 결재를 완료하기 전에는 상품을 준비하지 않는다.

### 주문 도메인 요구사항 - 분석
- 주문
    - '출고상태로 변경하기'
    - '배송지 정보 변경하기'
    - '주문 취소하기'
    - '결제완료로 변경하기'

### 주문 도메인 요구사항 - 코드
```
public class Order {
    public void changeShipped() {...}
    public void changeShippingInfo(ShippingInfo newShipping) { ... }
    public void cancel() { ... }
    public void completePayment() { ... }

}
```

### 주문 도메인 요구사항1
- 한 상품을 한 개 이상 주문할 수 있다.
- 각 상품의 구매 가격 합은 상품 가격에 구매 개수를 곱한 값이다.

### 주문 도메인 요구사항1 - 분석
- 주문 항목을 표현하는 OrderLine은 적어도 주문할 상품, 상품의 가격, 구매 개수를 포함 해야 한다.
- 각 구매 항목의 구매 가격도 제공 해야 한다.

### 주문 도메인 요구사항1 - 코드
```
public class OrderLine {
    private Product product;
    private int price;
    private int quantity;
    private int amounts;

    public OrderLine(Product product, int price, int quantity) {
        this.product = product;
        this.price = price;
        this.quantity = quantity;
        this.amounts = calculateAmounts();
    }

    private int calculateAmounts() {
        return price * quantity;
    }

    public int getAmounts() { ... }
    ...
}
```
- orderLine은 한 상품(product 필드)을 얼마에(price 필드), 몇 개 살지(count 필드)를 필드에 담고 있고
calculateAmounts 메서드로 구매 가격을 구하는 로직을 구현 하고 있다.

### 주문 도메인 요구사항2
- 최소 한 종류 이상의 상품을 주문해야 한다.
- 총 주문 금액은 각 상품의 구매 가격 합을 모두 더한 금액이다.

### 주문 도메인 요구사항2 - 분석
- 한 종류 이상의 상품을 주문할 수 있으므로 Order는 최소 한 개 이상의 OrderLine을 포함 해야 한다.
- OrderLine으로 부터 총 주문 금액을 구할 수 있다.

### 주문 도메인 요구사항2 - 코드
```
public class Order {
    private List<OrderLine> orderLines;
    private int totalAmounts;

    public Order(List<OrderLine> orderLines) {
        setOrderLines(orderLines);
    }

    private void setOrderLines(List<OrderLine> orderLines) {
        verifyAtLeastOneOrMoreOrderLines(orderLines);
        this.orderLines = orderLines;
        calculateTotalAmounts();
    }

    private void verifyAtLeastOneOrMoreOrderLines(List<OrderLine> orderLines) {
        if (orderLines == null || orderLines.isEmpty()) {
            throw new illegalArgumentException("no OrderLine");
        }
    }

    private void calculateTotalAmounts() {
        this.totalAmounts = new Money(orderLines.stream()
                .mapToInt(x -> x.getAmounts().getValue()).sum();
    }

    ... // 다른 메서드
}
```
- Order는 한 개 이상의 OrderLine을 가질 수 있으므로 Order를 생성할 때 OrderLine 목록을 List로 전달한다.
- 생성자에서 호출하는 setOrderLines() 메서드는 요구사항에 정의한 제약 조건을 검사한다.
- 요구사항에 따르면 최소 한 종류 이상의 상품을 주문해야 하므로 setOrderLines() 메서드는 verifyAtLeastOneOrMoreOrderLines() 메서드를 이용해서
OrderLine이 한 개 이상 존재하는지 검사한다.
- calculateTotalAmounts() 메서드를 이용해서 총 주문 금액을 계산한다.

```
public class ShippingInfo {
    private String receiverName;
    private String receiverPhoneNumber;
    private String shippingAddress1;
    private String shippingAddress2;
    private String shippingZipcode;

    ... 생성자, getter
}
```

### 주문 도메인 요구사항3
- '주문할 때 배송지 정보를 반드시 지정해야 한다'

### 주문 도메인 요구사항3 - 분석
- Order를 생성할 때 OrderLine의 목록뿐만 아니라 ShippingInfo도 함께 전달해야 한다.

### 주문 도메인 요구사항3 - 코드
```
public class Order {
    private List<OrderLine> orderLines;
    private int totalAmounts;
    private ShippingInfo shippingInfo;

    public Order(List<OrderLine> orderLines, ShippingInfo shippingInfo ) {
        setOrderLines(orderLines);
        setShippingInfo(shippingInfo);
    }

    private setShippingInfo(ShippingInfo shippingInfo) {
        if (shippingInfo == null)
            throw new illegalArgumentException("no ShippingInfo");
        this.shippingInfo = shippingInfo;
    }
    ...
}
```
- 생성자에서 호출하는 setShippingInfo() 메서드는 ShippingInfo가 null이면 익셉션이 발생하는데, 이렇게 함으로써
'배송지 정보 필수'라는 도메인 규칙을 구현

### 주문 도메인 요구사항4
- 출고를 하면 배송지 정보를 변경할 수 없다.
- 출고 전에 주문을 취소할 수 있다.
- 고객이 결제를 완료하기 전에는 상품을 준비하지 않는다.

### 주문 도메인 요구사항4 - 분석
- 출고 상태에 따라 배송지 정보 변경 기능과 주문 취소 기능이 제약을 받는다.
- 주문은 적어도 출고 상태를 표현할 수 있어야 한다.
- 결제 완료 전을 의미하는 상태와 결제 완료 내지 상품 준비 중이라는 상태가 필요하다.

### 주문 도메인 요구사항4 - 코드
```
public enum OrderState {
    PAYMENT_WAITING, PREPARING, SHIPPED, DELIVERING, DELIVERY_COMPLETED, CANCELED;
}
```

```
public class Order {
    private OrderState state;

    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        verifyNotYetShipped();
        setShippingInfo(newShippingInfo)
    }
    public void cancel() {
        verifyNotYetShipped();
        this.state = OrderState.CANCELED;
    }
    private void verifyNotYetShipped() {
        if (state != OrderState.PAYMENT_WAITING && state != OrderState.PREPARING)
            throw new illegalStateException("already shipped");
    }
    ...
}
```
- 배송지 변경이나 주문 취소 기능은 출고 전에만 가능하다는 제약 규칙이 있으므로 changeShippingInfo()와 cancel()
은 verifyNotYetShipped()메서드를 먼저 실행하게 했다.

> 노트
> 앞서 도메인 모델 패턴을 정리할 때에는 isShippingChangeable이라는 이름으로 제약 조건을 검사했는데 지금은
> verifyNotYetShipped라는 이름으로 변경했다. 이름을 바꾼 이유는 그 사이에 도메인을 더 잘 알게 되었기 때문이다.
> 최초에는 배송지 정보 변경에 대한 제약 조건만 파악했기 때문에 '배송지 정보 변경 가능 여부 확인'을 의미하는 isShippingChangeable라는
> 이름을 사용했다. 그런데, 요구사항을 분석하면서 배송지 정보 변경과 주문 취소가 둘다 '출고 전에 가능'하다는 제약 조건을
> 알게 되었고 이를 반영하기 위해 메서드 이름을 verifyNotYetShipped로 변경했다.



</details>

<details> <summary> 5. 엔티티와 밸류 </summary>

## 5. 엔티티와 벨류
- 도출한 모델은 크게 엔티티(Entity)와 벨류(Value)로 구분
- 앞서 요구사항 분석 과정으로 만든 모델 
  - ![image](https://user-images.githubusercontent.com/28394879/133707691-a201753b-7ccd-4d71-8b96-4ef1b810cc4f.png)
  - 크게 엔티티와 벨류로 구분된다. 
- 엔티티와 벨류를 제대로 구분해야 도메인을 올바르게 설계하고 구현할 수 있다.

> 노트
> Value타입은 우리말로 하면 값 타입으로 표현할 수 있지만
> '값'이란 단어를 여러 의미로 사용할 수 있기 때문에 
> 여기에서는 '밸류'를 사용한다.

### 엔티티 
- 큰특징은 식별자를 갖는다.
- 엔티티 객체마다 고유해서 각 엔티티는 서로 다른 식별자를 갖는다.
- 주문에서 배송지 주소가 바뀌거나 상태가 바뀌더라도 주문번호가 바뀌지 않는 것처럼 엔티티의 식별자는 바뀌지 않는다. 
- 엔티티를 생성하고 엔티티의 속성을 바꾸고 엔티티를 삭제할 때까지 식별자는 유지된다.
- 엔티티의 식별자는 바뀌지 않고 고유하기 때문에 두 엔티티 객체의 식별자가 같으면 두 엔티티는 같다고 판단할 수 있다.

### 엔티티의 식별자 생성
- 엔티티의 식별자를 생성하는 시점은 도메인의 특징과 사용한느 기술에 따라 달라진다. 
- 흔히 식별자는 다음 중 한가지의 방식으로 생성한다.
  - 특정 규칙에 따라 생성
    - 주문번호, 운송장번호, 카드번호와 같은 식별자는 특정 규칙에 따라 생성한다. 
    - 이 규칙은 도메인에 따라 다르고, 같은 주문번호라도 회사마다 다르다.
    - 흔히 사용하는 규칙은 현재 시간과 다른 값을 함꼐 조합하는 것이다.
  - UUID 사용
    - 다수의 개발언어가 UUID 생성기를 제공하고 있으므로 마땅한 규칙이 없다면 UUID를 식별자로 사용해도 된다. 
    - 자바의 경우 java.util.UUID 클래스를 사용하면 UUID를 생성할 수 있다.
    - `UUID uuid = UUID.randomUUID(); // 615f2ab9-c374-4b50-9420-2154594af151 `
  - 값을 직접 입력
    - 회원의 아이디나 이메일과 같은 식별자는 값을 직접 입력한다.
    - 사용자가 직접 입력하는 값이기 떄문에 식별자를 중복해서 입력하지 않도록 사전에 방지해야 된다.
  - 일련번호 사용(시퀀스나 DB의 자동 증가 칼럼 사용)
    - 주로 데이터베이스가 제공하는 자동 증가 기능을 사용한다.
    - 오라클을 사용한다면 시퀀스를 이용해서 자동 증가 식별을 구한다.
    - MySQL을 사용한다면 자동 증가 칼럼(auto_increament 칼럼)을 이용해서 일련번호 식별자를 생성한다.
    - 자동 증가 칼럼은 DB테이블에 데이터를 삽입해야 비로소 값을 알 수 있기 떄문에 테이블에 데이터를 추가하기 전에는 식별자를 알 수 없다. (엔티티 객체를 생성 할 때 식별자를 전달할 수 없다)
  - 식별자를 먼저 만들고 엔티티 객체를 생성할 떄 식별자를 전달 
    ```java
        //엔티티를 생성하기 전에 식별자 생성
        String orderNumber = orderRepository.generate();

        Order order = new Order(orderNumber, ...);
        orderRepository.save(order);
    ```

### 밸류 타입
- ShippingInfo 클래스는 받는 사람과 주소에 대한 데이터를 갖고 있다.
  ```java
    public class ShippingInfo {
        private String receiverName; // 받는사람
        private String receiverPhoneNumber; // 받는사람

        private String shippingAddress1; // 주소
        private String shippingAddress2; // 주소
        private String shippingZipcode; //주소
        
        // ... 생성자, getter
    } 
  ```
    - ShippingInfo 클래스의 receiverName 필드와 receiverPhoneNumber 필드는 서로 다른 두 데이터를 담고 있지만 두 필드는 개념적으로 받는 사람을 의미한다. 
    - 즉, 두 필드는 실제로 한 개의 개념을 표현하고 있다.
    - 비슷하게 shippingAddress1 필드, shippingAddress2, shippingZipcode 필드는 주소라는 하나의 개념을 표현한다.
- 밸류 타입을 개념적으로 완전한 하나르 표현할 때 사용한다.
- 예) 받는 사람을 위한 밸류 타입인 Receiver
  ```java

    public class Receiver {
        private String name;
        private String phoneNumber;

        public Receiver(String name, String phoneNumber) {
            this.name = name;
            this.phoneNumber = phoneNumber;
        }

        public String getName() {
            return name;
        }
        
        public String getPhoneNumber() {
            return phoneNumber;
        }
    }
  ```
    - Receiver는 '받는 사람' 이라는 도메인 개념을 표현한다.
    - 앞서 ShippingInfo의 receiverName 필드와 receiverPhoneNumber 필드가 필드 이름을 통해서 받는 사람을 위한 데이터라는 것을 유추한다면, Receiver는 그 자체로 받는 사람을 뜻한다.
    - 밸류 타입을 사용함으로써 개념적으로 완전한 하나를 잘 표현할 수 있다.
- 예) 주소르 위한 밸류 타입인 Address
```java
public class Address {
    private String address1;
    private String address2;
    private String zipcode;

    public Address(String address1, String address2, String zipcode) {
        this.address1 = address1;
        this.address2 = address2;
        this.zipcode = zipcode;
    }
}
```
- 밸류 타입을 이용한 ShippingInfo 클래스 
  ```java
  public class ShippingInfo {
      private Receiver receiver;
      private Address address;

      //... 생성자, get 메서드
  }
  ``` 
    - 배송정보가 받는 사람과 주소로 구성된다는 것을 쉽게 알 수 있다.
- 밸류 타입이 꼭 두개 이상의 데이터를 가질 필요는 없다.
- 의미를 명확하게 표현하기 위해 밸류 타입을 사용하는 경우도 있다.
  - 예) OrderLine
    ```java
    public class OrderLine {
        private Product product;
        private int price;
        private int quantity;
        private int amounts;
        //...
    }
    ``` 
    - OrderLine의 price와 amounts는 int 타입의 숫자를 사용하고 있지만 이들이 의미하는 값은 '돈'이다.
    - 따라서, '돈'을 의미하는 Money 타입을 만들어 사용하면 코드를 이해하는데 도움이 된다.
  - 예) OrderLine의 price를 위한 Money
    ```java
    public class Money {
        private int value;

        public Money(int value) {
            this.money = money;
        }
        
        public int getValue() {
            return this.value;
        }
    }
    ``` 
  - 예) Money를 이용한 OrderLine
    ```java
    public class OrderLine {
        private Product product;
        private Money price;
        private int quantity;
        private Money amounts;
    }
    ``` 
- 밸류 타입을 사용할 때의 또 다른 장점은 밸류 타입을 위한 기능을 추가 할 수 있다.
  - 예) Money타입은 돈 계산을 위한 기능을 추가 할 수 있다.
    ```java
    public class Money {
        private int value;

        //... 생성자, getValue()

        public Money add(Money money) {
            return new Money(this.value + money.value);
        }

        public Money multiply(int multiplier) {
            return new Money(value * multiplier);
        }
    }
    ``` 
    - Money를 사요하는 코드는 이제 '정수 타입 연산'이 아니라 '돈 계산' 이라는 의미로 코드를 작성할 수 있다.
- 밸류 객체의 데이터를 변경할 때는 기존 데이터를 변경하기보다는 변경한 데이터를 갖는 새로운 밸류 객체를 생성하는 방식을 선호한다.
  - 예) Money클래스의 add() 메서드
    ```java
    public class Money {
        private int value;

        public Money add(Money money) {
            return new Money(this.value + money.value);
        }

        // value를 변경할 수 잇는 메서드 없음
    }
    ```
- Money처럼 데이터 변경 기능을 제공하지 않는 타입을 불변(immutable)이라고 표현한다.
- 밸류 타입을 불변으로 구현하는 이유는 여러가지가 있지만 가장 중요한 이유는 안전한 코드를 작성할 수 있다는 것이다.
  - 예) OrderLine을 생성하려면 다음 코드 처럼 Money객체를 전달해야 한다.
    ```java
    Money price = ...;
    OrderLine line = new OrderLine(product, price, quantity);
    // 만약 price.setValue(0)로 값을 변경할 수 있다면?
    ``` 
  - 예) Money가 setValue()와 같은 메서드를 제공해서 값을 변경할 수 있다면? (하면안된다)
    ```java
    Money price = new Money(1000);
    OrderLine line = new OrderLine(product, price, 2); // -> [price=1000, quantity=2,amounts=2000]
    price.setValue(2000); // -> [price=2000, quantity=2, amounts=2000]
    ``` 
        - 참조 투명성과 관련된 문제가 생긴다.
  - 이런 문제가 발생하지 않도록 하려면 OrderLine생성자는 다음과 같이 새로운 Money 객체를 생성하도록 코드를 작성해야 한다.
    ```java
    public class OrderLine {
        //...
        private Money price;
        
        public OrderLine(Product product, Money price, int quantity) {
            this.product = product;
            // Money가 불변 객체가 아니라면,
            // price 파라미터가 변경될 때 발생하는 문제를 방지하기 위해
            // 데이터를 복사한 새로운 객체를 생성해야 한다.
            this.price = new Money(price.getValue());
            this.quantity = quantity;
            this.amounts = calculateAmounts();
        }
    }
    ``` 
    - Money가 불변이면 이런 코드를 작성할 필요가 없다.
- 엔티티 타입의 두 객체가 같은지 비교할 때 주로 식발져를 사용한다면 두 밸류 객체가 같은지 비교할 떄는 모든 속성이 같은지 비교해야 한다.
  ```java
  public class Receiver {
      private String name;
      private String phoneNumber;
      
      public boolean equals(Object other) {
          if(other == null) return false;
          if(this == other) return true;
          if(! (other instanceof Receiver) ) return false;
          Receiver that = (Receiver)other;
          return this.name.equals(that.name) && 
                this.phoneNumber.equals(this.phoneNumber);
      }
  }
  ``` 


### 엔티티 식별자 밸류 타입
- 엔티티 식별자의 실제 데이터는 String과 같은 문자열로 구성된 경우가 많다. (신용카드 번호 16자리 문자열, 이메일 주소 문자열 등)
- Money가 단순 숫자가 아닌 도메인의 '돈'을 의미하는 것처럼 이런 식별자는 단순한 문자열이 아니라 도메인에서 특별한 의미를 지니는 경우가 많기 떄문에 식별자를 위한 밸류 타입을 사용해서 의미가 잘 드러나도록 할 수 있다.
  - 예) 주문번호를 표현하기 위해 Order의 식별자 타입을 String대신 OrderNo 밸류타입을 사용
    ```java
    public class Order {
        // OrderNo 타입 자체로 id가 주문번호임을 알 수 있다.
        private OrderNo id;

        //...

        public OrderNo getId() {
            return id;
        }
    }
    ``` 
  - OrderNo 대신에 String 타입을 사용한다면 'id' 라는 이름만으로 해당 필드가 주문번호 인지 여부를 알 수 없다.
  - 필드의 의미가 드러나도록 하려면 'id' 라는 필드 이름 대신 'orderNo' 라는 필드 이름을 사용해야 한다.
  - 반면에, 식별자를 위해 OrderNo 타입을 만들면 타입 자체로 주문번호라는 것을 알 수 있으므로 필드 이름이 'id' 여도 실제 의미를 찾는 것은 어렵지 않다.

### 도메인 모델에 set 메서드 넣지 않기
- 도메인 모델에 get/set 메서드를 무조건 추가하는 것은 좋지 않은 버릇이다. 
- 특히 set메서드는 모데인의 핵심 개념이나 의도를 코드에서 사라지게 한다.
  - 예) Order의 메서드를 set메서드로 변경
    ```java
    public class Order {
        //...
        public void setShippingInfo(ShippingInfo newShipping) {..}
        public void setOrderState(OrderState state) {..}
    }
    ```  
    - 앞서 changeShippingInfo()가 배송지 정보를 새로 변경한다는 의미를 가졌다면 setShippingInfo()메서드는 단순히 배송지 값을 설정한다는 것을 뜻한다.
    - completePayment()는 결제를 완료했다는 의미를 갖는 반면에 setOrderState()는 단순히 주문상태 값을 설정한다는 것을 뜻한다.
    - 구현할 때에도 completePayment()는 결제 완료와 관련된 처리 코드를 함꼐 구현하기 떄문에 결제 완료와 관련된 도메인 지식을 코드로 구현하는 것이 자연스럽다.
    - setOrderState()는 단순히 상태 값만 변경할지 아니면 상태 값에 따른 다른 처리를 위한 코드를 함께 구현할지 애매하다.
    - 습관 적으로 코드를 작성하는 경우라면 필드 값만 변경하고 끝나는 경우가 많기 떄문에 상태 변경과 관련된 도메인 지식이 코드에서 사라지게 된다.
- set 메서드의 또 다른 문제는 도메인 객체를 생성할 때 완전한 상태가 아닐 수도 있다는 것이다.
  - 예) set메서드의 문제점
    ```java
    // set 메서드로 데이터를 전달하도록 구현하면
    // 처음 Order를 생성하는 시점에 order는 완전하지 않다.
    Order order = new Order();

    // set 메서드로 필요한 모든 값을 전달해야 함
    order.setOrdrLine(lines);
    order.setShippingInfo(shippingInfo);

    // 주문자(Orderer)를 설정하지 않은 상태에서 주문 완료 처리
    order.setState(OrderState.PREPARING);
    ``` 
    - 위 코드는 주문자를 설정하는 것을 누락하고 있다.
    - 주문자 정보를 담고 있는 필드인 orderer가 null인 상황에서 order.setState() 메서드로 상품 준비 중 상태로 바꾸는 것이다.
    - orderer가 정상인지 확인하기 위해 orderer가 null인지 검사하는 코드를 setState() 메서드에 위치하는 것도 맞지 않다.
- 도메인 객체가 불완전한 상태로 사용되는 것을 막으려면 생성 시점에 필요한 것을 전달해 주어야 한다. 즉, 생성자를 통해 필요한 데이터를 모두 받아야 한다.
  ```java
  Order order = new Order(orderer, lines, shippingInfo, OrderState.PREPARING);
  ``` 
  - 생성자로 필요한 것을 모두 받으므로 생성자를 호출하는 시점에 필요한 데이터가 올바른지 검사할 수 있다.
  ```java
  public class Order {
      public Order(Orderer orderer, List<OrderLine> orderLines, 
            ShippingInfo shippingInfo, OrderState state) {
                setOrderer(orderer);
                setOrderLines(orderLines);
                // ... 다른 값 설정
            }
      private void setOrderer(Orderer orderer) {
          if (orderer == null) throw new illegalArgumentException("no orderer");
          this.orderer = orderer;
      }  

      private void setOrderLines(List<OrderLine> orderLines) {
          verifyAtLeastOneOrMoreOrderLines(orderlines);
          this.orderLines = orderLines;
          calculateTotalAmounts();
      }
      
      private void verifyAtLeastOneOrMoreOrderLines(List<OrderLine> orderLines) {
          if (orderLines ==null || orderLines.isEmpty()){
              throw new illegalArgumentException("no OrderLine");
          }
      }

      private void calculateTotalAmounts() {
          this.totalAmounts = orderLines.stream().mapToInt(x -> x.getAmounts()).sum();
      }
  }

  ``` 
    - 이 코드의 set메서드는 앞서 set 메서드와 중요한 차이점이 있는데 접근 범위가 private라는점이다.
    - 이 코드에서 set메서드는 클래스 내부에서 데이터를 변경할 목적으로 사용된다.
    - private이기 떄문에 외부에서 데이터를 변경할 목적으로 set 메서드를 사용할 수 없다.
    - 불변 밸류 타입을 사용하면 자연스럽게 밸류 타입에는 set 메서드를 구현하지 않는다.
    - set 메서드를 구현해야 할 특별한 이유가 없다면 불변 타입의 장점을 살릴 수 있도록 밸류 타입은 불변으로 구현한다.

</details>

<details> <summary> 6. 도메인 용어  </summary>

## 6. 도메인 용어
- 코드를 작성할 때 도메인에서 사용하는 용어는 매우 중요하다.
- 도메인에서 사용하는 용어를 코드에 반영하지 않으면 그 코드는 개발자에게 코드의 의미를 해석해야 하는 부담을 준다.
  - 예) OrderState
    ```java
    public enum OrderState {
        STEP1, STEP2, STEP3, STEP4, STEP5, STEP6
    }
    ```  
    - 실제주문상태는 '결제대기중', '상품준비중', '출고완료됨', '배송중', '배송완료됨', '주문 취소됨' 이다.
    - 이 코드는 개발자가 전체 상태를 6단계로 보고 코드로 표현 한 것 이다.
    - 이 개발자는 Order 코드를 다음과 같이 작성할 가능성이 높다.
    ```java
    public class Order {
        public void changeShippingInfo(ShippingInfo newShippingInfo) {
            veryifyStep10rStep2();
            setShippingInfo(newShippingInfo);
        }
        private void verifyStep10rStep2() {
            if (state != OrderState.STEP1 && state != OrderState.STEP2) 
                throw new illegalStateException("already shipped");
        }
    }
    ``` 
    - 배송지 변경은 '출고 전'에 가능한데 이 코드의 verifyStep10rStep2라는 이름은 도메인의 중요 규칙이 드러나지 않는다.
    - 그저 STEP1과 STEP2인지 검사할 뿐이다. 
    - 실제 이 코드의 의미를 이해하려면 STEP1과 STEP2가 각각 '결제 대기 중' 상태와 '상품 준비중' 상태를 의미한 다는 것을 알아야 한다.
    - 기획자나 온라인 쇼핑 도메인 전문가가 개발자와의 업무 회의에서 '출고 전' 이라는 단어를 상요하면 개발자는 머릿속으로 '출고 전은 STEP1과 STEP2' 라고 도메인 지식을 코드로 해석해야 한다.
    ```java
    public enum OrderState {
        PAYMENT_WAITING, PREPARING, SHIPPED, DELIVERING, DELIVERY_COMPLETED;
    }
    ``` 
    - '출고 전은 STEP1과 STEP2' 같은 불필요한 변환 과정을 하지 않아도 된다.
    - 코드를 도메인 용어로 해석하거나 도메인 용어를 코드로 해석하는 과정이 줄어든다.
    - 코드의 가독성을 높여서 코드를 분석하고 이해하는 시간을 절약한다.
    - 도메인 용어를 사용해서 최대한 도메인 규칙을 코드로 작성하게 되므로 (의미를 변환하는과정에서 발생하는) 버그도 줄어들게 된다.
    - 도메인 용어는 좋은 코드를 만드는데 매우 중요한 요소임에 틀림없지만 국내 개발자는 이 점에 있어 불리한 면이 있다. ( 영어 떄문에 ) -> 도메인 용어를 영어로 해석하는 노력이 필요하다
      - 도메인에서 사용하는 용어의 의미를 명확하게 전달하는 영어 단어를 찾기 힘든 경우도 있고, 반대로 비슷한 의미의 영어 단어가 많으면 각 단어의 뉘앙스나 미세한 차이를 몰라서 선택하기 어려울 떄도 있다.
      - 도메인 용어의 '상태'를 코드로 표현할 때 'state'와 'status'중 어떤 단어를 사용할지 고민해야 한다.
      - '종류'를 표현하기 위해 'kind'와 'type' 중 어떤 단어가 맞는지 고심할 때도 있다.
      - 국내 개발자가 이해하기 쉽게 발음되는대로 'gubun(구분)' 과 같은 이름을 사용하기도 한다.
      - 알맞은 영어 단어를 찾는 것은 쉽지 않은 일이지만 시간을 들여 찾는 노력을 해야 한다.
      - 한영사전을 사용해서 적당한 단어를 찾는 노력을 하지 않고 도메인에 어울리지 않는 단어를 사용하면 코드는 도메인과 점점 멀어지게 된다.
    - 도메인 용어에 알맞은 단어를 찾는 시간을 아까워 하면 안된다. 

</details>

# [2.아키텍처 개요](./2.아키텍처-개요)

<details> <summary> 1. 네 개의 영역 </summary>

## 1. 네 개의 영역
- 아키텍처를 설계할 때 출현하는 전형적인 영역
  - '표현'
  - '응용'
  - '도메인'
  - '인프라스트럭처'

### 표현 영역
- 표현 영역 또는 UI 영역
- 사용자의 요청을 받아 응용 영역에 전달하고 응용 영역의 처리 결과를 다시 사용자에게 보여주는 역할
- 웹 애플리케이션을 개발할 때 많이 사용하는 스프링 MVC 프레임워크가 표현영역을 위한 기술에 해당 
- 웹 애플리케이션에서 표현 영역의 사용자는 웹 브라우저를 사용하는 사람이나, REST API를 호출하는 외부 시스템일 수 있다. 
![image](https://user-images.githubusercontent.com/28394879/134446261-7e0e79d6-73bb-4e9b-a72f-9dd7875e668b.png)
- 웹 애플리케이션에서 표현 영역은 HTTP 요청을 응용 영역이 필요로 하는 형식으로 변환해서 응용 영역에 전달하고, 응용 영역의 응답을 HTTP 응답으로 변환해서 전송한다.
- 예) 표현영역은 웹 브라우저가 HTTP 요청 파라미터로 전송한 데이터를 응용 서비스가 요구하는 형식의 객체 타입으로 변환해서 전달하고, 응용 서비스가 리턴한 결과를 JSON 형식으로 변환해서 HTTP 응답으로 웹 브라우저에 전송한다. 

### 응용 영역
- 표현 영역을 통해 사용자의 요청을 전달 받음
- 시스템이 사용자에게 제공해야 할 기능을 구현 
  - 예) '주문등록', '주문취소', '상품상세조회'
- 기능을 구현하기 위해 도메인 영역의 도메인 모델을 사용
  - 예) 주문 취소 기능을 제공하는 응용 서비스 
    ```java
    public class CancelOrderService {

        @Transactional
        public void cancelOrder(String orderId) {
            Order order = findOrderById(orderId);
            if (order == null) throw new OrderNotFoundException(orderId);
            order.cancel();
        }
        // ...
    }
    ```
  - 응용 서비스는 로직을 직접 수행하기보다는 도메인 모델에 로직 수행을 위임 
  - 위 코드도 주문 취소 로직을 직접 구현하지 않고 Order객체에 취소 처리를 위임 하고 있다. 
![image](https://user-images.githubusercontent.com/28394879/134448391-6ece8aaf-41fb-49f6-845e-87db339824f1.png)

### 도메인 영역
- 도메인 모델을 구현 
- Order, OrderLine, ShippingInfo와 같은 도메인 모델이 이영역에 위치한다. 
- 도메인의 핵심 로직을 구현
  - 예) 주문 도메인의 경우 
  - '배송지 변경'
  - '결제 완료'
  - '주문 총액 계산'

### 인프라스트럭처 영역
- 구현 기술에 대한 것을 다룸
- RDBMS 연동 처리
- 메시징 큐에 메시지를 전송하거나 수신하는 기능을 구현
- 몽고DB나 HBase를 사용해서 데이터베이스 연동을 처리 
- 예) SMTP를 이용한 메일 발송 기능을 구현, HTTP 클라이언트를 이용해서 REST API를 호출
- 논리적인 개념을 표현하기보다는 실제 구현을 다룸
![image](https://user-images.githubusercontent.com/28394879/134452096-ccefbb07-9775-4ba1-9004-06aceedf6af7.png)
- 도메인, 응용, 표현 영역은 구현 기술을 사용한 코드를 직접 만들지 않는 대신 인프라스트럭처 영역에서 제공하는 기능을 사용해서 필요한 기능을 개발한다.
- 예) 응용 영역에서 DB에 보관된 데이터가 필요하면 인프라스트럭처 영역의 DB 모듈을 사용해서 데이터를 읽어 온다.
- 예) 외부에 메일을 발생해야 하면 인프라스트럭처가 제공하는 SMTP 연동 모듈을 이용해서 메일을 발송한다. 

</details>

<details> <summary> 2. 계층 구조 아키텍처 </summary>

## 2. 계층 구조 아키텍처 
![image](https://user-images.githubusercontent.com/28394879/134459209-89490833-6dc8-40ae-9acf-4868470d13e9.png)
- 네 영역을 구성할 때 많이 사용하는 계층 구조이다. 
- 도메인의 복잡도에 따라 응용과 도메인을 분리하기도 하고 한 계층으로 합치기도 하지만 전체적인 아키텍처는 위 그림의 계층 구조를 따른다. 
- 상위 계층에서 하위 계층으로의 의존만 존재하고 하위 계층은 상위 계층에 의존하지 않는다. 
- 예) 표현계층은 응용 계층에 의존하고 응용 계층이 도메인 계층에 의존하지만, 반대로 인프라스트럭처 계층이 도메인에 의존하거나 도메인이 응용 계층에 의존하지 않는다.

**전형적인 계층 구조상의 의존 관계**

![image](https://user-images.githubusercontent.com/28394879/134459868-1ee24106-8de9-4aad-b5a9-6ec7857a65a0.png)
- 구현의 편리함을 위해 계층구조를 유용하게 적용 
- 응용 계층은 바로 아래 계층인 도메인 계층에 의존하지만 외부 시스템과의 연봉을 위해 아래 계층인 인프라스트럭처 계층의 의존하기도 한다. 
- 도메인과 응용계층은 룰 엔진과 DB 연동을 위해 같이 인프라스트럭처 모듈에 의존하게 된다. 
- 응용 영역과 도메인 영역은 DB나 외부 시스템 연동을 위해 인프라스트럭처의 기능을 사용하므로 이런 계층 구조를 사용하는 것은 직관적으로 이해하기 쉽다.
- 하지만, 표현, 응용, 도메인 계층이 상세한 구현 기술을 다루는 인프라스트럭처 계층에 종속된다. 
- 예) 도메인의 가격 계산 규칙 
  - 할인 금액 계산 로직이 복잡해지면 객체 지향으로 로직을 구현하는 것보다 룰 엔진을 사용하는 것이 더 알맞을 때가 있다. 
  - Drools라는 룰 엔진을 사용해서 로직을 수행할 수 있는 인프라스트럭처 영역의 코드 
  - evalutate() 메서드에 값을 주면 별도 파일로 작성한 규칙을 이용해서 연산을 수행하는 코드 정도로만 생각하고 넘어가자.
  ```java
    public class DroolsRuleEngine {
        private KieContainer kContainer;

        public DroolsRuleEngine() {
            KieServices ks = KieServices.Factory.get();
            kContainer = ks.getKieClasspathContainer();
        }

        public void evaluate(String sessionName, List<?> facts) {
            KieSession kSession = kContainer.newKieSession(sessionName);
            try {
                facts.forEach(x -> kSession.insert(x));
                kSession.fireAllRules();
            } finally {
                kSession.dispose();
            }
        }
    }
  ``` 
  - 응용 영역은 가격 계산을 위해 인프라스트럭처 영역의 DroolsRuleEngine을 사용 한다. 
  ```java
  public class CalculateDiscountService {
      private DroolsRuleEngine ruleEngine;

      public CalculateDiscountService() {
          ruleEngine = new DroolsRuleEngine();
      }

      public Money calculateDiscount(List<OrderLine> orderLines, String customerId) {
          Customer customer = findCustomer(customerId);

          MutableMoney money = new MutableMoney(0);
          List<?> facts = Arrays.asList(customer, money);
          facts.addAll(orderLines);
          ruleEngine.evalute("discountCalculation", facts);
          return money.toImmutableMoney();
      }
      //...
  }
  ``` 
  - CalculateDiscountService가 동작은 하겠지만 이 코드는 두가지 문제를 안고 있다.
    1.  테스트 어려움 
        -  CalculateDiscountService만 테스트하기 어렵다. 
        -  CalculateDiscountService를 테스트하려면 RuleEngine이 완벽하게 동작해야 한다.
        -  RuleEngine 클래스와 관련 설정 파일을 모두 만든 이후에 비로소 CalculateDiscountService가 올바르게 동작하는지 확인할 수 있다.
    2.  기능 확장의 어려움
        ```java
        public class CalculateDiscountService {
            private DroolsRuleEngine ruleEngine;

            public CalculateDiscountService() {
                ruleEngine = new DroolsRuleEngine();
            }

            public Money calculateDiscount(List<OrderLine> orderLines, String customerId) {
                Customer customer = findCustomer(customerId);

                MutableMoney money = new MutableMoney(0); // Drools에 특화된 코드: 연관결과를 받기 위해 추가한 타입
                List<?> facts = Arrays.asList(customer, money); // Drools에 특화된 코드: 룰에 필요한 데이터(지식)
                facts.addAll(orderLines); // Drools에 특화된 코드: 룰에 필요한 데이터(지식)
                ruleEngine.evalute("discountCalculation", facts); // discountCalculation => Drools에 특화된 코드: Drools의 세션 이름 
                return money.toImmutableMoney();
            }
        }
        ```
        -  코드만 보면 Drools가 제공하는 타입을 직접 사용하지 않으므로 CalculateDiscountService가 Drools 자체에 의존하지 않는다고 생각할 수 있다. 
        -  하지만, `discountCalculation` 문자열은 Drools의 세션 이름을 의미한다. 따라서, Drools의 세션 이름을 변경하면 CalculateDiscountService의 코드도 함께 변경해야 한다. 
        -  MutableMoney는 룰 적용 결과값을 보관하기 위해 추가한 타입인데 다른 방식을 사용했다면 필요 없는 타입이다.
 - 이처럼 CalculateDiscountService가 겉으로는 인프라스트럭처의 기술에 직접적인 의존을 하지 않는 것처럼 보여도 실제론느 Drools라는 인프라스트럭처 영역의 기술에 완전하게 의존하고 있다.
 - 이런 상황에서 Drools가 아닌 다른 구현 기술을 사용하려면 코드의 많은 부분을 고쳐야 한다.
 - '테스트 어려움', '기능 확장의 어려움' 을 해소하려면 어떻게 해야 할까? 답은 DIP를 적용하면 된다.  

</details>

<details> <summary> 3. DIP </summary>

## 3. DIP
![image](https://user-images.githubusercontent.com/28394879/134463969-c5c2ac6b-0e5f-4351-846c-7aa64c390442.png)
- 가격 할인 계싼을 하려면 왼쪽과 같이 고객 정보를 구해야 하고, 구한 고객 정보와 주문 정보를 이용해서 룰을 실행해야 한다. 
- 여기서 CalculateDiscountService는 고수준 모듈이다.

### 고수준 모듈 
- 고수준 모듈: 의미 있는 단일 기능을 제공하는 모듈
  - 예) CalculateDiscountService는 '가격 할인 계산' 이라는 기능을 구현
- 고수준 모듈의 기능을 구현하려면 여러 하위 기능이 필요하다.
  - 예) 가격 할인 계산 기능을 구현하려면 고객 정보를 구해야하고 룰을 실행해야하는데 이 두 기능이 하위 기능이다.

### 저수준 모듈 
- 저수준 모듈: 하위 기능을 실제로 구현한 것
  - 예) JPA를 이용해서 고객 정보를 읽어오는 모듈과 Drools로 룰을 실행하는 모듈이 저수준 모듈
- 고수준 모듈이 제대로 동작하려면 저수준 모듈을 사용해야 한다.
- 고수준 모듈이 저수준 모듈을 사용하면 앞서 계층 구조 아키텍처에서 언급했던 두가지 문제(구현 변경과 테스트가 어려움)가 발생한다.

### DIP
- 저수준 모듈이 고수준 모듈에 의존하도록 바꿈으로써 두가지 문제(구현 변경과 테스트가 어려움)을 해결함 
- 고수준 모듈을 구현하려면 저수준 모듈을 사용해야 하는데, 반대로 저수준 모듈이 고수준 모듈에 의존하도록 하려면 어떻게 해야 할까? ==> 추상화한 인터페이스 
- CalculateDiscountService 입장에서 봤을 때 룰 적용을 Drools로 구현했는지, 자바로 직접 구현했는지는 중요하지 않다. 
- 단지, '고객 정보와 구매 정보에 룰을 적용해서 할인 금액을 구한다'는 것이 중요할 뿐이다. 이를 추상화한 인터페이스는 다음과 같다.
```java
public interface RuleDiscounter {
    public Money applyRules(Customer customer, List<OrderLine> orderLines);
}
``` 

- CalculateDiscountService가 RuleDiscounter를 이용한 코드 
```java
public class CalculateDiscountService {
    private RuleDiscounter ruleDiscounter;

    public CalculateDiscountService(RuleDiscounter ruleDiscounter) {
        this.ruleDiscounter = ruleDiscounter;
    }

    public Money calculateDiscount(List<OrderLine> orderLines, String customerId) {
        Customer customer = findCustomer(customerId);
        return ruleDiscounter.applyRules(customer, orderLines);
    }
    //...
}
``` 
- CalculateDiscountService는 Drools에 의존하는 코드를 포함하고 있지 않다. 
- 단지, RuleDiscounter가 룰을 적용한다는 것만 안다.
- 실제 RuleDiscounter의 구현 객체는 생성자를 통해서 전달 받는다. 
- 룰 적용을 구현한 클래스는 RuleDiscounter 인터페이스를 상속받아 구현한다. Drools 관ㄹ녀 코드를 이해할 필요는 없고, 상속받아 구현한다는 것만 이해하면 된다.
```java
public class DroolsRuleDiscounter implements RuleDiscounter {
    private KieContainer kContainer;

    public DroolsRuleDiscounter() {
        KieServices ks = KieServices.Factory.get();
        kContainer = ks.getKieClasspathContainer();
    }

    @Override
    public Money applyRule(Customer customer, List<OrderLine> orderLines) {
        KieSession kSession = kContainer.newKieSession("discountSession");
        try {
            //...
            kSession.fireAllRules();
        } finally {
            kSession.displose();
        }
        return money.toImmutableMoney(); 
    }
}
``` 

![image](https://user-images.githubusercontent.com/28394879/134466307-b732fbe8-7e6c-4932-9f4b-8e97cd55889d.png)
- DIP를 적용한 구조
- CalculateDiscountService는 더이상 구현 기술인 Drools에 의존하지 않는다.
- '룰을 이용한 할인 금액 계산'을 추상화한 RuleDiscounter 인터페이스에 의존할 뿐이다. 
- '룰을 이용한 할인 금액 계산'은 고수준 모듈의 개념이므로 RuleDiscounter 인터페이스는 고수준 모듈에 속한다. 
- DroolsRuleDiscounter는 고수준의 하위 기능인 RuleDiscounter를 구현한 것이므로 저수준 모듈에 속한다.    

![image](https://user-images.githubusercontent.com/28394879/134466814-9e554aae-4477-4102-9814-4f4846614335.png)
- 저수준 모듈이 고수준 모듈에 의존(상속은 의존의 다른 형태)
- 고수준 모듈이 저수준 모듈을 사용하려면 고수준 모듈이 저수준 모듈에 의존해야 하는데, 반대로 저수준 모듈이 고수준 모듈에 의존한다고 해서 이를 DIP(dependency Inversion Principle, 의존 역전 원칙) 이라 부른다. 

### 구현 기술 교체 예시 (구현 변경 어려움 해결)
**기존 기술 예시**

```java
// 사용할 저수준 객체 생성
RuleDiscounter ruleDiscounter = new DroolsRuleDiscounter();

// 생성자 방식으로 주입
CalculateDiscountService disService = new CalculateDiscountService(ruleDiscounter);
```
**구현 기술 변경**
```java
// 사용할 저수준 구현 객체 변경 
RuleDiscounter ruleDiscounter = new SimpleRuleDiscounter();

// 사용할 저수준 모듈을 변경해도 고수준 모듈을 수정할 필요가 없다. 
CalculateDiscountService disService = new CalculateDiscountService(ruleDiscounter);
```
- 의존 주입을 지원하는 스프링과 같은 프레임워크를 사용하면 설정 코드를 수정해서 쉽게 구현체를 변경할 수 있다. 


### 테스트 해결 예시 (테스트 어려움 해결)
- 테스트를 언급하기 전에 CalculateDiscounterService가 제대로 동작하려면 Customer를 찾는 기능도 구현해야 한다. 
- 이를 위한 고수준 인터페이스를 CustomerRepository라고 하자.
- CalculateDiscountService는 다음과 같이 두 인터페이스인 CustomerRepository와 RuleDiscounter를 사용해서 기능을 구현하게 된다. 
```java
public class CalculateDiscountService {
    private CustomerRepository customerRepository;
    private RuleDiscounter ruleDiscounter;

    public CalculateDiscountService (
        CustomerRepository customerRepository, RuleDiscounter ruleDiscounter) {
            this.customerRepository = customerRepository;
            this.ruleDiscounter = ruleDiscounter;
        }
    public Money calculateDiscount(OrderLine orderLines, String customerId) {
        Customer customer = findCustomer(customerId);
        return ruleDiscounter.applyRules(customer, orderLines);
    }

    private Customer findCustomer(String customerId) {
        Customer customer = customerRepository.findById(customerId);
        if (customer == null) throw new NoCustomerException();
        return customer;
    }
    //...
}
```

- CalculateDiscountService가 제대로 동작하는지 테스트하려면 CustomerRepository와 RuleDiscounter를 구현한 객체가 필요하다.
- 만약 CalculateDiscountService가 저수준 모듈에 직접 의존했다면 저수준 모듈이 만들어지기 전까지 테스트를 할 수가 없었다. 
- 하지만, CustomerRepository와 RuleDiscounter는 인터페이스이므로 대용 객체를 사용해서 테스트를 진행할 수 있다. 
- 다음은 대용 객체를 사용해서 Customer가 존재하지 않는 경우 익셉션이 발생하는지 검증하는 테스트 코드의 예시 코드이다.
```java
public class CalculateDiscountServiceTest {
    
    @Test(expected = NoCustomerException.class);
    public void noCustomer_thenExceptionShouldBeThrown() {
        // 테스트 목적의 대용 객체
        CustomerRepository stubRepo = mock(CustomerRepository.class);
        when(stubRepo.findById("noCustId")).thenReturn(null);

        RuleDiscounter stubRule = (cust, lines) -> null;

        // 대용 객체를 주입받아 테스트 진행
        CalculateDiscountService calDisSvc = new CalculateDiscountService(stubRepo, stubRule);
        calDisSvc.calculateDiscount(someLines, "noCustId");
    }
}
``` 
- stubRepo와 stubRule은 각각 CustomerRepository와 RuleDiscounter의 대용 객체이다.
- stubRepo는 Mockito라는 Mock 프레임워크를 이용해서 대용 객체를 생성했고, stubRule은 메서드가 한 개여서 람다식을 이용해서 객체를 생성했다.
- 두 대용 객체는 테스트를 수행하는 데 필요한 기능만 수행한다.
- stubRepo의 경우 findById("noCustId")를 실행하면 null을 리턴하는데, calDisSvc를 생성할 때 생성자로 stubRepo를 주입받는다.
- 따라서, calDisSvc.calculateDiscount(someLines, "noCustId") 코드를 실행하면 CalculateDiscountService의 findById() 메서드에서 실행하는 customerRepository.findById(customerId) 코드는 null을 리턴하고 결과적으로 NoCustomerException을 발생시킨다. 
- CustomerRepository와 RuleDiscounter의 실제 구현 클래스가 없어도 CalculateDiscountService를 테스트할 수 있음을 보여준다. 
- 실제 구현 대신 스텁이나 Mock과 같은 테스트 목적의 대용 객체를 사용해서 거의 모든 상황을 테스트할 수 있다. 
- 이렇게 실제 구현 없이 테스트를 할 수 있는 이유는 DIP를 적용해서 고수준 모듈이 저수준 모듈에 의존하지 않도록 했기 때문이다.
- 고수준 모듈인 CalculateDiscountService는 저수준 모듈에 직접 의존하지 않기 떄문에 RDBMS를 이용한 CustomerRepository 구현 클래스와 Drools를 이용한 RuleDiscounter 구현 클래스가 없어도 테스트 대용 객체를 이용해서 거의 모든 기능을 테스트할 수 있는 것이다.

### DIP 주의사항
- DIP를 잘못 생각하면 단순히 인터페이스와 구현 클래스를 분리하는 정도로 받아들일 수 있다.
- DIP의 핵심은 고수준 모듈이 저수준 모듈에 의존하지 않도록 하기 위함이다.

**잘못된 DIP 적용 예시**

![image](https://user-images.githubusercontent.com/28394879/134473367-9ae5ee28-ecfc-4c15-b8ef-6a38b78ad7aa.png)
- DIP를 적용한 결과 구조만 보고 저수준 모듈에서 인터페이스를 추출하는 경우이다.
- 이 구조에서 도메인 영역은 구현 기술을 다루는 인프라스트럭처 영역에 의존하고 있다. 
- 즉, 여전히 고수준 모듈이 저수준 모듈에 의존하고 있는 것이다.
- RuleEngine 인터페이스는 고수준 모듈인 도메인 관점이 아니라 룰 엔진이라는 저수준 모듈 관점에서 도출한 것이다.
- DIP를 적용할 때 하위 기능을 추상화한 인터페이스는 고수준 모듈 관점에서 도출한다.
- CalculateDiscountService 입장에서 봤을 때 할인 금액을 구하기 위해 룰 엔진을 사용하는지, 직접 연산하는지 여부는 중요하지 않다.
- 단지 규칙에 따라 할인 금액을 계산한다는 것이 중요할 뿐이다. 
- 즉, '할인 금액 계산'을 추상화한 인터페이스는 저수준 모듈이 아닌 고수준 모듈에 위치한다. 

**하위 기능을 추상화한 인터페이스가 고수준 모듈에 위치한 제대로된 DIP 적용 예시**

![image](https://user-images.githubusercontent.com/28394879/134473847-7b92d97c-89fb-46f2-b548-f842b5ef423d.png)


### DIP와 아키텍처 
**아키텍처 수준에서 DIP를 적용하면 인프라스트럭처 영역이 응용 영역과 도메인 영역에 의존하는 구조가 된다**

![image](https://user-images.githubusercontent.com/28394879/134475146-8d08e3f7-db8d-4b3c-9caf-16bffc334ad4.png)
- 인프라스트럭처 영역은 구현 기술을 다루는 저수준 모듈이고, 응용 영역과 도메인 영역은 고수준 모듈이다. 
- 인프라스트럭처 계층의 가장 하단에 위치하는 계층형 구조와 달리 아키텍처에 DIP를 적용하면 인프라스트럭처 영역이 응용 영역과 도메인 영역에 의존(상속)하는 구조가 된다. 
- 인프라스트럭처에 위치한 클래스가 도메인이나 응용 영역에 정의한 인터페이스를 상속받아 구현하는 구조가 되므로 도메인과 응용 영역에 대한 영향을 주지 않거나 최소화 하면서 구현 기술을 변경하는 것이 가능하다.

**구현 기술을 변경하는것이 쉬운 DIP 대한 예시** 

![image](https://user-images.githubusercontent.com/28394879/134475925-7cf8e0f6-8b2a-4495-9291-c74e2e9b1341.png)
- 인프라스트럭처 영역의 EmailNotifier 클래스는 응용 영역의 Notifier인터페이스를 상속받고 있다. 
- 주문 시 통지 방식에 SMS를 추가해야 한다는 요구사항이 들어왔을 경우 응용 영역의 OrderService는 변경할 필요가 없다.
  - 두 통지 방식을 함께 제공하는 Notifier 구현 클래스를 인프라스트럭처 영역에 추가하면 된다.
  - 비슷하게 Mybatis 대신 JPA를 구현 기술로 사용하고 싶다면 JPA를 이용한 OrderRepository 구현 클래스를 인프라스트럭처 영역에 추가하면 된다. 

**바로 위의 DIP그림에서 구현체를 변경했을 경우**

![image](https://user-images.githubusercontent.com/28394879/134476389-56d2873a-ead2-4ccd-be83-30d36b3286e9.png)
- DIP를 적용하면 응용 영역과 도메인 영역에 영향을 최소화하면서 구현체를 변경하거나 추가할 수 있다. 

</details>

<details> <summary> 4. 도메인 영역의 주요 구성요소 </summary>

## 4. 도메인 영역의 주요 구성요소 
- 도메인 영역의 모델은 도메인의 주요 개념을 표현하며 핵심이 되는 로직을 구현한다.

**표) 도메인 영역의 주요 구성요소**
|요소|설명|
|---|-------|
|엔티티 ENTITY|고유의 식별자를 갖는 객체로 자신의 라이프사이클을 갖는다. 주문(Order), 회원(Member), 상품(Product)과 같이 도메인의 고유한 개념을 표현한다. 도메인 모델의 데이털르 포함하며 해당 데이터와 관련된 기능을 함께 제공한다.|
|밸류 VALUE|고유의 식별자를 갖지 않는 객체로 주로 개념적으로 하나인 도메인 객체의 속성을 표현할 때 사용된다. 배송지 주소를 표현하기 위한 주소(Address)나 구매 금액을 위한 금액(Money)과 같은 타입이 밸류 타입이다. 엔티티의 속성으로 사용될 뿐만 아니라 다른 밸류 타입의 속성으로도 사용될 수 있다.|
|애그리거트 AGGREGATE|애그리거트는 관련된 엔티티와 뺄류 객체를 개념적으로 하나로 묶은 것이다. 예를 들어, 주문과 관련된 Order엔티티, OrderLine 밸류, Orderer 밸류 객체를 '주문'애그리거트로 묶을 수 있다.|
|리포지터리 REPOSITORY|도메인 모델의 영속성을 처리한다. 예를들어, DBMS 테이블에서 엔티티 객체를 로딩하거나 저장하는 기능을 제공한다.|
|도메인 서비스 DOMAIN SERVICE|특정 엔티티에 속하지 않은 도메인 로직을 제공 한다. '할인 금액 계산'은 상품, 쿠폰, 회원 등급, 구매 금액 등 다양한 조건을 이용해서 구현하게 되는데, 이렇게 도메인 로직이 여러 엔티티와 밸류를 필요로 할 경우 도메인 서비스에서 로직을 구현한다.|

### 엔티티와 밸류
- 도메인 모델의 엔티티와 DB 관계형 모델의 엔티티는 다르다. (같지 않다)
- DB관계형 모델의 엔티티는 데이터만 제공하지만, 도메인 모델의 엔티티는 데이터와 함께 도메인 기능을 함께 제공한다. 
  - 예) 주문을 표현하는 엔티티는 주문과 관련된 데이터뿐만 아니라 배송지 주소 변경을 위한 기능을 함께 제공한다. 

```java
public class Order {
    // 주문 도메인 모델의 데이터
    private OrderNo number;
    private Orderer orderer;
    private ShippingInfo shippingInfo;
    //...

    // 도메인 모델 엔티티는 도메인 기능도 함께 제공
    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        //...
    }
}
```
- 도메인 모델의 엔티티는 단순히 데이터를 담고 있는 데이터 구조라기보다는 데이터와 함께 기능을 제공하는 객체이다. 
- 도메인 모델의 엔티티는 두 개 이상의 데이터가 개념적으로 하나인 경우 밸류 타입을 이용해서 표현할 수 있다. (RDBMS는 밸류 타입을 제대로 표현하기 힘들다)
  - 위 코드에서 주문자를 표현하는 Orderer는 밸류 타입으로 다음과 같이 주문자 이름과 이메일 데이터를 포함할 수 있다.
  ```java
  public class Orderer {
      private String name;
      private String email;
  }
  ```  

**RDBMS는 밸류를 제대로 표현하기 힘들다**
![image](https://user-images.githubusercontent.com/28394879/134623817-c899365e-0834-4756-8f83-444af1aa1d16.png)

- 왼쪽 테이블의 경우 주문자(Orderer)라는 개념이 드러나지 않고 주문자의 개별 데이터만 드러난다.
- 오른쪽 테이블의 경우 주문자 데이터를 별도 테이블에 저장했지만 이는 테이블의 엔티티에 가깝지 밸류 타입의 의미가 드러나지는 않는다.
- 반면 도메인 모델의 Orderer는 주문자라는 개념을 잘 반영하므로 도메인을 보다 잘 이해할 수 있도록 돕는다. 

**밸류 타입 데이터를 변경할 때 객체 자체를 완전히 교체한다**
```java
public class Order {
    private ShippingInfo shippingInfo;
    //...
    // 도메인 모델 엔티티는 도메인 기능도 함께 제공
    public void changeShippingInfo(ShippingInfo shippingInfo) {
        checkShippingInfoChangeable();
        setShippingInfo(newShippingInfo);
    }

    private void setShippingInfo(ShippingInfo newShippingInfo) {
        if(newShippingInfo == null) throw new IllegalArgumentException() ;
        // 밸류타입의 데이털르 변경할 때는 새로운 객체로 교체한다.
        this.ShippingInfo = newShippingInfo;
    }
}
```
- 밸류는 불변으로 구현하는것이 권장사항이다.
- 엔티티의 밸류 타입 데이터를 변경할 때 객체 자체를 완전히 교체 한다. 
- 배송지 정보를 변경하는 코드는 기존 객체의 값을 변경하지 않고 위 코드 같이 새로운 객체를 필드에 할당한다.


### 애그리거트

**애그리거트의 필요성**
- 도메인이 커질수록 개발할 도메인 모델도 커지면서 많은 엔티티와 밸류가 출현한다.
- 엔티티와 밸류 개수가 많아지면 많아 질수록 모델은 점점 더 복잡해진다.
- 도메인 모델이 복잡해지면 개발자가 전체 구조가 아닌 한 개 엔티티와 밸류에만 집중하게 되는 경우가 발생한다.
- 이때 상위 수준에서 모델을 관리하기보다 개발 요소에만 초점을 맞추다 보면 큰 수준에서 모델을 이해하지 못해 큰 틀에서 모델을 관리 할 수 없는 상황에 빠질 수 있다.
- 지도를 볼때 매우 상세하게 나온 대축적 지도를 보면 큰 수준에서 어디에 위치하고 있는지 이해하기 어려우므로 큰 수준에서 보여주는 소축척 지도를 함꼐 봐야 현재 위치를 보다 정확하게 이해할 수 있따.
- 이와 비슷하게 도메인 모델도 개발 객체뿐만 아니라 상위 수준에서 모델을 볼 수 있어야 전체 모델의 관계와 개발 모델을 이해하는데 도움이 된다. 
- 도메인 모델에서 전체 구조를 이해하는데 도움이 되는 것이 바로 애그리거트이다.
  
**애그리 거트**
- 관련 객체를 하나로 묶은 군집이다.
- 예) 주문 도메인 
  - 주문
  - 배송지정보
  - 주문자
  - 주문목록
  - 총 결제 금액 
  - 5개의 하위 모델로 구성되는데 이때 이 하위 개념을 표현한 모델을 하나로 묶어서 '주문'이라는 상위 개념으로 표현할 수 있다.
- 개별 객체가 아닌 관련 객체를 묶어서 객체 군집 단위로 모델을 바라볼 수 있게 된다.
- 개별 객체 간의 관계가 아닌 애그리거트 간의 관계로 도메인 모델을 이해하고 구현할 수 있게 되며, 이를 통해 큰 틀에서 도메인 모델을 관리할 수 있게 된다.
- 애그리거트는 군집에 속한 객체들을 관리하는 루트 엔티티를 갖는다.
- 루트엔티티
  - 애그리거트에 속해 있는 엔티티와 밸류 객체를 이용해서 애그리거트가 구현해야 할 기능을 제공
  - 애그리거트를 사용하는 코드는 애그리거트 루트가 제공하는 기능을 실행하고 애거리거트 루트를 통해서 간접적으로 애그리거트 내의 다른 엔티티나 밸류 객체에 접근하게 된다. 
  - 이는 애그리거트의 내부 구현을 숨겨서 애그리거트 단위로 구현을 캡슐화 할 수 있도록 돕는다.

**애그리거트 루트인 Order가 애그리거트에 속한 객체를 관리한다.**
![image](https://user-images.githubusercontent.com/28394879/134633979-5e762e94-62ff-49f4-b9ee-4b29b367ae31.png)
- 주문 애그리거트
- 애그리거트 루트인 Order는 주문 도메인 로직에 맞게 애그리거트의 상태를 관리한다. 
  - 예) Order의 배송지 정보 변경 기능은 배송지를 변경할 수 있는지 확인한 뒤에 배송지 정보를 변경한다.
  
**예) Order의 배송지 정보 변경 기능은 배송지를 변경할 수 있는지 확인한 뒤에 배송지 정보를 변경한다.**
```java
public class Order {
    //...
    public void changeShippingInfo(ShippingInfo newInfo) {
        checkShippinrgInfoChangeable(); // 배송지 변경 가능 여부 확인
        this.shippingInfo = newInfo;
    }
    
    private void checkShippinginfoChangeable() {
        //... 배송지 정보를 변경할 수 있는지 여부를 확인하는 도메인 규칙 구현 
    }
}
```
- checkShippingInfoChangeable() 메서드는 도메인 규칙에 따라 배송지를 변경할 수 있는지 확인한다.
  - 예) 이미 배송이 시작된 경우 익셉션을 발생하는 식으로 도메인 규칙을 구현 
- 주문 개그리거트는 Order를 통하지 않고 ShippingInfo를 변경할 수 있는 방법을 제공하지 않는다.
- 즉, 배송지를 변경하려면 루트 엔티티인 Order를 사용해야 하므로 배송지 정보를 변경할 떄에는 Order가 구현한 도메인 로직을 항상 따르게 된다.
- 애그리거트를 구현할떄는 고려할 것이 많다.
- 애그리거트를 어떻게 구현하느냐에 따라 구현이 복잡해지기도 하고 트랜잭션 범위가 달라지기도 한다.
- 또한 선택한 기술에 따라 애그리거트 구현에 제약이 생기기도 한다.
- 애그리거트의 구현에 대한 내용은 3장에서 자세히 살펴본다.

### 리포지터리
- 도메인 객체를 지속적으로 사용하려면 RDBMS, NoSQL, 로컬 파일과 같은 물리적인 저장소에 도메인 객체를 보관해야 한다.
- 이를 위한 도메인 모델이 리포지터리(repository)이다.
- 엔티티나 밸류: 요구사항에서 됴출되는 도메인 모델 / 리포지터리: 구현을 위한 도메인 모델
- 리포지터리는 애그리거트 단위로 도메인 객체를 저장하고 조회하는 기능을 정의한다.

**예) 주문 애그리거트를 위한 리포지 터리**

```java
public interface OrderRepository {
    public Order findBynumber(OrderNumber number);
    public void save(Order order);
    public void delete(Order order);
}
``` 
- OrderRepository의 메서드를 보면 대상을 찾고 저장하는 단위가 애그리거트 루트인 Order인 것을 알 수 있다.
- Order는 애그리거트에 속한 모든 객체를 포함하고 있으므로 결과적으로 애그리거트 단위로 저장하고 조회한다.
- 도메인 모델을 사용해야 하는 코드는 리포지터리를 통해서 도메인 객체를 구한 뒤에 도메인 객체의 기능을 실행하게 된다.

**예) 주문 취소 기능을 제공하는 응용 서비스는 OrderRepository를 이용해서 Order 객체를 구하고 해당 기능을 실행**
```java
public class CancelOrderService {
    private OrderRepository orderRepository;

    public void cancel(OrderNumber number) {
        Order order = orderRepository.findByNumber(number);
        if (order == null) throw new NoOrderException(number);
        order.cancel();
    }

    //... DI 등의 방식으로 OrderRepository 객체 전달 
}
```
- 도메인 모델 관점에서 OrderRepository는 도메인 객체를 영속화하는데 필요한 기능을 추상화한 것으로 고수준 모듈에 속한다.
- 기반 기술을 이용해서 OrderRepository를 구현한 클래스는 저수준 모듈로 인프라스트럭처 영역에 속한다. 

**리포지터리 인터페이스는 도메인 모델 영역에 속하며, 실제 구현 클래스는 인프라스트럭처 영역에 속한다.**
![image](https://user-images.githubusercontent.com/28394879/134641093-792e01b7-4417-444e-8500-917665513c8e.png)


- 응용 서비스는 의존 주입과 같은 방식을 사용해서 실제 리포지터리 구현 객체에 접근한다.

**스프링 프레임워크의 의존 주입 방식**
```java
@Configuration
public class OrderServiceConfig { // 응용 서비스 영역 설정
    @Autowired
    private OrderRepository orderRepository;

    @Bean
    public CancelOrderService cancelOrderService() {
        return new CancelOrderService(orderRepository);
    }
}

@Configuration
public class RepositoryConfig { // 인프라스트럭처 영역 설정
    @Bean
    public JpaOrderRepository orderRepository() {
        return new JpaOrderRepository();
    }

    @Bean
    public LocalContainerEntityManagerFactoryBean emf() {
        //...
    }

}
``` 
- 응용 서비스와 리포지터리는 밀접한 연관이 있다.
  - 응용 서비스는 필요한 도메인 객체를 구하거나 저장할 떄 리포지터리를 사용한다.
  - 응용 서비스는 트랜잭션을 관리하는데, 트랜잭션 처리는 리포지터리 구현 기술에 영향을 받는다.
- 리포지터리의 사용 주체가 응용 서비스이기 때문에 리포지터리는 응용 서비스가 필요로 하는 메소드를 제공한다. 가장 기본이 되는 메서드는 다음의 두 메서드이다.
  - 에그리거트를 저장하는 메서드
  - 에그리거트 루트 식별자로 에그리거트를 조회하는 메서드 
  - 두 메서드는 다음의 형태를 갖는다.
  ```java
  public interface SomeRepository {
      void save(Some some);
      Some findById(SomeId id);
  }
  ``` 
  - 이 외에 필요에 따라 delete(id)나 counts() 등의 메서드를 제공하기도 한다.
- 리포지터리를 구현하는 방법은 선택한 구현 기술에 따라 달라지는데 리포지터리의 구현에 대한 내용은 4장과 5장에서 살펴보도록 한다. 


</details>

<details> <summary> 5. 요청 처리 흐름 </summary>

## 5. 요청 처리 흐름
- 사용자 입장에서 봤을 때 웹 애플리케이션이나 데스크톱 애플리케이션과 같은 소프트웨어는 기능을 제공한다.
- 사용자가 애플리케이션에 기능 실행을 요청하면 그 요청을 처음 받는 영역은 표현 영역이다.
- 스프링 MVC를 사용해서 웹 애플리케이션을 구현했다면 컨트롤러가 사용자의 요청을 받아 처리하게 된다.
- 표현 영역은 사용자가 전송한 데이터 형식이 올바른지 검사하고 문제가 없다면 데이터를 이용해서 응용 서비스에 기능 실행을 위임한다. 
- 이때 표현 영역은 사용자가 전송한 데이터를 응용 서비스가 요구하는 형식으로 변환해서 전달한다.
- 웹 브라우저를 이용해서 기능 실행을 요청할 경우, 컨트롤러가 HTTP 요청 파라미터를 응용 서비스가 필요로 하는 데이터로 변환해서 응용 서비스를 실행할 때 파라미터로 전달한다.
 
**요청 처리 흐름**
![image](https://user-images.githubusercontent.com/28394879/134645891-ffd75beb-fa46-4cab-9af3-08d527ebe7eb.png)
- 응용 서비스는 도메인 모델을 이용해서 기능을 구현한다.
- 기능 구현에 필요한 도메인 객체를 리포지터리에서 가져와 실행하거나 신규 도메인 객체를 생성해서 리포지터리에 저장한다.
- 두 개 이상의 도메인 객체를 사용해서 구현하기도 한다.

**스프링의 트랜잭션 관리 기능을 이용한 트랜잭션 처리**
```java
public class CancelOrderService {
    private OrderRepository orderRepository;

    @Transaction // 응용 서비스는 트랜잭션을 관리한다.
    public void cancel(OrderNumber number) {
        Order order = orderRepository.findByNumber(number);
        if (order == null) throw new NoOrderException(number);
        order.cancel();
    }
    //...
}
```
- 예매하거나 예매 취소와 같은 기능을 제공하는 응용 서비스는 도메인의 상태를 변경하므로 변경 상태가 물리 저장소에 올바르게 반영되도록 트랜잭션을 관리해야 한다.
- 응용 서비스의 구현에 대해서는 6장에서 자세히 다룬다.

### 인프라스트럭처 개요 
- 인프라스트럭처는 표현 영역, 응용 영역, 도메인 영역을 지원한다. 
- 도메인 객체의 영속성 처리, 트랜잭션, SMTP 클라이언트, REST 클라이언트 등 다른 영역에서 필요로 하는 프레임워크, 구현 기술, 보조 기능을 지원한다.
- DIP에서 언급한 것처럼 도메인 영역과 응용 영역에서 인프라스트럭처의 기능을 직접 사용하는 것보다 이 두 영역에 정의한 인터페이스를 인프라스트럭처 영역에서 구현하는 것이 시스템을 더 유연하고 테스트하기 쉽게 만들어준다. 
- 하지만, 무조건 인프라스트럭처에 대한 의존을 없애는 것이 좋은 것은 아니다.
  - 예) 스프링을 사용할 경우 응용 서비스는 트랜잭션 처리를 위해 스프링이 제공하는 @Transactional을 사용하는 것이 편리하다. 영속성 처리를 위해 JPA를 사용할 경우 @Entity나 @Table과 같은 JPA 전용 애노테이션(Annotation)을 도메인 모델 클래스에 사용하는 것이 XML 매핑 설정을 이용하는 것 보다 편리하다.

**인프라스트럭처에 대한 의존을 일부 도메인에 넣은 코드**
```java
// 구현의 편리함을 위해 인프라스트럭처에 대한 의존을 일부 도메인에 넣은 코드 
// JPA의 @Table 애노테이션을 이용해서 엔티티틀 저장할 테이블 이름을 지정 
// XML 설정을 사용하는 것보다 편리하게 테이블 이름을 지정할 수 있다.
@Entity
@Table(name = "TBL_ORDER")
public class Order {
    //...
}
```
- 구현의 편리함은 DIP가 주는 다른 장점(변경의 유연함, 테스트가 쉬움) 만큼 중요하기 때문에 DIP의 장점을 해치지 않는 범위에서 응용 영역과 도메인 영역에서 구현 기술에 대한 의존을 가져가는 것이 현명하다.
- 응용 영역과 도메인 영역이 인프라스트럭처에 대한 의존을 완전히 갖지 않도록 시도하는 것은 자칫 구현을 더 복잡하고 어렵게 만들 수 있다.
  - 좋은 예) 스프링의 @Transactional 애노테이션
  - @Transactional을 사용하면 한줄로 트랜잭션을 처리할 수 있는데, 코드에서 스프링에 대한 의존을 없애려면 복잡한 스프링 설정을 사용해야 한다.
  - 의존을 없앴지만 특별히 테스트를 더 쉽게 할 수 있다거나 유연함을 증가시켜주지 못한다.
  - 단지 설정만 복잡해지고 개발 시간만 늘어날 뿐이다.
- 표현 영역은 항상 인프라스트럭처 영역과 쌍을 이룬다.
  - 스프링 MVC를 사용해서 웹 요청을 처리하면 스프링이 제공하는 MVC 프레임워크에 맞게 표현 영역을 구현해야 하고, Vert.x를 사용해서 REST API 서버를 구축하려면 Vert.x에 맞게 웹 요청 처리부분을 구현해야 한다.


</details>

<details> <summary> 6. 모듈 구성 </summary>

## 6. 모듈 구성
**영역별로 별도 패키지로 구성한 모듈 구조**

![image](https://user-images.githubusercontent.com/28394879/134653015-94c85889-e4bf-4ff2-9782-d07412ffcf63.png)
- 아키텍처의 각 영역은 별도 패키지에 위치한다.
- 패키지 구성 규칙에 한 개의 정답만 존재하는 것은 아니지만 영역별로 모듈이 위치한 패키지를 구성 할 수 있다.
- 여기서 com.myshop은 예시로 든 패키지이므로 알맞은 패키지로 대체하면 된다.
  
**도메인이 크면 하위 도메인별로 모듈을 나눈다**

![image](https://user-images.githubusercontent.com/28394879/134657605-0013a15d-c32a-443f-9f06-4d40bf1fbb62.png)


**하위 도메인을 하위 패키지로 구성한 모듈 구조**

![image](https://user-images.githubusercontent.com/28394879/134657118-86d15ac3-5917-441a-8061-0aa62639430f.png)

- domain 모듈은 도메인에 속한 애그리거트를 기준으로 다시 패키지를 구성한다.
- 예) 카탈로그 하위 도메인을 위한 도메인은 상품 애그리거트와 카테고리 애그리거트로 구성된다고 할 경우 domain을 두 개의 하위 패키지로 구성할 수 있다.


**etc**

- 각 애그리거트와 모델과 리포지터리는 같은 패키지에 위치시킨다.
  - 예) 주문과 관련된 Order, OrderLine, Orderer, OrderRepository 등은 com.myshop.order.domain 패키지에 위치시킨다.
- 도메인이 복잡하면 도메인 모델과 도메인 서비스를 다음과 같이 별도 패키지에 위치시킬 수도 있다.
  - com.myshop.order.domain.order: 애그리거트 위치
  - com.myshop.order.domain.service: 도메인 서비스 위치
- 응용 서비스도 다음과 같이 도메인 별로 패키지를 구분할 수 있다.
  - com.myshop.catalog.application.proudct
  - com.myshop.catalog.application.category

- 모듈 구조를 얼마나 세분화해야 하는지에 대해 정해진 규칙은 없다.
- 단지, 한 패키지에 너무 많은 타입이 몰려서 코드를 찾을 때 불편한 정도만 아니면 된다.
- 개인적으로는 한 패키지에 가능하면 10개 미만으로 타입 개수를 유지하려고 노력한다.
- 이 개수가 넘어가면 모듈을 분리하는 시도를 해본다. 
  

</details>



# [3. 애그리거트](./3.애그리거트)

<details> <summary> 1. 애그리거트 </summary>

## 1. 애그리거트

**상위 수준에서 모델을 정리하면 복잡한 도메인 모델의 관계를 이해하는데 도움이 된다**

![image](https://user-images.githubusercontent.com/28394879/134831585-7d49ef99-f4b7-458b-8e53-370fc2fbd0f8.png)
- 온라인 쇼핑몰을 위한 시스템을 개발한다면 위 그림과 같이 상위 수준 개념을 이용해서 전체 모델을 정리하면 전반적인 관계를 이해하는데 도움이 된다. 
- 주문은 회원, 상품, 결제와 관련이 있다는것을 쉽게 파악할 수 있다. 


**개별 객체 수준에서 모델을 바라보면 상위 수준에서 관계를 파악하기 어렵다**

![image](https://user-images.githubusercontent.com/28394879/134831864-05a44944-0fc9-43bd-99aa-a20631822c8e.png)
- 상위수준 모델을 개별 객체 단위로 다시 그린 그림이다. 
- 상위모델에 대한 이해 없이 위 그림만 보고 상위 수준에서 개념을 파악하려면 더 오랜 시간이 걸린다. 
- 더 많은 코드를 보고 도메인 전문가와 더 많은 대화를 나눠야 비로소 상위 수준에서 모델 간의 관계가 이해되기 시작한다. 
- 백 개 이상의 테이블을 한장의 ERD에 모두 표시하면 개별 테이블 간의 관계를 파악하느라 큰 틀에서 데이터 구조를 이해하는데 어려움을 겪게 되는 것처럼, 도메인 객체 모델이 복잡해지면 개별 구성요소 위주로 모델을 이해하게 되고 전반적인 구조나 큰 수준에서 도메인 간의 관계를 파악하기 어려워진다. 
  - 주요 도메인 개념 간의 관계를 파악하기 어렵다는 것은 곧 코드를 변경하고 확장하는 것이 어려워진다는 것을 의미한다.
  - 상위 수준에서 모델이 어떻게 엮여 있는지 알아야 전체 모델을 망가뜨리지 않으면서 추가 요구사항을 모델에 반영할 수 있는데 세부적인 모델만 이해한 상태로는 코드를 수정하기가 두렵기 때문에 코드 변경을 최대한 회피하는 쪽으로 요구사항을 협의하게 된다. 
  - 꼼수를 부려 당장 돌아가는 코드를 추가할 수는 있지만 이는 장기적인 관점에서 코드를 더 수정하기 어렵게 만들기도 한다. 


 **애그리거트는 복잡한 모델을 관리하는 기준을 제공한다.**

 ![image](https://user-images.githubusercontent.com/28394879/134832495-e9985c97-adc7-4264-8b2c-78c6d3335c09.png)
 - 복잡한 도메인을 이해하고 관리하기 쉬운 단위로 만들려면 상위 수준에서 모델을 조망할 수 있는 방법이 필요한데, 그 방법이 바로 애그리거트이다. 
   - 애그리거트는 관련된 객체를 하나의 군으로 묶어준다.
   - 수많은 객체를 애그리거트로 묶어서 바라보면 좀 더 상위 수준에서 도메인 모델 간의 관계를 파악할 수 있다.
 - 위 그림은 객체 수준 모델에서 모델을 애그리거트로 묶어서 다시 표현한 것이다.
 - 동일한 모델이지만 애그리거트를 사용함으로써 모델 간의 관계를 개별 모델 수준뿐만 아니라 상위 수준에서도 이해할 수 있게 된다. 
 - 애그리거트는 모델을 이해하는데 도움을 줄 뿐만 아니라 일관성을 관리하는 기준이 된다.
 - 모델을 잘 이해할 수 있고 애그리거트 단위로 일관성을 관리하기 때문에 애그리거트는 복잡한 도메인을 단순한 구조로 만들어준다.
   - 복잡도가 낮아지는 만큼 도메인 기능을 확장하고 변경하는데 필요한 노력(개발시간)도 줄어든다.
 - 애그리거트는 관련된 모델을 하나로 모은 것이기 떄문에 한 애그리거트에 속한 객체는 유사하거나 동일한 라이프사이클을 갖는다. 
   - 주문 애그리거트를 만들렴녀 Order, OrderLine, Orderer와 같은 관련 객체를 함께 생성해야 한다.
   - Order는 생성했는데 ShippingInfo는 만들지 않았거나 ShippingInfo를 생성하면서 Orderer를 생성하지 않는 경우는 없다.
   - 도메인 규칙에 따라 최초 주문 시점에 일부 객체를 만들 필요가 없는 경우도 있지만 애그리거트에 속한 구성요소는 대부분 함께 생성하고 함께 제거한다.
 - 애그리거트는 경계를 갖는다.
   - 한 애그리거트에 속한 객체는 다른 애그리거트에 속하지 않는다.
   - 애그리거트는 독립된 객체 군이며, 각 애그리거트는 자기 자신을 관리할 뿐 다른 애그리거트를 관리하지 않는다.
   - 예) 주문 애그리거트는 배송지를 변경하거나 주문 상품 개수를 변경하는 등 자기자신을 관리하지만, 주문 애그리거트에서 회원읜 비밀번호를 변경하거나 상품의 가격을 변경하지 않는다.
 - 경계를 설정할 때 기본이 되는 것은 도메인 규칙과 요구사항이다.
   - 도메인 규칙에 따라 함께 생성되는 구성요소는 한 애그리거트에 속할 가능성이 높다.
   - 예) 주문할 상품 개수, 배송지 정보, 주문자 정보는 주문 시점에 함께 생성되므로 이들은 한 애그리거트에 속한다. 또한, OrderLine의 주문 상품 개수를 변경하면 도메인 규칙에 따라 Order의 총 주문 금액을 새로 계산해야 한다. 
   - 사용자 요구사항에 따라 주문 상품 개수와 배송지를 함께 변경하기도 한다.
   - 이렇게 함께 변경되는 빈도가 높은 객체는 한 애그리거트에 속할 가능성이 높다. 
 - 흔히 'A가 B를 갖는다' 로 설계할 수 있는 요구사항이 있다면 A와 B를 한 애그리거트로 묶어서 생각하기 쉽다.
   - 주문의 경우 Order가 ShippingInfo와 Orderer를 가지므로 이는 어느 정도 타당해 보인다.
   - 하지만, 'A가 B를 갖는다'로 해석할 수 있는 요구사항이 있다고 하더라도 이것이 반드시 A와 B가 한 애그리거트에 속한다는 것을 의미하는 것은 아니다.
   - 예) 상품과 리뷰
     - 상품 상세 페이지에 들어가면 상품 상세 정보와 함께 리뷰 내용을 보여줘야 한다는 요구사항이 있다면 Product 엔티티와 Review 엔티티가 한 애그리거트에 속한다고 생각할 수 있다.
     - 하지만, Product와 Review는 함께 생성 되지 않고 함께 변경되지도 않는다.
     - 게다가, Product를 변경하는 주체가 상품 담당자라면 Review를 생성하고 변경하는 주체는 고객이다.


**Product가 Review를 갖는 것으로 생각할 수 있지만, 상품과 리뷰는 함께 생성되거나 변경되지 않고 변경 주체도 다르기 떄문에 서로 다른 애그리거트에 속한다.**

![image](https://user-images.githubusercontent.com/28394879/134835112-e53027c7-8f99-4858-bc51-c665b2ca6cdb.png) 
- Review의 변경이 Product에 영향을 주지 않고 반대로 Product의 변경이 Review에 영향을 주지 않기 때문에 이 둘은 한 애그리거트에 속한다기 보다는 서로 다른 애그리거트에 속한다.


<br>

- 처음 도메인 모델을 만들기 시작하면 큰 애그리거트로 보이는 것들이 많지만 도메인에 대한 경험이 생기고 도메인 규격을 제대로 이해할수록 실제 애그리거트의 크기는 줄어들게 된다.
- 애그리거트가 한 개의 엔티티 객체만 갖는 경우가 많으며 두 개 이상의 엔티티로 구성되는 애그리거트는 드물게 존재한다. 


</details>

<details> <summary> 2. 애그리거트 루트 </summary>

## 2. 애그리거트 루트 

- 주문 애그리거트는 다음을 포함한다.
  - 총 금액인 totalAmounts를 갖고 있는 Order 엔티티
  - 개별 구매 상품의 개수인 quantity와 금액인 price를 갖고 있는 OrderLine 밸류
- 구매할 상품의 개수를 변경하면 한 OrderLine의 quantity를 변경하고 더불어 Order의 totalAmounts도 변경해야 한다. 
- 그렇지 않으면 '주문 총 금액은 개별 상품의 주문 개수 X 가격의 합이다.' 라는 도메인 규칙을 어기고 데이터 일관성이 깨진다. 
- 애그리거트는 여러 객체로 구성되기 떄문에 한 객체만 상태가 정상이어서는 안 된다. 
- 도메인 규칙을 지키려면 애그리거트에 속한 모든 객체가 정상 상태를 가져야 한다. 
- 주문 애그리거트의 경우 OrderLine을 변경하면 Order의 totalAmounts도 다시 계산해서 총 금액이 맞아야 한다. 


**주문 애그리거트의 루트는 Order이다** 

![image](https://user-images.githubusercontent.com/28394879/134840374-d2694c1a-a776-4625-91cd-c709fa107a0f.png)

- 애그리거트에 속한 모든 객체가 일관된 상태를 유지하려면 애그리거트 전체를 관리할 주체가 필요한데 이 책임을 지는 것이 바로 애그리거트의 루트 엔티티이다. 
- 애그리거트 루트 엔티티는 애그리거트의 대표 엔티티로 애그리거트에 속한 객체는 애그리거트 루트 엔티티에 직접 또는 간접적으로 속한다.
- 주문 애그리거트에서 루트 역할을 하는 엔티티는 Order이다.
  - OrderLine, ShippingInfo, Orderer 등 주문 애그리거트에 속한 모델은 Order에 직접 또는 간접적으로 속한다.


### 도메인 규칙과 일관성 
- 애그리거트 루트가 단순히 애그리거트에 속한 객체를 포함하는 것으로 끝나는 것은 아니다.
- 애그리거트 루트의 핵심 역할은 애그리거트의 일관성이 깨지지 않도록 하는 것이다.
  - 예) 주문 애그리거트는 배송지 변경, 상품 변경과 같은 기능을 제공하는데 애그리거트 루트인 Order가 이 기능을 구현한 메서드를 제공한다.
- 애그리거트 루트가 제공하는 메서드는 도메인 규칙에 따라 애그리거트에 속한 객체의 일관성이 꺠지지 않도록 구현해야 한다.
  - 예) 배송이 시작되기 전까지만 배송지 정보를 변경할 수 있다는 규칙이 있다면, 애그리거트 루트인 Order의 changeShippingInfo() 메서드는 이 규칙에 따라 배송 시작 여부를 확인하고 변경이 가능한 경우에만 배송지 정보를 변경해야 한다.
  ```java
  public class Order{
      
      // 애그리거트 루트는 도메인 규칙을 구현한 기능을 제공한다.
      public void changeShippingInfo(ShippingInfo newShippingInfo) {
          verifyNotYetShipped();
          setShippingInfo(newShippingInfo);
      }

      private void verifyNotYetShipped() {
          if (state != OrderState.PAYMENT_WAITING && state != OrderState.WAITING) throw new IllegalStateException("already shipped");
      }
  }
  ``` 
- 애그리거트 루트가 아닌 다른 객체가 애그리거트에 속한 객체를 직접 변경하면 안된다.
- 이는 애그리거트 루트가 강제하는 규칙을 적용할 수 없어 모델의 일관성을 꺠지는 원인이 된다. 
  ```java
  ShippingInfo si = order.getShippingInfo();
  si.setAddress(newAddress);
  ``` 
  - 이 코드는 애그리거트 루트인 Order에서 ShippingInfo를 가져와 직접 정보를 변경하고 있다. 
  - 주문 상태에 상관없이 배송지 주소를 변경할 수 있는데, 이는 업무 규칙을 무시하고 DB 테이블에서 직접 데이터를 수정하는 것과 같은 결과를 만든다.
  - 즉, 논리적인 데이터 일관성이 깨지게 되는 것이다.
  - 일관성을 지키기 위해 다음과 같이 상태 확인 로직을 응용 서비스에 구현할 수도 있지만, 이렇게 되면 동일한 검사 로직을 여러 응용 서비스에서 중복해서 구현할 가능성이 높아져 상황을 더 악화시킬 수 있다.
  ```java
  ShippinrgInfo si = order.getShippingInfo();
  
  // 주요 도메인 로직이 중복되는 문제 
  if (state != OrderState.PAYMENT_WAITING && state != OrderState.WAITING) throw new IllegalStateException("already shipped");

  si.setAddress(newAddress);
  ``` 
- 불필요한 중복을 피하고 애그리거트 루트를 통해서만 도멩니 로직을 구현하게 만들려면 도메인 모델에 대해 다음의 두가지를 습관적으로 적용해야 한다.
  - 단순히 필드를 변경하는 set 메서드를 공개(public)범위로 만들지 않는다.
  - 밸류 타입은 불변으로 구현한다.

**set 메서드를 공개(public)범위로 만들지 않는다**

```java
// 도메인 모델에서 공개 set 메서드는 가급적 피해야 한다.
public void setName(String name) {
    this.name = name;
}
```
- 보통 공개 set 메서드는 위와 같이 필드에 값을 할당하는 것으로 끝내는 경우가 많다. 잘해야 null을 검사하는 정도이다.
- 공개 set 메서드는 중요 도메인의 의미나 의도를 표현하지 못하고 도메인 로직이 도메인 객체가 아닌 응용 영역이나 표현 영역으로 분산되게 만드는 원인이 된다. 
- 도메인 로직이 한곳에 응집되어 있지 않게 되므로 코드를 유지보수할 대에도 분석하고 수정하는 데 더 많은 시간을 들이게 된다. 
- 도메인 모델의 엔티티나 밸류에 공개 set 메서드만 넣지 않아도 일관성이 꺠질 가능성이 줄어든다.
- 공개 set 메서드를 사용하지 않게 되면 의미가 드러나는 메서드를 사용해서 구현할 가능성이 높아진다.
  - 예) set형식의 이름을 갖는 공개 메섣르르 사용하지 않으면 자연스럽게 cancel이나 changePassword처럼 의미가 더 잘드러나는 이름을 사용하는 빈도가 높아진다.

**밸류 타입은 불변으로 구현한다**

```java
ShippingInfo si = order.getShippingInfo();
si.setAddress(newAddress); // ShippingInfo 밸류 객체가 불변이면, 이 코든느 컴파일 에러!
```
- 공개 set 메서드를 만들지 않는 것의 연장으로 밸류는 불변 타입으로 구현한다.
- 밸류 객체의 값을 변경할 수 없으면 애그리거트 루트에서 밸류 객체를 구해도 값을 변경할 수 없기 떄문에 애그리거트 외부에서 밸류 객체의 상태를 변경할 수 없게 된다.


**애그리거트 루트가 제공하는 메서드로 새로운 밸류 객체로 변경**

```java
public class Order {
    private ShippingInfo shippingInfo;
    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        verifyNotYetShipped();
        setShippingInfo(newShippingInfo);
    }
    // set 메서드의 접근 허용 범위는 private이다.
    private void setShippingInfo(ShippingInfo newShippingInfo) {
        // 밸류가 불변이면, 새로운 객체를 할당해서 값을 변경해야 한다. 
        // 불변이므로 this.shippingInfo.setAddress(newShippingInfo.getAddress())와 같은 
        // 코드를 사용할 수 없다.
        this.shippingInfo = newShippingInfo;
    }
}
```
- 애그리거트 외부에서 내부 상태를 함부로 바꾸지 못하므로 애그리거트의 일관성이 꺠질 가능성이 줄어든다.
- 밸류 객체가 불변이면 밸류 객체의 값을 변경하는 방법은 새로운 밸류 객체를 할당하는 것 뿐이다.
- 즉, 위의 코드와 같이 애그리거트 루트가 제공하는 메서드에 새로운 밸류 객체를 전달해서 값을 변경하는 방법밖에 없다.
- 밸류 타입의 내부 상태를 변경하려면 애그리거트 루트를 통해서만 가능하다.
- 그러므로, 애그리거트 루트가 도메인 규칙을 올바르게만 구현하면 애그리거트 전체의 일관성을 올바르게 유지할 수 있다. 

### 애그리거트 루트의 기능 구현 
- 애그리거트 루트는 애그리거트 내부의 다른 객체를 조합해서 기능을 완성한다.
  - 예) Order는 총 주문 금액을 구하기 위해 OrderLine 목록을 사용한다.
  ```java
  public class Order {
      private Money totalAmounts;
      private List<OrderLine> orderLines;

      private void calculateTotalAmounts() {
          int sum = orderLines.stream()
                .mapToInt(ol -> ol.getPrice() * ol.quantity())
                .sum();
        this.totalAmounts = new Money(sum);
      }
  }
  ```
  - 예) 회원을 표현하는 Member 애그리거트 루트는 암호를 변경하기 위해 Password 객체에 암호가 일치하는지 여부를 확인할 수 있다.
  ```java
  public class Member {
      private Password password;

      public void changePassword(String currentPassword, String newPassword) {
          if (!password.match(currentPassword)) {
              throw new PasswordNotMatchException();
          }
          this.password = new Password(newPassword);
      }
  }
  ``` 
- 애그리거트 루트가 구성요소의 상태만 참조하는 것은 아니다. 기능 실행을 위임 하기도 한다.
  - 예) 구현 기술의 제약이나 내부 모델링 규칙 때문에 OrderLine 목록을 별도 클래스로 분리했다고 해보자.
  ```java
  public class OrderLines {
      private List<OrderLine> lines;

      public Money getTotalAmounts() {...구현;}
      public void changeOrderLines(List<OrderLine> newLines) {
          this.lines = newLines;
      }
  }
  ```
  - 이 경우 Order의 changeOrderLines() 메서드는 다음과 같이 내부의 orderLines 필드에 상태 변경을 위임하는 방식으로 기능을 구현한다.
  ```java
  public class Order {
      private OrderLines orderLines;
      
      public void changeOrderLines(List<OrderLine> newLines) {
          orderLines.changeOrderLines(newLines);
          this.totalAmounts = orderLines.getToitalAmounts();
      }
  }
  ```   
  - OrderLines는 changeOrderLines()와 getTotalAmounts() 같은 기능을 제공하고 있다.
  - 만약 Order가 getOrderLines()와 같이 OrderLines를 구할 수 있는 메서드를 제공하면 애그리거트 외부에서 OrderLines의 기능을 실행할 수 있게 된다.  
  ```java
  OrderLines lines = order.getOrderLines();
  // 외부에서 애그리거트 내부 상태 변경!
  // order의 totalAmounts가 값이 OrderLines가 일치하지 않게 됨
  lines.changeOrderLines(newOrderLines);
  ```
  - 이 코드는 주문의 OrderLine 목록이 바뀌는데 총합은 계산하지 않는 버그를 만든다. 
  - 이런 버그가 생기지 않도록 하려면 애초에 애그리거트 외부에서 OrderLine 목록을 변경할 수 없도록 OrderLines를 불변으로 구현하면 된다. 
  - 팀 표준이나 구현 기술의 제약으로 OrderLines를 불변으로 구현할 수 없다면 OrderLines의 변경 기능을 패키지나 protected 범위로 한정해서 외부에서 실행할 수 없도록 제한하는 방법이 있다.
  - 보통 한 애그리거트에 속하는 모델은 한 패키지에 속하기 때문에 패키지나 protected 범위를 사용하면 애그리거트 외부에서 상태 변경 기능을 실행하는 것을 방지할 수 있다. 

### 트랜잭션 범위
- 트랜잭션 범위는 작을수록 좋다.
- DB 테이블을 기준으로 한 트랜잭션이 한 개 테이블을 수정하는 것과 세개의 테이블을 수정하는 것은 성능에서 차이가 발생한다.
  - 한 개 테이블을 수정할 떄에는 트랜잭션 충돌을 막기 위해 잠그는 대상이 한 개 테이블의 한 행으로 한정되지만, 세 개의 테이블을 수정하면 잠금 대상이 더 많아진다. 
  - 잠금 대상이 많아진다는 것은 그만큼 동시에 처리할 수 있는 트랜잭션 개수가 줄어든다는 것을 뜻하고 이는 전체적인 성능(처리량)을 떨어뜨린다. 
- 동일하게 한 트랜잭션에서는 한 개의 애그리거트만 수정해야 한다.
  - 한 트랜잭션에서 두 개 이상의 애그리거트를 수정하면 트랜잭션 충돌이 발생할 가능성이 더 높아지기 떄문에 한번에 수정하는 애그리거트 개수가 많아질수록 전체 처리량이 떨어지게 된다.
- 한 트랜잭션에서 한 애그리거트만 수정한다는 것은 애그리거트에서 다른 애그리거트를 변경하지 않는다는 것을 뜻한다.
  - 한 애그리거트에서 다른 애그리거트를 수정하면 결과적으로 두 개의 애그리거트를 한 트랜잭션에서 수정하게 되므로 한 애그리거트 내부에서 다른 애그리거트의 상태를 변경하는 기능을 실행하면 안 된다.
  - 예) 배송지 정보를 변경하면서 동시에 배송지 정보를 회원의 주소로 설정하는 기능이 있다고 해보자. 
  ```java
  public class Order {
      private Orderer orderer;

      public void shipTo(ShippingInfo newShippingInfo, boolean useNewShippingAddrAsMemberAddr) {
          verifyNotYetShipped();
          setShippingInfo(newShippingInfo);
          if(useNewShippingAddrAsMemberAddr) {
              // 다른 애그리거트의 상태를 변경하면 안 됨!
              orderer.getCustomer().changeAddress(newShippingInfo.getAddress());
          }
      }
  }
  ``` 
  - 이 경우 주문 애그리거트는 회원 애그리거트의 정보를 변경하면 안된다.
  - 이는 애그리거트가 자신의 책임 범위를 넘어 다른 애그리거트의 상태까지 관리하는 꼴이 된다.
  - 애그리거트는 서로 최대한 독립적이어야 하는데 한 애그리거트가 다른 애그리거트의 기능에 의존하기 시작하면 애그리거트 간 결합도가 높아지게 된다.
  - 결합도가 높아지면 높아질수록 향후 수정 비용이 증가하므로 애그리거트에서 다른 애그리거트의 상태를 변경하지 말아야 한다.
  - 만약 부득이하게 한 트랜잭션으로 두 개 이상의 애그리거트를 수정해야 한다면 애그리거트에서 다른 애그리거트를 직접 수정하지 말고 응용 서비스에서 두 애그리거트를 수정하도록 구현해야 한다.
  ```java
  public class ChangeOrderService {
      // 두 개 이상의 애그리거트를 변경해야 하면,
      // 응용 서비스에서 각 애그리거트의 상태를 변경한다.
      @Transactional
      public void changeShippingInfo(OrderId id, ShippingInfo newShippingInfo, boolean useNewShippingAddrAsMemberAddr) {
          Order order = orderRepository.findById(id);
          if (order == null) throw new OrderNotFoundException();
          order.shipTo(newShippingInfo);
          if(useNewShippingAddrAsMemberAddr) {
              order.getOrderer()
                    .getCustomer().changeAddress(newShippingInfo.getADdress());
          }
      }
  }
  ``` 

  
- 도메인 이벤트를 사용하면 한 트랜잭션에서 한 개의 애그리거트를 수정하면서도 동기나 비동기로 다른 애그리거트의 상태를 변경하는 코드를 작성할 수 있는데, 이에 대한 내용은 10장에서 살펴보자. 
- 한 트랜잭션에서 한 개의 애그리거트를 변경하는 것을 권장하지만 다음의 경우에는 한 트랜잭션에서 두 개 이상의 애그리거트를 변경하는 것을 고려할 수 있다. 
  - 팀 표준: 팀이나 조직의 표준에 따라 사용자 유스케이스와 관련된 응용 서비스의 기능을 한 트랜잭션으로 실행해야 하는 경우가 있다. DB가 다른 경우 글로벌 트랜잭션을 반드시 사용하도록 규칙을 정하는 곳도 있다.
  - 기술 제약: 한 트랜잭션에서 두 개 이상의 애그리거트를 수정하는 대신 도메인 이벤트와 비동기를 사용하는 방식을 사용하는데, 기술적으로 이벤트 방식을 도입할 수 없는 경우 한 트랜잭션에서 다수의 애그리거트를 수정해서 일관성을 처리해야 한다. 
  - UI 구현의 편리: 운영자의 편리함을 위해 주문 목록 화면에서 여러 주문의 상태를 한 번에 변경하고 싶을 것이다. 이 경우 한 트랜잭션에서 여러 주문 애그리거트의 상태를 변경할 수 있을 것이다.


</details>

<details> <summary> 3. 리포지터리와 애그리거트 </summary>

</details>

<details> <summary> 4. ID를 이용한 애그리거트 참조 </summary>

</details>


<details> <summary> 5. 애그리거트 간 집합 연관 </summary>

</details>

<details> <summary> 6. 애그리거트를 팩토리로 사용하기 </summary>

</details>