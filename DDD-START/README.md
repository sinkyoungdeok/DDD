
# [1.도메인 모델 시작](./1.도메인-모델-시작)

<details> <summary> 1. 도메인 </summary>

## 도메인

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

## 도메인 모델

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

## 도메인 모델 패턴

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

## 도메인 모델 도출

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

## 엔티티와 벨류
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
    ```
        //엔티티를 생성하기 전에 식별자 생성
        String orderNumber = orderRepository.generate();

        Order order = new Order(orderNumber, ...);
        orderRepository.save(order);
    ``` 
- 

</details>

<details> <summary> 6. 도메인 용어  </summary>

</details>
