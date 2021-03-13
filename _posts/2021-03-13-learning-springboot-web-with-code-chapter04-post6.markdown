---
layout: post
title: 코드로 배우는 스프링 부트 웹 프로젝트-Part2-06
date: 2021-03-13 13:00:00 0000
tags: [Intellij, SpringBoot, Guesbook]
categories: [SpringBoot]
description: 방명록 만들기
---

<br><br>

# <center>검색처리</center>

<br>

이번 게시물에서는 화면에서 검색 처리 기능을 추가해 본다. 검색 처리는 크게 서버 사이드 처리와 화면 쪽의 처리로 나뉜다.

서버 사이드 처리는 다음과 같다.

- PageRequestDTO에 검색 타입(type)과 키워드(keyword)를 추가
- 이하 서비스 계층에서 Querydsl을 이용해서 검색 처리

<br>

검색 항목은 크게 다음과 같이 정의한다.

- '제목(t), 내용(c), 작성자(w)'로 검색하는 경우
- '제목 혹은 내용(tc)'으로 검색하는 경우
- '제목 혹은 내용 혹은 작성자(tcw)'로 검색하는 경우

<br>

가장 우선으로 PageRequestDTO을 검색 조건(type)과 검색 키워드(keyword)를 추가한다.

**PageRequestDTO.java**

```java
package org.zerock.guestbook.dto;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Pageable;
import org.springframework.data.domain.Sort;

@Builder
@AllArgsConstructor
@Data
public class PageRequestDTO {

    private int page;
    private int size;
    private String type;
    private String keyword;


    public PageRequestDTO(){
        this.page = 1;
        this.size = 10;
    }

    public Pageable getPageable(Sort sort){

        return PageRequest.of(page -1, size, sort);

    }
}

```

<br>

PageRequestDTO에서 변경된 것은 type과 keyword가 추가된 것뿐이다.

동적으로 검색 조건이 처리되는 경우의 실제 코딩은 Querydsl을 통해서 BooleanBuilder를 작성하고 GuestbookRepository는 Querydsl로 작성된 BooleanBuilder를 findAll()처리하는 용도로 사용한다. BooleanBuilder 작성은 별도의 클래스 등을 작성해서 처리할 수 있지만 간단히 하려면 GuestbookServiceImpl 내에 메서드를 하나 작성해서 처리하면 된다.

**GuestbookServiceImpl.java 일부**

```java
(...)
@Override
    public GuestbookDTO read(Long gno) {
         (...)
    }

    @Override
    public void remove(Long gno) {

         (...)

    }

    @Override
    public void modify(GuestbookDTO dto) {
        (...)
    }


    private BooleanBuilder getSearch(PageRequestDTO requestDTO){

        String type = requestDTO.getType();

        BooleanBuilder booleanBuilder = new BooleanBuilder();

        QGuestbook qGuestbook = QGuestbook.guestbook;

        String keyword = requestDTO.getKeyword();

        BooleanExpression expression = qGuestbook.gno.gt(0L); // gno > 0 조건만 생성

        booleanBuilder.and(expression);

        if(type == null || type.trim().length() == 0){ //검색 조건이 없는 경우
            return booleanBuilder;
        }


        //검색 조건을 작성하기
        BooleanBuilder conditionBuilder = new BooleanBuilder();

        if(type.contains("t")){
            conditionBuilder.or(qGuestbook.title.contains(keyword));
        }
        if(type.contains("c")){
            conditionBuilder.or(qGuestbook.content.contains(keyword));
        }
        if(type.contains("w")){
            conditionBuilder.or(qGuestbook.writer.contains(keyword));
        }

        //모든 조건 통합
        booleanBuilder.and(conditionBuilder);

        return booleanBuilder;
    }

}

```

<br>

GuestbookServiceImpl에 작성한 getSearch()는 PageRequestDTO를 파라미터로 받아서 검색 조건(type)이 있는 경우에는 conditionBuilder 변수를 생성해서 각 검색 조건을 'or'로 연결해서 처리한다. 반면에 검색 조건이 없다면 'gno>0'으로만 생성된다. GuestbookServiceImpl에서 목록을 조회할 때 사용하는 getList()는 기존의 코드를 조금 수정해서 다음과 같이 작성한다.

<br>

**GuestbookServiceImpl.java 일부**

