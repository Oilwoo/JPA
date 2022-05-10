# JPA
### JPA란
JPA(Java Persistent API)는 자바 진영의 ORM 기술 표준입니다. ORM(Object Relational Mapping)이란 객체는 객체대로, 관계형 DB는 관계형 DB대로 설계하고 중간에서 ORM 프레임워크가 매핑 역할을 수행하는 것을 가르킵니다. 
![image](https://user-images.githubusercontent.com/53050413/167528462-979a217e-396c-4eaa-82f9-bd047ab201d4.png)
### JPA특장점
- SQL 중심적인 개발 → 객체 중심적인 개발
- 생산성
- 유지보수 용이
- 패러다임 불일치 해결

### JPA사용법
#### Entity
보통사용하는 MYBATIS, VO(DTO)를 JPA에서는 테이블을 그냥 객체화 시켰다고 생각하면 편하다.
@Entity 어노테이션을 자바클래스에 적용 lombok과 함께 사용하면 더욱 코드가 간결해진다.

```java
@Entity
@Data //lombok
@Table(name = "basic_maker")
public class Member {
    @Id //pk
    @GeneratedValue(strategy= GenerationType.AUTO)
    private long id;

    @Column(name = "mName")
    private String name;

    @Column
    private int age;

}
```
##### @Id
primary key를 가지는 변수를 선언하는 것을 뜻한다. @GeneratedValue 어노테이션은 해당 Id 값을
어떻게 자동으로 생성할지 전략을 선택할 수 있다. 여기서 선택한 전략은 "AUTO"이다.

##### @Table
별도의 이름을 가진 데이터베이스 테이블과 매핑한다. 기본적으로 @Entity로 선언된 클래스의 이름은 실제
데이터베이스의 테이블 명과 일치하는 것을 매핑한다. 따라서 @Entity의 클래스명과 데이터베이스의 테이블명이
다를 경우에 @Table(name=" ")과 같은 형식을 사용해서 매핑이 가능하다.

##### @Column
@Column 선언이 꼭 필요한 것은 아니다. 하지만 @Column에서 지정한 변수명과 데이터베이스의 컬럼명을
서로 다르게 주고 싶다면 @Column(name=" ") 같은 형식으로 작성하면 된다.
그렇지 않은 경우에는 기본적으로 멤버 변수명과 일치하는 데이터베이스 컬럼을 매핑한다.

#### Repository
Entity클래스를 작성했다면 이번엔 Repository 인터페이스를 만들어야 한다.
스프링부트에서는 Entity의 기본적인 CRUD가 가능하도록 JpaRepository 인터페이스를 제공한다.

#### 사용메소드


|method|기능|
|---||---|
|save()|레코드 저장(insert, update)|
|findOne()|primary key로 레코드 한건 찾기|
|findAll()|전체 레코드 불러오기. 정렬(sort), 페이징(pageable) 가능|
|count()|레코드 갯수|
|delete()|레코드 삭제|

### 참고출처링크
https://velog.io/@tmdgh0221/JPA-%EA%B8%B0%EB%B3%B8%ED%8E%B8-%EC%A0%95%EB%A6%AC -> 이론적인내용
https://jobc.tistory.com/120 -> JPA 구체적인 사용법
