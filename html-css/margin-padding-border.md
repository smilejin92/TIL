# CSS - Padding, Borders, and Margins

## Margin

마진(Margin)이란 박스(요소) 주변의 보이지 않는 여백을 의미한다. 마진은 주변의 다른 요소를 밀어낸다. 마진은 양수 값과 음수 값을 모두 가질 수 있다. 요소의 한 부분에 음수 마진을 지정하면 페이지의 다른 요소들과 겹칠 수 있다. 박스 모델에 관계 없이 마진은 항상 눈에 보이는(visible) 박스의 영역이 계산된 후 더해진다.

`margin` 속성을 사용하여 요소의 모든 면에 대한 마진을 한 번에 설정할 수 있으며, 개별적으로도 설정할 수 있다.

* `margin`
* `margin-top`
* `margin-right`
* `margin-bottom`
* `margin-left`

```html
<!-- margin 사용 예제 -->
<style>
  .container {
    border: 5px solid tomato;
    height: 300px;
    margin: 50px;
  }
  
  .box {
    background-color: lightgreen;
    height: 200px;
    margin-top: -40px;
    margin-right: 30px;
    margin-bottom: 40px;
    margin-left: 4em;
    /* margin: -40px 30px 40px 4em; */
  }
</style>

<div class="container">
  <div class="box">box with margin</div>
</div>
```

<img src="/Users/smilejin92/Desktop/Screen Shot 2020-04-20 at 8.49.02 PM.png" style="zoom:50%;" />

위 예제에서 `.box` 클래스(연두색)를 가진 요소가 자신의 컨테이너 요소(주황색) 밖으로 튀어나온 것을 볼 수 있다. 이처럼 음수 마진 값을 적용하여 요소가 끌어당겨진 것 같은 효과를 연출할 수 있다. 단, 위 예제의 경우 컨테이너 요소에 마진 혹은 패딩 속성을 지정하여 연두색 요소가 끌어당겨질 수 있는 영역을 만들어 주어야한다.

&nbsp;  

### Margin Collapsing (마진 겹침)

마진을 이해하려면 우선 **마진 겹침 현상**이 무엇인지 알고 있어야한다. 만약 마진이 맞닿는 두 요소가 있고, **마진의 값이 모두 양수일 경우 두 마진은 하나의 마진으로 병합되며, 두 마진 값 중 더 큰 값으로 적용된다.** 또한, **마진이 맞닿는 두 요소가 있고, 하나 또는 두 개의 마진 영역이 모두 음수인 경우 음수 값은 전체 영역에서 차감된다.**

아래 예제는 두 개의 단락 요소(`<p>`)를 포함하고 있다. 첫 번째 단락 요소는 `margin-bottom` 속성의 값으로 50px를 갖는다. 두 번째 단락 요소는 `margin-top` 속성의 값으로 30px을 갖는다. 두 요소의 마진이 맞닿아있고, 마진의 값이 모두 양수이므로 마진은 하나의 영역으로 병합된다. 이 때 50px이 30px보다 크기 때문에 하나로 합쳐진 마진의 값은 50px이된다.

두 번째 단락 요소의 `margin-top` 속성 값으로 0을 지정하여도 변화는 없다. 두 요소가 맞닿는 부분의 마진 값으로 각각 50px, 0씩 가지기 때문에 50px의 여백은 그대로 존재한다. 만약 두 번째 단락 요소의 `margin-top` 속성 값을 -10px으로 지정할 경우, 전체 영역(50px)에서 음수 값을 차감한만큼(40px) 여백이 생성된다.

<img src="/Users/smilejin92/Desktop/Screen Shot 2020-04-20 at 10.35.39 PM.png" style="zoom:50%;" />

```html
<style>
  .one {
    margin-bottom: 50px;
  }
  
  .two {
    margin-top: 30px;
  }
</style>

<div class="container">
  <p class="one">I am paragraph one.</p>
  <p class="two">I am paragraph two.</p>
</div>
```

마진이 겹치거나 겹치지 않을 때를 구분하는 몇가지 규칙이 있다. 자세한 내용은 [mastering margin collapsing](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)에서 살펴보길 바란다. 기억해야할 것은 마진 겹침 현상이 발생한다는 사실 그 자체이다. 마진을 활용하여 여백을 생성할 경우, 의도한대로 결과가 나오지 않는다면 아마 마진 겹침 현상이 생긴 것일 수도 있다.

&nbsp;  

## Borders

보더는 상자의 마진과 패딩 사이의 그려진 테두리를 말한다. 스탠다드 박스 모델을 사용할 경우, 보더의 크기는 상자의 `width`와 `height`에 더해진다. 대체 박스 모델을 사용할 경우, 보더의 크기는 `width`와 `height`에 포함되기 때문에 컨텐트 박스를 작게 만든다.

보더를 스타일링할 수 있는 속성은 아래와 같다. 네 개의 보더가 있고, 각 보더의 스타일, 두께, 색을 변경할 수 있다. `border` 속성을 사용하여 두께, 스타일, 혹은 컬러를 한번에 지정할 수도 있다.

각 보더의 속성을 개별적으로 지정할 경우 아래 속성을 사용할 수있다.

* `border-top`
* `border-right`
* `border-bottom`
* `border-left`

보더의 두께와, 스타일, 색을 일괄적으로 지정할 경우 아래 속성을 사용할 수 있다.

* `border-width`
* `border-style`
* `border-color`

각 보더의 두께, 스타일, 색을 개별적으로 지정할 경우 아래 속성을 사용할 수 있다.

* `border-top-width`
* `border-top-style`
* `border-top-color`
* `border-right-width`
* `border-right-style`
* `border-right-color`
* `border-bottom-width`
* `border-bottom-style`
* `border-bottom-color`
* `border-left-width`
* `border-left-style`
* `border-left-color`

아래는 단축 표기법와 일반 표기법을 사용하여 보더의 스타일을 지정한 예제이다.

<img src="/Users/smilejin92/Desktop/Screen Shot 2020-04-21 at 6.09.23 PM.png" style="zoom:50%;" />

```html
<style>
	.container {        
    border-top: 5px dotted green;
    border-right: 1px solid black;
    border-bottom: 20px double rgb(23,45,145);
	}

  .box {
    background-color: lightgray;
    height: 150px;
    border: 2px solid #333333;
    border-top-style: dotted;
    border-right-width: 20px;
    border-bottom-color: hotpink;
  }
</style>

<div class="container">
  <div class="box">box with border</div>
</div>
```

&nbsp;  

## Padding