```java
    @Override
    public PageResultDTO<GuestbookDTO, Guestbook> getList(PageRequestDTO requestDTO) {

        Pageable pageable = requestDTO.getPageable(Sort.by("gno").descending());

        BooleanBuilder booleanBuilder=getSearch(requestDTO);

        Page<Guestbook> result = repository.findAll(booleanBuilder,pageable);

        Function<Guestbook, GuestbookDTO> fn = (entity -> entityToDto(entity));


        return new PageResultDTO<>(result, fn );
    }
```

<br>

위와 같이 서비스 영역에서 검색 조건을 처리할 수 있도록 구성했다면 테스트 코드로 결과를 확인한다.

![](/images/Learning_SpringBoot_with_Web_Project/Part4/Chapter7/2021-03-13-13-34-27.png)

<br>

**GuestbookServiceTests.java 일부**

```java
@Test
    public void testSearch(){
        PageRequestDTO pageRequestDTO=PageRequestDTO.builder()
                .page(1)
                .size(10)
                .type("tc")
                .keyword("한글")
                .build();
        PageResultDTO<GuestbookDTO, Guestbook> resultDTO=service.getList(pageRequestDTO);
        System.out.println("PREV: "+resultDTO.isPrev());
        System.out.println("NEXT: "+resultDTO.isNext());
        System.out.println("TOTAL: "+resultDTO.getTotalPage());

        System.out.println("-----------------------------------");
        for(GuestbookDTO guestbookDTO:resultDTO.getDtoList()){
            System.out.println(guestbookDTO);
        }
        System.out.println("===================================");
        resultDTO.getPageList().forEach(i->System.out.println(i));

    }
```

<br>

위의 코드는 '제목(t)이나 내용(c)'에 '한글'이라는 키워드가 있는 글을 검색한다. 다시 부연 설명을 하자면 pageRequestDTO에서 size를 10으로 하는 page들로 구성하라는 의미와 'tc'는 제목과 내용을 의미한다. 거기서 keyword '한글'이라고 되어 있는 게시물을 찾는 것이다. 테스트 결과 내용과 제목이 '한글'로 되어 있는 게시물이 없기 때문에 아래와 같은 결과가 나온다.

![](/images/Learning_SpringBoot_with_Web_Project/Part4/Chapter7/2021-03-13-13-44-33.png)

<br>

검색 처리를 위해서는 화면에서 검색 타입(type)과 키워드(keyword)를 입력할 수 있는 UI가 필요하다. 검색 자체가 GET 방식이므로 한글이 아니면 간단히 GET 방식의 쿼리 스트링(query string)을 조작해서 충분히 테스트할 수 있다. 예를 들어 프로젝트를 실행한 상태에서 브라우저의 주소창에서 '/guestbook/list?page=1?type=t&keyword=11' 같이 조작하면 '제목' 안에 '11'이라는 문자열이 포함된 글들의 1페이지를 확인할 수 있다.

<br>

일단 목록 화면을 처리하는 list.html에는 '검색 타입'과 '키워드'를 입력하고 '검색' 버튼을 추가해야 한다.

![](/images/Learning_SpringBoot_with_Web_Project/Part4/Chapter7/2021-03-13-13-47-57.png)

<br>

**list.html 일부**

```html
(...)
<h1 class="mt-4">
  GuestBook List Page
  <span>
    <a th:href="@{/guestbook/register}">
      <button type="button" class="btn btn-outline-primary">REGISTER</button>
    </a>
  </span>
</h1>

<form action="/guestbook/list" method="get" id="searchForm">
  <div class="input-group">
    <input type="hidden" name="page" value="1" />
    <div class="input-group-prepend">
      <select class="custom-select" name="type">
        <option th:selected="${pageRequestDTO.type == null}">-------</option>
        <option value="t" th:selected="${pageRequestDTO.type =='t'}">
          제목
        </option>
        <option value="c" th:selected="${pageRequestDTO.type =='c'}">
          내용
        </option>
        <option value="w" th:selected="${pageRequestDTO.type =='w'}">
          작성자
        </option>
        <option value="tc" th:selected="${pageRequestDTO.type =='tc'}">
          제목 + 내용
        </option>
        <option value="tcw" th:selected="${pageRequestDTO.type =='tcw'}">
          제목 + 내용 + 작성자
        </option>
      </select>
    </div>
    <input
      class="form-control"
      name="keyword"
      th:value="${pageRequestDTO.keyword}"
    />
    <div class="input-group-append" id="button-addon4">
      <button class="btn btn-outline-secondary btn-search" type="button">
        Search
      </button>
      <button class="btn btn-outline-secondary btn-clear" type="button">
        Clear
      </button>
    </div>
  </div>
</form>
(...)
```

