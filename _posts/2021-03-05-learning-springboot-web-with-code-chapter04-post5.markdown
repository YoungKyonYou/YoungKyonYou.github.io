---
layout: post
title: 코드로 배우는 스프링 부트 웹 프로젝트-Part2-05
date: 2021-03-05 14:00:00 0000
tags: [Intellij, SpringBoot, Guesbook]
categories: [SpringBoot]
description: 방명록 만들기
---

<br><br>

# <center>방명록의 조회, 수정 그리고 삭제 처리</center>

<br>

방명록의 조회는 아직 GuestbookService 쪽에 기능이 구현이 되지 않은 상태이므로 서비스 계층부터 구현을 시작한다.

**GuestbookService 인터페이스**

```java
(...)
public interface GuestbookService {
    Long register(GuestbookDTO dto);
    @Builder.Default
    ModelMapper modelMapper= ModelMapperUtil.getModelMapper();
    PageResultDTO<GuestbookDTO, Guestbook> getList(PageRequestDTO requestDTO);
    GuestbookDTO read(Long gno);
    default Guestbook dtoToEntity(GuestbookDTO dto){
        Guestbook entity=modelMapper.map(dto,Guestbook.class);

        return entity;
    }
    (...)
```

<br>

GuestbookService에는 read()라는 메서드를 추가하고 파라미터는 Long 타입의 gno 값을, 리턴 타입은 GuestbookDTO로 지정한다.

**GuestbookServiceImpl.java**

```java
(...)
  @Override
    public GuestbookDTO read(Long gno) {

        Optional<Guestbook> result = repository.findById(gno);

        return result.isPresent()? entityToDto(result.get()): null;
    }
(...)
```

<br>

> #### **line 7:** result.get()를 통해서 해당 엔티티 객체를 DTO 객체로 변환시켜주기 위해서 entityToDto 메서드로 파라미터로 넘겨서 DTO를 반환받는다.<br>

<br>

GuestbookServiceImple 클래스의 내부에는 인터페이스에 정의된 read() 기능을 구현한다. GuestbookRepository에서 findById()를 통해서 만일 엔티티 객체를 가져왔다면, entityToDto()를 이용해서 엔티티 객체를 DTO를 변환해서 반환한다.

GuestbookController에서는 GET 방식으로 gno 값을 받아서 Model에 GuestbookDTO 객체를 담아서 전달하도록 코드를 작성한다. 추가로 나중에 다시 목록 페이지로 돌아가는 데이터를 같이 저장하기 위해서 PageRequestDTO를 파라미터로 같이 사용한다. @ModelAttribute는 없어도 처리가 가능하지만 명시적으로 requestDTO라는 이름으로 처리해 둔다.

**GuestbookController.java 일부**

```java
(...)
    @GetMapping({"/read", "/modify"})
    public void read(long gno, @ModelAttribute("requestDTO") PageRequestDTO requestDTO, Model model) {

        log.info("gno: " + gno);

        GuestbookDTO dto = service.read(gno);

        model.addAttribute("dto", dto);

    }
    (...)
```

<br>

> #### **line 3:** 여기서 @ModelAttribute는 PageRequestDTO 클래스의 객체 requestDTO를 자동으로 생성한다. 이때 @ModelAttribute가 지정되는 클래스는 빈 클래스여야 하고 getter setter가 만들어져 있어야 한다.<br>

<br>

방명록의 조회는 등록 화면과 유사하지만 readonly 속성이 적용되고, 다시 목록 페이지로 이동하는 링크와 수정과 삭제가 가능한 링크를 제공한다.

![](/images/Learning_SpringBoot_with_Web_Project/Part2/Chapter4/2021-03-05-15-14-06.png)

<br>

**read.html**

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">

<th:block th:replace="~{/layout/basic :: setContent(~{this::content} )}">

    <th:block th:fragment="content">

        <h1 class="mt-4">GuestBook Read Page</h1>

        <div class="form-group">
            <label >Gno</label>
            <input type="text" class="form-control" name="gno" th:value="${dto.gno}" readonly >
        </div>

        <div class="form-group">
            <label >Title</label>>
            <input type="text" class="form-control" name="title" th:value="${dto.title}" readonly >
        </div>
        <div class="form-group">
            <label >Content</label>
            <textarea class="form-control" rows="5" name="content" readonly>[[${dto.content}]]</textarea>
        </div>
        <div class="form-group">
            <label >Writer</label>
            <input type="text" class="form-control" name="writer"
             th:value="${dto.writer}" readonly>
        </div>
        <div class="form-group">
            <label >RegDate</label>
            <input type="text" class="form-control" name="regDate"
             th:value="${#temporals.format(dto.regDate, 'yyyy/MM/dd HH:mm:ss')}" readonly>
        </div>
        <div class="form-group">
            <label >ModDate</label>
            <input type="text" class="form-control" name="modDate"
             th:value="${#temporals.format(dto.modDate, 'yyyy/MM/dd HH:mm:ss')}" readonly>
        </div>

               <a th:href="@{/guestbook/modify(gno = ${dto.gno}, page=${requestDTO.page})}">
               <button type="button" class="btn btn-primary">Modify</button></a>

               <a th:href="@{/guestbook/list(page=${requestDTO.page})}">
               <button type="button" class="btn btn-info">List</button></a>



    </th:block>

