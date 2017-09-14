---
title: "Conterller Interface 그리고 Generic"
date: 2017-09-09
draft: false
tags: [Java, Generic]
---

"모든 메뉴는 목록조회, 상세, 추가, 수정, 삭제 기능을 가진다. 관리자 기능 접근을 제어 할 수 있다." 라는 요구사항이 있었다.

요구사항을 보는순간 Interface 가 떠올랐다.
그리고 바로 샘플을 구현하였다.
설계 점검이라 코드는 간략히 작성 하기로 하였다.

최초 코드는 다음과 같은 모습였다.

TestController.java
``` 
public interface TestController {

    Object search(Object schDto);

    Object find(Object findDto);

    void add(Object addDto);
}
```

TestControllerImpl.java
```
@RestController
public class TestControllerImpl implements TestController{

    @Autowired
    private TestService service;

    @Override
    public Object search(Object reqDto) {
        return null;
    }

    @Override
    public Object find(Object findDto) {
        return null;
    }

    @Override
    public void add(Object addDto) {

    }


}
```

위 코드는 문제가 있다. Object 를 DTO 로 형변환 할수가 없다.
해결책을 고민하다 제너릭이 생각이 났다. 제네릭을 이용해 Interface 매개변수를 T 로 만들면 될것 같았다.
Interface 제네릭 사용법을 몰라 구글링후 아래 코드를 다시 작성하였다.

TestController.java
```
public interface TestController<T1, T2, T3> {

    Object search(T1 schDto);

    Object find(T2 findDto);

    void add(T3 addDto);
}
```

TestControllerImpl.java
```
@RestController
public class TestControllerImpl implements TestController<SearchDto, FindDto, AddDto> {

    @Override
    public Object search(SearchDto reqDto) {
        return null;
    }

    @Override
    public Object find(FindDto findDto) {
        return null;
    }

    @Override
    public void add(AddDto addDto) {

    }
}
```

나와 동료는 나름 만족하였고 샘플 코드를 참조하여 개발 진행 하기로 했다.

### 에필로그

코딩 시작 얼마후 Controller Interface(위 코드 TestController)를 삭제했다. 
필요하지도 않은 DTO 를 작성해야 되는 상황이 발생 하였고, 이것은 유지보수때 의문점만 생길 것이다.

제너릭을 제거하고 Interface 에서 모든 매개변수를 Map 으로 변경하자는 의견도 나왔다.
하지만 유지보수를 위해서 DTO 를 사용하기로 결정하였기 때문에 의견을 받아드릴수 없었다. 

결국 메뉴 URL 을 DB에 저장하고 Interceptor 나 Filtter 제어 하기로 하고 제너릭을 제거 하였다.
