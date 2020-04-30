# HTML/CSS3 - Markup Board

### Markup Board

``` html
<!-- board 영역을 감싼다 -->
<div class="board">
    <!-- 공지사항 영역 -->
    <section class="notice tab-act">
        <h2 class="notice-heading">
            <a href="#" class="tab" role="button" id="notice">공지사항</a>
        </h2>
        <ul class="notice-list">
            <li class="icon-dot-circled">
                <a href="#">HTML의 모든 것을 알려주마 샘플 활용법</a>
                <time datetime="2018-05-31T13:53:45">2018.05.31</time>
            </li>
            <li class="icon-dot-circled">
                <a href="#">W3C 사이트 리뉴얼 및 공지사항</a>
                <time datetime="2018-05-31T13:53:45">2018.05.31</time>
            </li>
            .
            .
            .
        </ul>
        <!-- link <a> to a#notice -->
        <a href="#" class="icon-plus notice-more more"
           title="공지사항" aria-labelledby="notice">더보기</a>
    </section>
	
    <!-- 자료실 영역 -->
    <section class="pds">
        <h2 class="pds-heading" id="pds-heading">
            <a href="#" class="tab" role="button" id="pds">자료실</a>
        </h2>
        <ul class="pds-list">
            <li class="icon-dot-circled">
                <a href="#">디자인 사이트 링크 모음</a>
                <time datetime="2018-05-31T13:53:45">2018.05.31</time>
            </li class="icon-dot-circled">
            <li class="icon-dot-circled">
                <a href="#">웹 접근성 관련 자료 모음</a>
                <time datetime="2018-05-31T13:53:45">2018.05.31</time>
            </li>
            .
            .
            .
        </ul>
        <a href="#" class="icon-plus pds-more more"
           title="자료실" aria-labelledby="pds">더보기</a>
    </section>
</div>
```

* board 영역 (`div`) 안에 공지사항 (`section`) 영역과 자료실 영역 (`section`)을 생성한다
* 각 `section`의 `heading`을 나란히 배치하여 탭 메뉴를 만든다
* 각 `heading` 속 `a.tab` 영역이 **클릭되면,** 해당 `section`에 `tab-act` 클래스를 부여한다 (jQuery)

```javascript
var section = $('.board section');
var tab = $('.tab');

// 'e' as event
tab.on('click', function(e){
    e.preventDefault(); // cancel default function (ex. href="url")
    if((e.keyCode === 13 && e.type === 'keyup') || e.type ==='click') {
        section.removeClass('tab-act');
        $(this).parent().parent().addClass('tab-act');
    }
});
```

* `tab-act` 클래스를 부여 받은 `section`은 CSS로 `display: block` 속성을 부여하고, 그 반대의 경우는 `display: none` 처리해준다

``` css
.board ul, .board .more{
  display: none;
}
.tab-act ul, .tab-act .more{
  display: block !important;
}
```