</th:block>

```

<br>

수정과 삭제의 모든 시작은 GET 방식으로 진입하는 '수정' 화면에서 작업을 선택해서 처리하게 된다.

![](../images/Learning_SpringBoot_with_Web_Project/Part2/Chapter4/2021-03-05-15-15-57.png)

<br>

- Guestbook의 수정(1)은 POST 방식으로 처리하고 다시 수정된 결과를 확인할 수 있는 조회 화면으로 이동한다.
- 삭제(2)는 POST 방식으로 처리하고 목록 화면으로 이동한다.
- 목록을 이동하는 작업은 GET 방식으로 처리한다. 이때 기존에 사용하던 페이지 번호 등을 유지해서 이동해야 한다.

<br>

방명록의 수정과 삭제를 구현할 때는 삭제 작업이 상대적으로 단순하므로 삭제를 먼저 처리하고 수정은 마지막에 처리한다. 게시물의 수정과 삭제는 동일하게 '수정/삭제가 가능한 페이지'로 이동한 상태에서 선택을 통해서 이루어진다. 이를 위해 GuestbookController에서는 조회와 비슷하게 GET 방식으로 진입하는 '/guestbook/modify'를 기존의 read()에 어노테이션의 값을 변경해서 처리한다.

**GuestbookController.java**

```java
(...)
    @GetMapping({"/read", "/modify"})
    public void read(long gno, @ModelAttribute("requestDTO") PageRequestDTO requestDTO, Model model) {

        log.info("gno: " + gno);

        GuestbookDTO dto = service.read(gno);

        model.addAttribute("dto", dto);

    }
    (...)
```

<br>

화면으로 사용하는 modify.html을 생성하고 read.html을 복사해서 그대로 추가한다. modify.html는 가장 먼저 화면의 `<h1>` 태그의 내용을 수정한다.

![](../images/Learning_SpringBoot_with_Web_Project/Part2/Chapter4/2021-03-05-15-21-04.png)

<br>

**modify.html 일부**

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">

<th:block th:replace="~{/layout/basic :: setContent(~{this::content} )}">

    <th:block th:fragment="content">

        <h1 class="mt-4">GuestBook Modify Page</h1>

        <form action="/guestbook/modify" method="post">

            <input type="hidden" name="type" th:value="${requestDTO.type}" >
            <input type="hidden" name="keyword" th:value="${requestDTO.keyword}" >


            <div class="form-group">
                <label >Gno</label>
                <input type="text" class="form-control"
                name="gno" th:value="${dto.gno}" readonly >
            </div>

            <div class="form-group">
                <label >Title</label>
                <input type="text" class="form-control"
                 name="title" th:value="${dto.title}" >
            </div>
            <div class="form-group">
                <label >Content</label>
                <textarea class="form-control" rows="5"
                 name="content">[[${dto.content}]]</textarea>
            </div>
            <div class="form-group">
                <label >Writer</label>
                <input type="text" class="form-control"
                name="writer" th:value="${dto.writer}" readonly>
            </div>
            <div class="form-group">
                <label >RegDate</label>
                <input type="text" class="form-control"
                th:value="${#temporals.format(dto.regDate, 'yyyy/MM/dd HH:mm:ss')}" readonly>
            </div>
            <div class="form-group">
                <label >ModDate</label>
                <input type="text" class="form-control"
                th:value="${#temporals.format(dto.modDate, 'yyyy/MM/dd HH:mm:ss')}" readonly>
            </div>

        </form>

        <button type="button" class="btn btn-primary">Modify</button>

        <button type="button" class="btn btn-info">List</button>

        <button type="button" class="btn btn-danger">Remove</button>




    </th:block>

</th:block>

```

<br>

modify.html은 수정/삭제 작업을 POST 방식으로 처리하므로 `<form>` 태그로 수정하는 내용을 감싸도록 처리한다.

위의 코드에서 날짜 부분은 화면에서 수정 자체도 불가능하고 JPA에서 자동으로 처리될 것이므로, nmae 속성 없이 작성되었다. 마지막으로 화면에 기능을 처리할 때 사용하는 버튼들을 추가했다.