<br>

list.html에는 새롭게 하나의 \<form> 태그와 \<select> 태그 등이 추가되었다. \<select> 태그는 검색 타입을 선택하는 용도로 사용하는데 PageRequestDTO를 이용해서 검색 타입에 맞게 자동으로 선택될 수 있도록 구성한다. 키워드는 \<input> 태그로 처리한다. 여기까지 구성한 상태에서 '/guestbook/list?page=1&type=t&keyword=11'과 같이 브라우저의 주소창을 조작하면 해당 검색 타입과 키워드가 입력된 형태로 출력되는 것을 볼 수 있다.

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part4/Chapter7/2021-03-13-14-01-07.png)

<br>

'Search' 버튼을 누르는 것은 새롭게 검색을 진행하는 것이므로 무조건 1페이지를 지정하도록 한다. 'Clear' 버튼을 클릭하면 모든 검색 조건 없이 새로 목록 페이지를 보는 것을 의미한다. 이제 list.html 아래쪽에 이벤트 처리를 다음과 같이 추가한다.

**list.html의 하단**

```html
(...)
<script th:inline="javascript">

  var msg = [[${msg}]];

  console.log(msg);

  if(msg){
      $(".modal").modal();
  }
  var searchForm = $("#searchForm");

  $('.btn-search').click(function(e){

      searchForm.submit();

  });

  $('.btn-clear').click(function(e){

      searchForm.empty().submit();

  });
</script>
```

<br>

'btn-search'를 클릭하면 새롭게 선택된 검색 타입과 키워드로 1페이지를 검색하고, 'btn-clear'를 클릭하면 모든 검색과 관련된 내용을 삭제하고 검색이 없는 목록 페이지를 호출한다. 예를 들어 '제목+내용'을 선택하고 키워드를 '123'으로 하면 다음과 같이 처리 된다.(아래 첫 번째 사진) 만일 화면에서 'Clear' 버튼을 클릭하면 모든 검색 조건과 페이지 번호는 초기화 된다. (아래 두 번째 사진)

![](/images/Learning_SpringBoot_with_Web_Project/Part4/Chapter7/2021-03-13-14-05-13.png)

<br>

![](/images/Learning_SpringBoot_with_Web_Project/Part4/Chapter7/2021-03-13-14-05-28.png)

<br>

목록 페이지 하단의 검색은 단순히 page라는 값만을 처리하므로, 검색 타입(type)과 키워드(keyword)를 추가해 주어야 한다.

**list.html 일부**

```html
<ul class="pagination h-100 justify-content-center align-items-center">
  <li class="page-item " th:if="${result.prev}">
    <a
      class="page-link"
      th:href="@{/guestbook/list(page= ${result.start -1},
                    type=${pageRequestDTO.type} ,
                    keyword = ${pageRequestDTO.keyword} ) }"
      tabindex="-1"
      >Previous</a
    >
  </li>

  <li
    th:class=" 'page-item ' + ${result.page == page?'active':''} "
    th:each="page: ${result.pageList}"
  >
    <a
      class="page-link"
      th:href="@{/guestbook/list(page = ${page} ,
                   type=${pageRequestDTO.type} ,
                   keyword = ${pageRequestDTO.keyword}  )}"
    >
      [[${page}]]
    </a>
  </li>

  <li class="page-item" th:if="${result.next}">
    <a
      class="page-link"
      th:href="@{/guestbook/list(page= ${result.end + 1} ,
                    type=${pageRequestDTO.type} ,
                    keyword = ${pageRequestDTO.keyword} )}"
      >Next</a
    >
  </li>
</ul>
```

<br>

목록 페이지에서 마지막으로 처리해야 하는 내용은 특정 글의 번호를 클릭해서 이동하는 부분이다. 이는 페이지 처리와 동일하게 type과 keyword 항목을 추가하면 된다.

**list.html 일부**

```html
(...)
<tr th:each="dto : ${result.dtoList}">
  <th scope="row">
    <a
      th:href="@{/guestbook/read(gno = ${dto.gno},
           page= ${result.page},
           type=${pageRequestDTO.type} ,
        keyword = ${pageRequestDTO.keyword})}"
    >
      [[${dto.gno}]]
    </a>
  </th>
  <td>[[${dto.title}]]</td>
  <td>[[${dto.writer}]]</td>
  <td>[[${#temporals.format(dto.regDate, 'yyyy/MM/dd')}]]</td>
</tr>
(...)
```

<br>

