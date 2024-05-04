# HTML/CSS 과제
float과 flex를 활용한 레이아웃 작업하기

## _과제내용_
다음 조건을 만족할 수 있도록 마크업과 스타일링을 완성하자.

- 아바타 이미지는 배경 방식이 아닌 콘텐츠 이미지(\<img\> 요소)로 마크업한다.
- 아바타의 상태 정보를 알 수 있도록 정보를 제공한다.
- 아바타 이미지의 크기 - 64px X 64px
- 아바타 이미지 간의 간격 - 20px
- 회색 원 배경색 - #DBDBDB <span style="color:#dbdbdb;">●</span>
- 초록색 원 배경색- #4CFE88 <span style="color:#4CFE88;">●</span>
- `float`을 사용하여 다음의 레이아웃을 구현해 본다. (여성그룹이 상위 배치)
- `flex`를 지원하는 환경에서는 다음과 같이 배치되도록 레이아웃을 구현해 본다. (남성그룹이 상위배치)
- 아바타 과제 수행에 대한 설명을 `avatars.md` 파일에 작성하고 `homework` 폴더에 있는 `README.md`에 링크로 연결한다.
- 과제는 `5월 4일 오후 11시 59분`까지 Github 저장소에 Push 한다.

&nbsp;


# 과제 수행
## 1. 구조설계
### HTML <!DOCTYPE> 선언

```html:avatars.html

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Avatars</title>
</head>
<body>
  
</body>
</html>
```
&nbsp;



### 스타일 지정을 위해 avatars.css 파일을 연결
```html:avatars.html

<link rel="stylesheet" href="avatars.css" />
```
&nbsp;

### html 뼈대 작업
여기까지 작업해두고 과제내용을 다시 살펴보며 마크업 방향을 정리해보았다.

- 일단은 목록이니까 ul>li 구조로 작업하고 class는 ul.avatars_list>li.avatar로 하기
- 디자인상 ul이 회색박스의 가운데에 위치하도록 하기위해 ul 전체를 감싸는 div를 만들고 class는 avatars_wrapper로 하기,  role="application"으로 롤 부여
- 프로필 이미지와 상태표시 원은 li의 자식이지만 둘은 형제관계로 마크업하고, 상태표시 원은 span 요소로 작업하기

이렇게 큰 뼈대를 생각하고 아래 구조로 마크업 
```html:avatars.html

div.avatars_wrapper>ul.avatars_list>li.avatar.avatar$*8>img+span.avatars_state
```
&nbsp;

### html 디테일 작업
상태표시 원은 의미가 없는 요소라고 생각했지만 `접속중/자리비움`을 표시해주는 중요한 요소라는 생각이 듦
- 그래서 상태표시 원을 span으로 작업하되 접근성을 높이기 위해 `aria-label` 속성을 추가해서 `aria-label="자리비움"`, ` aria-label="접속중"` 으로 상태를 알 수 있도록 함
- 회색과 초록색의 스타일 적용을 위해 접속중일 경우에는 span에 class="on"을 추가

&nbsp;

> 이 시점에서 img 태그에 alt 속성을 작성하려고 했지만 li에 aria-label로 대체텍스트를 넣어주면 접근성이 더 향상되지 않을까 고민해보았다.  
> 그래도 이미지를 설명하는 대체텍스트는 img의 alt 속성을 사용하는 것이 필수이니 일단은 원칙대로 하기로 했다.  
> 이 부분에 대해서는 조금 더 고민이 필요할 것 같다.

&nbsp;

과제의 내용에서 `flex가 지원되는 브라우저 환경에서는 남성과 여성의 순번이 바뀌게 구현하라`는 요구사항 때문에 마크업을 어떻게 해야할지 가장 큰 고민이 되었다.
1. 여성 아바타 그룹과 남성 아바타 그룹을 크게 나눠서 마크업해야할 지
2. 아바타를 성별에 관계없이 모두 하나의 그룹으로 지은 뒤에 작업할 지

혹여 단순히 여성그룹과 남성그룹의 순서를 바꿔달라는 요청이 아닐 수도 있기 때문에 아래와 같이 작업하였다.
- 성별 그룹을 하나의 ul에 넣어서 마크업
- ul의 하위인 li에 female 과 male라는 class를 추가해 성별 구분
- 아바타의 순서를 단순히 성별이 아닌 하나하나 지정해서 변경해야할 상황을 대비하여 li에 각각의 class 부여 (avatar1~avatar8)

```html:avatars.html

  <div role="application" class="avatars_wrapper">
    <ul aria-label="아바타 목록" class="avatars_list">
      <li aria-label="아바타1" class="avatar avatar1 female">
        <img src="./images/faces/face1.jpg" alt="" />
        <span aria-label="자리비움" class="avatars_state"></span>
      </li>      
      <li aria-label="아바타2" class="avatar avatar2 female">
        <img src="./images/faces/face2.jpg" alt="" />
        <span aria-label="접속중" class="avatars_state on"></span>
      </li>
      .
      .
      <li class="avatar avatar5 male">...</li>
      .
      .
      <li class="avatar avatar8 male">...</li>
    </ul>
  </div>
```