브라우저로 확인하면 '제목(title)'과 '내용(content)'은 수정이 가능하고 나머지 부분들은 readonly로 처리되게끔 이벤트를 처리해보자.

modify.html에 있는 버튼은 'Modify(수정), Remove(삭제), List(목록)' 세 가지이다. 각 버튼을 클릭할 때 마다 다르게 이벤트를 처리해야 한다. '수정'과 '삭제' 작업은 `<form>` 태그의 action 속성을 조정해서 처리할 수 있다. 이에 대한 이벤트 처리는 조금 뒤쪽에서 처리한다.

<br>

현재까지 서비스 계층에 구현된 기능은 수정과 삭제 기능 자체가 없었기 때문에 관련된 기능들은 메서드를 추가한다.

**GuestbookService 인터페이스 일부**

```java
(...)
public interface GuestbookService {
    Long register(GuestbookDTO dto);
    @Builder.Default
    ModelMapper modelMapper= ModelMapperUtil.getModelMapper();
    PageResultDTO<GuestbookDTO, Guestbook> getList(PageRequestDTO requestDTO);
    GuestbookDTO read(Long gno);
    void remove(Long gno);
    void modify(GuestbookDTO dto);
    default Guestbook dtoToEntity(GuestbookDTO dto){
        Guestbook entity=modelMapper.map(dto,Guestbook.class);

        return entity;
    }
    (...)
```

<br>

GuestbookServiceImpl 클래스에서는 위의 remove()와 modify() 메서드를 아래와 같이 구현해 준다.

**GuestbookServiceImpl.java**

```java
(...)
@Override
    public void remove(Long gno) {

        repository.deleteById(gno);

    }

    @Override
    public void modify(GuestbookDTO dto) {

        //업데이트 하는 항목은 '제목', '내용'

        Optional<Guestbook> result = repository.findById(dto.getGno());

        if(result.isPresent()){

            Guestbook entity = result.get();

            entity.changeTitle(dto.getTitle());
            entity.changeContent(dto.getContent());

            repository.save(entity);

        }
    }
(...)
```

<br>

방명록의 수정은 기존의 엔티티에서 '제목'과 '내용'만을 수정하고 다시 저장하는 방식으로 구현한다.

방명록의 삭제는 POST 방식으로 gno 값을 전달하고 삭제 후에는 다시 목록의 첫 페이지로 이동하는 방식이 가장 보편적이다. GuestbookController에는 다음과 같은 형태의 메서드를 추가한다.

**GuestbookController.java**

```java
    @PostMapping("/remove")
    public String remove(long gno, RedirectAttributes redirectAttributes) {


        log.info("gno: " + gno);

        service.remove(gno);

        redirectAttributes.addFlashAttribute("msg", gno);

        return "redirect:/guestbook/list";

    }
```

<br>

> #### **line 9:** redirectAttributes.addFlashAttribute("msg", gno)으로 인해서 /guestbook/list 내부로 msg라는 이름으로 gno 값이 전달된다.<br>

<br>

삭제 작업은 GET 방식으로 수정 페이지에 드어가서 '삭제' 버튼을 클릭하는 방식으로 제작한다. modify.html에는 삭제 외에도 다른 버튼들도 있음으로 이들을 구분하기 위해서 클래스 속성을 아래와 같이 추가한다.

**modify.html 일부**

```html
(...)
<button type="button" class="btn btn-primary modifyBtn">Modify</button>

<button type="button" class="btn btn-info listBtn">List</button>

<button type="button" class="btn btn-danger removeBtn">Remove</button>
(...)
```

<br>

삭제 버튼을 클릭할 때의 이벤트 처리는 아래와 같이 구성한다.

**modify.html 일부**

```html
(...)
<button type="button" class="btn btn-danger removeBtn">Remove</button>

<script th:inline="javascript">
  var actionForm = $("form");

  $(".removeBtn").click(function () {
    actionForm.attr("action", "/guestbook/remove").attr("method", "post");

    actionForm.submit();
  });
</script>
(...)
```

<br>

> #### **line 5:** <form> 태그를 가져온다<br>
>
> #### **line 7~10:** removeBtn 클래스를 가져와서 그것을 클릭하면 <form> 태그가 등록되어 있는 removBtn 클래스에 action 속성과 method 속성을 추가한다.<br>

<br>

'Remove' 버튼을 클릭하면 `<form>` 태그의 action 속성과 method 속성을 조정한다. `<form>` 태그 내에는 `<input>` 태그로 name이 'gno'로 된 gno가 있기 때문에 컨트롤러에서는 remove 메소드 파라미터의 long gno랑 매핑이 된다. 여러 파라미터 중에서 gno를 추출해서 삭제 시에 이용하게 된다. 삭제 후에는 다시 목록 1페이지로 이동하게 된다.