화면에서는 특정 글의 번호를 선택하면 기존과 다르게 type과 keyword 파라미터가 추가로 전송되는 것을 볼 수 있다.

<br>

기존의 조회 페이지는 page 값만 처리했기 때문에 다시 목록으로 돌아가는 링크 앞에서 처리한 것과 동일하게 type과 keyword 값을 추가해 주어야 한다. 조회 페이지는 PageRequestDTO를 컨트롤러에서 @ModealAttribute를 이용해서 'requestDTO'라는 이름으로 처리하고 있다.

**read.html 하단의 링크 처리**

```html
<a
  th:href="@{/guestbook/modify(gno = ${dto.gno}, page=${requestDTO.page},
   type=${requestDTO.type}, keyword =${requestDTO.keyword})}"
>
  <button type="button" class="btn btn-primary">Modify</button>
</a>

<a
  th:href="@{/guestbook/list(page=${requestDTO.page} , 
  type=${requestDTO.type}, keyword =${requestDTO.keyword})}"
>
  <button type="button" class="btn btn-info">List</button>
</a>
```

<br>

조회 페이지의 검색 처리는 다음과 같은 순서로 확인할 수 있다.

- 목록 페이지에서 특정한 조건으로 검색을 수행
- 검색한 상태에서 특정 글을 선택해서 조회 페이지로 이동
- 조회 페이지에서 목록 페이지로 이동하는 버튼을 클릭해서 이동

<br>

GuestbookController는 작업이 끝난 후에 RedirectAttributes를 이용해서 이동하는 경우가 종종 있다.

- 등록 처리: 1페이지로 이동
- 삭제 처리: 1페이지로 이동
- 수정 처리: 조회 페이지로 이동

<br>

수정은 다시 조회 페이지로 이동하기 때문에 검색 조건을 같이 유지해야만 한다. 조회 페이지에서는 다음과 같이 page뿐 아니라 type과 keyword를 처리해야 한다.

\*modify.html 일부\*\*

```html
(...)
<form action="/guestbook/modify" method="post">
  <!--페이지 번호  -->
  <input type="hidden" name="page" th:value="${requestDTO.page}" />
  <input type="hidden" name="type" th:value="${requestDTO.type}" />
  <input type="hidden" name="keyword" th:value="${requestDTO.keyword}" />

  <div class="form-group">
    <label>Gno</label>
    <input
      type="text"
      class="form-control"
      name="gno"
      th:value="${dto.gno}"
      readonly
    />
  </div>
  (...)
</form>
```

<br>

기존의 코드에 type과 keyword 부분이 추가된 것을 볼 수 있다. 수정 페이지에서 다시 목록 페이지로 이동하는 경우에도 type과 keyword가 같이 전달될 수 있도록 이벤트 처리 부분도 약간 수정이 필요하다.

**modify.html 일부**

```html
(...) $(".listBtn").click(function() { var page = $("input[name='page']"); var
type = $("input[name='type']"); var keyword = $("input[name='keyword']");
actionForm.empty(); //form 태그의 모든 내용을 지우고 actionForm.append(page);
actionForm.append(type); actionForm.append(keyword); actionForm .attr("action",
"/guestbook/list") .attr("method","get"); actionForm.submit(); }) (...)
```

<br>

수정된 부분은 page뿐 아니라 type과 keyword 부분도 같이 보관했다가 <form> 태그와 같이 전송하도록 수정한 것이다. 수정 작업의 마지막은 GuestbookController에서 수정한 후에 페이지로 리다이렉트 처리될 대 검색 조건을 유지하도록 추가해 주는 것이다.

**GuestbookController.java**

```java
(...)
 @PostMapping("/modify")
    public String modify(GuestbookDTO dto,
                     @ModelAttribute("requestDTO") PageRequestDTO requestDTO,
                        RedirectAttributes redirectAttributes) {


    log.info("post modify.........................................");
    log.info("dto: " + dto);

    service.modify(dto);

    redirectAttributes.addAttribute("page", requestDTO.getPage());
    redirectAttributes.addAttribute("type", requestDTO.getType());
    redirectAttributes.addAttribute("keyword", requestDTO.getKeyword());

    redirectAttributes.addAttribute("gno", dto.getGno());


    return "redirect:/guestbook/read";

}
    (...)
```

<br>

최종적인 실행 결과는 수정한 후에 다시 원래의 정보를 그대로 유지하는 조회 페이지로 이동하는 것이다. 이때 목록과 검색 관련 데이터도 같이 유지가 된다.