&nbsp;

## 2. 스타일 지정
### ul, li의 user agent style 초기화
- ul, li 의 user agent style에 있는 list-style 과 margin, padding 값 초기화  
```css:avatars.css

ul, li{list-style:none;margin:0;padding:0;}
```
&nbsp;

### 전체적인 레이아웃 style 작업
### _- float을 사용한 레이아웃 구성_
- 목록 전체를 감싸고 있는 div.avatars_wrapper 에 style 지정
- 먼저 li를 float으로 배치하는 기본적인 레이아웃을 구현함
- img를 감싸고 있는 li의 높이값이 딱맞게 떨어지지 않아 li에 line-height:0.5 값을 부여
- 상태표시 회색 원이 활성화 될 경우는 class="on"이 추가된다는 가정하에 .on 에 초록색 스타일 추가
- 모든 li들이 float되어서 ul이 높이를 잃지 않도록 display:flow-root; 를 넣었지만, 해당 속성을 지원하지 않는 브라우저 환경을 대비해 ul:after에 clear:both; 속성도 함께 부여
```css:avatars.css

.avatars_wrapper{padding:60px 0;border:1px solid #DBDBDB;background-color:#fbfbfb;}
.avatars_list{width:336px;margin:0 auto;display:flow-root;}
.avatars_list:after{content:'';display:block;clear:both;}
.avatars_wrapper li{position:relative;float:left;margin:10px;line-height:0.5;}
.avatars_wrapper li img{width:64px;border-radius:50%;}
.avatars_wrapper li .avatars_state{display:block;position:absolute;bottom:0px;right:0px;width:16px;height:16px;background-color:#DBDBDB;border:1px solid #fff;border-radius:50%;}
.avatars_wrapper li .avatars_state.on{background-color:#4CFE88;}
```
&nbsp;


### _- flex를 지원하는 브라우저 환경을 위한 레이아웃 구성_
- flex를 지원하는 환경을 위한 style은 css 파일의 최하단에서 @supports (display:flex) {} 를 활용
- 아바타 목록인 ul.avatars_list 에 display:flex;flex-flow:row wrap; 값을 부여하고, 목록이 항상 가운데에 위치하도록 justify-content: center; 값을 지정함
- float으로 구현한 아바타 목록에서는 여성 아바타들이 먼저 배치되고 남성 아바타들이 배치되어있지만, flex를 지원하는 환경에서는 남성 아바타들이 먼저 배치되기를 요청받음
- li.avatar 들에게 male, female 이라는 class를 각각 부여하고, male에 order:-1; 값을 지정하여 순서가 먼저 배치되도록 작업

```css:avatars.css

@supports (display: flex){
  .avatars_list{display:flex;flex-flow:row wrap;justify-content: center;}
  .male{order:-1;}
}
```


&nbsp;
<details>
<summary>🙃<span style="background-color:#f1f1f1;">아쉽다</span></summary>
클라이언트(슬비쌤)의 요청사항을 확실하게 물어보았다면 이렇게 다양한 상황을 대비할 필요가 없었을텐데, 다소 아쉬운 부분이 있다. 이런 부분은 반성하자.
</details>



&nbsp;
<details>
<summary>🧐<span style="background-color:#f1f1f1;">접근성, 어렵다</span></summary>
접근성에 대한 고민은 html을 처음 접했을 때부터 많이 했다고 생각했는데, 슬비쌤 수업을 들으면서 그동안 고민만 하고 찾아보는 행위는 하지 않았구나, 라는걸 절실히 느꼈다. 이 과제를 통해 접근성이 조금이라도 더 향상된 코드를 짤 수 있게 되지 않았을까 돌아보게 되었다.
</details>

&nbsp;

<details>
<summary>🤔<span style="background-color:#f1f1f1;">Trailing slash 에 대한 고민</span></summary>
웹표준 검사를 해보았더니 "void 요소의 후행 슬래시는 아무런 효과가 없으며 따옴표가 없는 속성 값과 잘못 상호 작용 합니다." 라고 적혀있어서 안 넣는게 나은가하는 고민을 해보았다. 선생님께서 자유롭게 선택하라고 하셨으니 앞으로는 마음 편한대로 해보아야겠다.
</details>


&nbsp;

<details>
<summary>😅<span style="background-color:#f1f1f1;">마크다운 이렇게 쓰는거 맞나</span></summary>
마크다운은 간단해야하지 않나? 너무 구구절절 적고 있는 것 같은데, 말이 많은 성향이 또 이렇게 드러난다. 선생님 과제검사하시기 힘드시겠다.😅
</details>