<br>

수정 처리는 POST 방식으로 이루어져야 하는데 다음과 같은 점들을 고려해야 한다.

- 수정 시에 수정해야 하는 내용('제목', '내용', '글번호')이 전달되어야 한다.
- 수정된 후에는 목록 페이지로 이동하거나 조회 페이지로 이동해야 한다. 이대 가능하면 기존의 페이지 번호를 유지하는 것이 좋다.

현재 modify.html에는 '/guestbook/read'로 이동할 때 페이지 번호(page)가 파라미터로 전달되고 있고, 수정 페이지로 이동할 경우에도 간티 전달된다.

이를 이용해서 수정이 완료된 후에도 다시 동일한 정보를 유지할 수 있도록 page 값 역시 `<form>` 태그에 추가해서 전달한다. 이는 차후 GuestbookController에서 전달해준다.

**modify.html 일부**

```html
(...)
<h1 class="mt-4">GuestBook Modify Page</h1>

<form action="/guestbook/modify" method="post">
  <!--페이지 번호  -->
  <input type="hidden" name="page" th:value="${requestDTO.page}" />
  (...)
</form>
```

<br>

GuestbookController에서는 Guestbook 자체의 수정과 페이징 관련 데이터 처리를 같이 진행해야 한다.

**GuestbookController.java**

```java
    @PostMapping("/modify")
    public String modify(GuestbookDTO dto,
                         @ModelAttribute("requestDTO") PageRequestDTO requestDTO,
                         RedirectAttributes redirectAttributes) {


        log.info("post modify.........................................");
        log.info("dto: " + dto);

        service.modify(dto);

        redirectAttributes.addAttribute("page", requestDTO.getPage());
        redirectAttributes.addAttribute("gno", dto.getGno());


        return "redirect:/guestbook/read";

    }
```

<br>

GuestbookController에서는 세 개의 파라미터가 사용되는 것을 볼 수 있다. 수정해야 하는 글의 정보를 가지는 GuestbookDTO, 기존의 페이지 정보를 유지하기 위한 PageRequestDTO, 마지막으로 리다이렉트로 이동하기 위한RedirectAttributes가 필요하다. 수정 작업이 진행된 이후에는 조회 페이지로 이동한다. 이때 기존 페이지 정보도 같이 유지해서 조회 페이지에서 다시 목록 페이지로 이동하는데 어려움이 없도록 한다.

<br>

컨트롤러를 호출하는 화면에서는 'Modify' 버튼의 이벤트 처리를 통해서 작업한다.

**Modify.html**

```html
(...) $(".modifyBtn").click(function() { if(!confirm("수정하시겠습니까?")){
return ; } actionForm .attr("action", "/guestbook/modify")
.attr("method","post") .submit(); }); (...)
```

<br>

브라우저에서는 사용자에게 글의 수정 여부를 확인하고 POST 방식으로 서버에 요청한다. 컨트롤러에서 처리 이후에는 조회 페이지로 다시 이동한다.

<br>

글의 수정과 삭제가 완료되었다면 마지막으로 다시 목록 페이지로 이동하는 버튼을 처리해야 한다. 현재 modify.html은 `<form>` 태그를 이용해서 모든 작업이 이루어지고 있고 여러 개의 `<input>` 을 이용해서 파라미터들을 전송한다. 목록 페이지로 이동하는 경우에는 page와 같은 파라미터 외에 다른 파라미터들은 별도로 필요하지 않다는 것이다. 따라서 목록으로 이동할 경우에는 page를 제외한 파라미터들은 지운 상태로 처리하는 것이 깔끔하다.

**modify.html 일부**

```html
$(".btn-list").click(function(){ var pageInfo=$("input[name='page']");
actionForm.empty(); actionForm.append(pageInfo); //guestbook/list url로
pageInfo를 보낸다. actionForm .attr("action", "/guestbook/list")
.attr("method","get"); console.log(actionForm.html()); actionForm.submit(); });
```

<br>

이벤트 처리 시에는 우선 page와 관련된 부분만 따로 보관하고 empty()를 이용해서 `<form>` 최근의 모든 파라미터는 삭제한다. 빈 `<form>` 태그에 보관해둔 page 관련 정보를 추가하고 목록 페이지로 이동하도록 구현한다. 브라우저에서는 'List' 버튼을 클릭하는 경우 원래의 페이지로 다시 이동해야 한다.

---

다음 게시물에서는 검색에 대한 처리를 한다.
