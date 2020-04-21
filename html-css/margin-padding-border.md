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

<img src="https://user-images.githubusercontent.com/32444914/79850879-7b7e5f00-83ff-11ea-98a9-3fe45e1677bf.png" style="zoom:50%;" />

위 예제에서 `.box` 클래스(연두색)를 가진 요소가 자신의 컨테이너 요소(주황색) 밖으로 튀어나온 것을 볼 수 있다. 이처럼 음수 마진 값을 적용하여 요소가 끌어당겨진 것 같은 효과를 연출할 수 있다. 단, 위 예제의 경우 컨테이너 요소에 마진 혹은 패딩 속성을 지정하여 연두색 요소가 끌어당겨질 수 있는 영역을 만들어 주어야한다.

&nbsp;  

### Margin Collapsing (마진 겹침)

마진을 이해하려면 우선 **마진 겹침 현상**이 무엇인지 알고 있어야한다. 만약 마진이 맞닿는 두 요소가 있고, **마진의 값이 모두 양수일 경우 두 마진은 하나의 마진으로 병합되며, 두 마진 값 중 더 큰 값으로 적용된다.** 또한, **마진이 맞닿는 두 요소가 있고, 하나 또는 두 개의 마진 영역이 모두 음수인 경우 음수 값은 전체 영역에서 차감된다.**

아래 예제는 두 개의 단락 요소(`<p>`)를 포함하고 있다. 첫 번째 단락 요소는 `margin-bottom` 속성의 값으로 50px를 갖는다. 두 번째 단락 요소는 `margin-top` 속성의 값으로 30px을 갖는다. 두 요소의 마진이 맞닿아있고, 마진의 값이 모두 양수이므로 마진은 하나의 영역으로 병합된다. 이 때 50px이 30px보다 크기 때문에 하나로 합쳐진 마진의 값은 50px이된다.

두 번째 단락 요소의 `margin-top` 속성 값으로 0을 지정하여도 변화는 없다. 두 요소가 맞닿는 부분의 마진 값으로 각각 50px, 0씩 가지기 때문에 50px의 여백은 그대로 존재한다. 만약 두 번째 단락 요소의 `margin-top` 속성 값을 -10px으로 지정할 경우, 전체 영역(50px)에서 음수 값을 차감한만큼(40px) 여백이 생성된다.

<img src="https://user-images.githubusercontent.com/32444914/79850888-7e794f80-83ff-11ea-877e-1327d4731b5f.png" style="zoom:50%;" />

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

<img src="https://user-images.githubusercontent.com/32444914/79850893-7faa7c80-83ff-11ea-84ce-e77fcad8a8a6.png" style="zoom:50%;" />

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

패딩은 보더와 컨텐트 영역 사이에 존재하는 박스 안쪽의 여백을 말한다. 마진과 다르게 패딩 속성은 음수 값을 가질 수 없다. 따라서 패딩 속성의 값은 0 이상이어야 한다. 요소에 적용된 배경은 패딩 뒤편에 적용되며, 일반적으로 컨텐츠를 보더에서 밀어내기 위해 사용한다.

`padding` 속성을 사용하여 박스 각 면의 패딩을 지정할 수 있다. 또한 개별 속성을 사용하여도 각 면의 패딩을 지정할 수 있다. 개별 속성은 아래와 같다.

* `padding-top`
* `padding-right`
* `padding-bottom`
* `padding-left`

아래 예제에서 `container` 클래스를 가진 요소는, `box` 클래스를 가진 요소를 안쪽으로 밀어낸다. 또한 `box` 클래스를 가진 요소는 자신이 포함하는 텍스트를 오른쪽으로 밀어낸다.

![](https://user-images.githubusercontent.com/32444914/79854172-03666800-8404-11ea-9821-5e55de05c0ae.png)

```html
<style>
	.box {
    padding-top: 0;
    padding-right: 30px;
    padding-bottom: 40px;
    padding-left: 4em;
  }

  .container {
    padding: 20px;
  }
</style>

<div class="container">
  <div class="box">box with padding</div>
</div>
```

&nbsp;  

## 박스 모델과 인라인 상자

위에서 설명한 마진, 보더, 패딩 속성은 블록 상자에 전체적으로 적용된다. 각 속성은 `<span>` 요소와 같은 인라인 상자에도 일부 적용된다.

아래 예제에서 단락 요소는 `width`, `height`, `margin`, `border`, `padding` 속성이 적용된 `<span>` 요소를 포함하고있다. 인라인 상자는 `width`, `height` 속성이 적용되지 않는다. `margin`, `padding`, `border` 속성은 적용되었지만, 주변 요소와의 관계를 무너트리지 않는다. 패딩과 보더가 주변 글자와 겹쳐지는 것을 보면 이러한 내용을 확인할 수 있다. 단, 주의해야할 것은 **인라인 상자는 주변 요소를 자신의 좌우 패딩, 보더, 마진 값만큼 밀어낸다는 것**이다.

![](https://user-images.githubusercontent.com/32444914/79855841-7a046500-8406-11ea-960a-312b9ae616a8.png)

```html
<style>
	.paragraph {        
    border: 5px solid black;
    padding: 20px;
  }

  .inlinebox {
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 2px solid blue;
    margin: 10px;
  }
</style>

<p class="paragraph">
  I am a paragraph and this is a <span class="inlinebox">span</span> inside that paragraph. A span is an inline element and so does not respect width and height.
</p>
```

&nbsp;  

## display: inline-block 사용

`inline-block` 디스플레이 타입은 `inline`과 `block` 디스플레이 타입의 특징을 모두 가진 속성이다. 해당 속성을 가진 요소는 줄바뀜이 발생하지 않고, `width`와 `height` 속성이 적용될 수 있다. 또한 `padding`, `margin`, `border` 속성이 적용되며, 적용된 값만큼 인접한 상하좌우의 요소를 밀어낸다.

`inline-block` 속성을 가진 요소에 `width와 `height`을 지정하지 않으면, 컨텐트 상자는 컨텐츠의 크기에 맞게 생성된다.

![](https://user-images.githubusercontent.com/32444914/79862171-aae99780-8410-11ea-9253-d553981c3f66.png)

```html
<style>
	p {        
    border: 5px solid black;
    padding: 20px;
  }

  span {
    display: inline-block;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid blue;
    margin: 10px;
  }
</style>

<p>
  I am a paragraph and this is a <span>span</span> inside that paragraph. A span is an inline element and so does not respect width and height.
</p>
```

`inline-block` 속성은 클릭/터치될 수 있는 영역이 넓은 링크를 제공할 때 유용하다. `<a>` 요소는 `<span>` 요소와 같은 인라인 요소지만, `display: inline-block` 속성을 지정한 후 패딩 영역을 확장하면 사용자가 링크를 쉽게 클릭/터치할 수 있다. 

&nbsp;  

## 참고 자료

* [MDN Web Docs - The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)

