# HTML/CSS 과제
grid를 활용한 APPLE 홈페이지 레이아웃 작업하기


## _과제내용_
apple 제품 카드
- 그리드를 사용하여 구현하고 구현 결과를 움직이는 이미지로 생성하여 삽입해주세요.
- 중단점(breakpoint)은 `1024px` 로 지정한다.  
(Small Screen - 1024px 이하 / Large Screen - 1024px 이상)
- `theme.css` 파일에 제공 된 값(색상, 텍스트 크기, 여백 등)을 사용한다.

&nbsp;

## _과제 수행 결과_
[apple.html 페이지 확인 클릭!]

&nbsp;

[apple.html 페이지 확인 클릭!]: <https://hammadam.github.io/homework/apple/apple.html>



\< 과제 수행 과정 \>
## 1. 구조설계
### 1-1. 피그마에서 마크업 설계 짜보기

![initial](https://github.com/hammadam/homework/blob/main/apple/images/html_structure_design01.png?raw=true) 

- 페이지에서 카드 영역을 묶는 `section`을 최상위에 두고
- `div.cards` 로 각 카드 한장한장을 감싸기. 컴포넌트 관점에서 작업하기!!!!
- 텍스트와 버튼 영역을 굳이 묶을 필요가 있을까 싶었지만 `div.cards-text-box` 로 묶기로 했다.
- 큰제목, 부제목는 각각 `h2.card-title` `p.card-subtitle` 로 마크업 하기로.
- 출시일 추후 공개는 클래스명을 뭐라고 해야할지 한참 고민했는데 `p.card-info` 로 하기로 함.
- 버튼 영역은 하나로 묶어서 `div.button-area` 로 묶고
- 버튼을 클릭하면 다른 페이지로 넘어가는 역할이라서 `a 태그`로 작업
- 카드의 배경이미지를 적용하기 위해 각 카드마다 클래스명 다르게 부여하기로 함.

&nbsp;

### 1-2. HTML <!DOCTYPE> 선언

```
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Apple</title>
</head>
<body>
  
</body>
</html>
```
&nbsp;


### 1-3. html 마크업
피그마에서 설계했던 내용을 토대로 마크업 작업을 진행했다.
- `div.cards` 를 샘플로 하나 먼저 만들고 복제하는 방식으로 진행.
- 콘텐츠가 바뀌는 부분은 큰제목 내용, 부제목 내용, 출시일 추후 공개 유무 여부
- 이미지는 css에서 배경으로 처리

```
<div class="cards cards-ipad-pro">
  <div class="cards-text-box">
    <h2 class="card-title">큰제목</h2>
    <p class="card-subtitle">
      부제목
    </p>
    <p class="card-info">출시일 추후 공개</p>
    <div class="button-area">
      <a href="/" class="button button-more">더 알아보기</a>
      <a href="/" class="button button-price">가격보기</a>
    </div>
  </div>
</div>
```
&nbsp;

&nbsp;

## 2. 스타일 지정
![initial](https://github.com/hammadam/homework/blob/main/apple/images/html_structure_design02.png?raw=true) 
- css 작업순서는 "모바일 퍼스트!"
- card 내부 레이아웃도 grid로 할까 싶었는데 flex로 작업하는게 더 간단할 것 같아서 `flex` 로 배치하기로 함
- card를 나열하는 방법은 `grid` 속성을 활용!
- **grid guide**
  - 모바일 환경에서는 grid 컬럼을 1개로
  - 데스크탑 환경에서는 2개로 나눠서 작업하기로 설계함.
  - (하지만 css 마지막에 그냥 처음부터 2개의 컬럼으로 나눠서 작업하기로 수정함. 마크업도 수정함. 자세한 내용은 아래에서...)
- **텍스트 및 버튼 컬러적용 고민**
  - 흰글자와 까만색 글자 등 번갈아가면서 컬러가 바뀌는 것을 `nth-child` 를 활용해서 홀수와 짝수로 구분해서 컬러를 나누려고 했는데, 나중에 상단에 카드가 하나 더 추가되는 상황에는 맞지 않을 것 같음.
  - 컬러가 바뀌는 분기가 배경이 어두운 배경인지, 밝은 배경인지에 따라 바뀌는 것 같아서 `div.cards` 에 어두운 배경이면 `cards-dark` 밝은 배경이면 `cards-light` 라는 클래스를 부여하기로 해서 마크업을 수정함.


### 2-1. 스타일 지정을 위해 apple.css 파일을 연결
```
<link rel="stylesheet" href="apple.css" />
```
&nbsp;


### 2-2. reset, base, theme.css 연결

```
@import url(reset.css);
@import url(base.css);
@import url(theme.css);
```
&nbsp;

### 2-3. 모바일 환경에서 카드 레이아웃 style 작업
- 반복되는 카드의 기본 레이아웃을 먼저 작업.
- 슬비쌤께서 `theme.css` 에서 변수에 넣어주신 값으로 작업
```
/* 카드 컴포넌트 */
/* 카드 기본 레이아웃 */
/* Small Screen */
.cards{
  text-align:center;
  background-color:var(--black);
  background-position:50% 50%;
  background-repeat:no-repeat;
  background-size:cover;
}

.cards-text-box{
  height:var(--size);
  block-size:var(--size);
  padding-top:var(--large-spacing);
  display:flex;
  flex-flow:column nowrap;

  .card-title{
    padding-bottom:var(--small-spacing);
    font-size:var(--large-text);
    font-weight:bold;
  }
  .card-subtitle{
    padding-bottom:var(--x-small-spacing);
    font-size:var(--base-text);
    line-height:var(--line-normal);
  }
  .card-info{
    padding-bottom:var(--small-spacing);
    font-size:var(--small-text);
    color:var(--gray);
  }
}
```
&nbsp;

- 버튼 기본 디자인 작성
```
/* 버튼 기본 디자인 */
.button-area{
  display:flex;
  flex-flow:row nowrap;
  justify-content: center;
  gap:var(--base-spacing);
  
  .button{
    display:inline-block;
    font-size:var(--xx-small-text);
    padding:var(--x-small-spacing) var(--base-spacing);
    border:1px solid transparent;
    border-radius:50px;
    transition:background 0.2s;
  }
}
```
&nbsp;


### 2-4. 데스크탑 환경에서의 폰트사이즈, 여백 등 작업
```
/* Large Screen */
@media (min-width:1024px){
  .cards-text-box{
    padding-top:var(--extra-large-spacing);
  
    .card-title{
      font-size:var(--extra-large-text);
    }
    .card-subtitle{
      font-size:var(--medium-text);
    }
  }
  .button-area{

    .button{
      font-size:var(--x-small-text);
    }
  }
}
```
&nbsp;


### 2-5. 콘텐츠 컬러 분기 작업
- 카드 배경이 어두울 때와 밝을 때를 구분해서 각각 style 지정

```
/* 어두운 카드 */
.cards-dark{

  .cards-text-box{
    color:var(--white);
  }

  .button-more{
    color:var(--white);
    background-color:var(--blue-400);
    
    &:hover{
      background-color:var(--blue-200);
    }
  }
  .button-price{
    color:var(--blue-100);
    border-color:var(--blue-100);
    
    &:hover{
      color:var(--white);
      background-color:var(--blue-200);
      border-color:var(--blue-200);
    }
  }
}

/* 밝은 카드 */
.cards-light{
  
  .cards-text-box{
    color:var(--black);
  }

  .button-more{
    color:var(--white);
    background-color:var(--black);

    &:hover{
      background-color:#282828;
    }
  }
  .button-price{
    color:var(--black);
    border-color:var(--black);

    &:hover{
      color:var(--white);
      background-color:var(--black);
    }
  }
}
```

&nbsp;

### 2-6. 각 카드의 배경이미지 지정
- 해상도에 따라서 다른 배율의 배경이미지 지정
```
/* 각 카드 배경 */
.cards-ipad-pro{
  background-image:image-set(
    url(../products/ipad_pro.jpeg) 1x, 
    url(../products/ipad_pro_2x.jpeg) 2x);
}
.
.
.
.cards-airpods-pro{
  background-image:image-set(
    url(../products/airpods_pro.jpeg) 1x, 
    url(../products/airpods_pro_2x.jpeg) 2x);
}
```
&nbsp;

- 디바이스 크기에 따라서 다른 비율의 배경이미지 지정
```
@media (min-width:1024px){
  .cards-ipad-pro{
    background-image:image-set(
      url(../products/ipad_pro_wide.jpeg) 1x, 
      url(../products/ipad_pro_wide_2x.jpeg) 2x);
  }
  .cards-ipad-air{
    background-image:image-set(
      url(../products/ipad_air_wide.jpeg) 1x, 
      url(../products/ipad_air_wide_2x.jpeg) 2x);
  }
  .cards-iphone-15-pro{
    background-image:image-set(
      url(../products/iphone15_pro_wide.jpeg) 1x, 
      url(../products/iphone15_pro_wide_2x.jpeg) 2x);
  }
}
```
&nbsp;


### 2-7. grid guide
- 카드 컴포넌트 배치를 위해 `div.cards-wrapper` 에 `grid` 속성 선언
- 모바일 환경에서는 모든 카드가 1칸씩(가로100%)을 차지하다가
- 데스크탑 환경에서는 column이 2개로 나뉘고
- `cols-1` 클래스를 가진 카드는 1칸(가로50%)를 차지하고
- `cols-2` 클래스를 가진 카드는 2칸(가로100%)를 차지하는 방법으로
- 아래와 같이 스타일 지정함
- 위 내용에 맞게 마크업에도 클래스 부여함.
```
/* grid guide */
.cards-wrapper{
  display:grid;
  grid-template-columns: 1fr;
  gap:var(--small-spacing);

  @media (min-width:1024px){
    &{
      grid-template-columns: repeat(2,1fr);
    }
    .cols-1{
      grid-column: span 1;
    }
    .cols-2{
      grid-column: span 2;
    }
  }
}
```
&nbsp;

- 과제 제출 직전에 아래 내용으로 grid guide를 재선언
- 모바일 환경에서부터 column은 2개로 나눠진 상태에서
- `.sm-cols-1` 은 1칸(50%)를 차지, `.sm-cols-2` 는 2칸(100%)를 차지
- 데스크탑 환경이 되면 여전히 column은 2개로 유지
- `.lg-cols-1` 은 1칸(50%)를 차지, `.lg-cols-2` 는 2칸(100%)를 차지
- 이에 맞춰서 마크업도 수정함
```
/* grid guide */
.cards-wrapper{
  display:grid;
  grid-template-columns: repeat(2,1fr);
  gap:var(--small-spacing);
}

.sm-cols-1{
  grid-column: span 1;
}
.sm-cols-2{
  grid-column: span 2;
}

@media (min-width:1024px){
  .lg-cols-1{
    grid-column: span 1;
  }
  .lg-cols-2{
    grid-column: span 2;
  }
}
```

&nbsp;

# 어려웠던 부분, 성장한 부분

### 🙃 grid guide 작업을 두번함
> 처음 설계대로 그리드 가이드를 작업했을 때도 문제없이 구현되었지만, 부트스트랩에서 사용하는 방식대로 가이드를 작성하는게 다른 사람들이 이해하기에도, 유지보수하기에도 용이할 것 같아서 과제 제출 직전에 수정했다. 처음부터 이렇게 생각했으면 더 빨리 끝났을 것을.. 역시 기획, 설계가 제일 중요함.  
지금에 와서 컬럼을 12개로 나누는게 나았을까 싶기도 하지만, 그렇게되면 기획자의 멱살을 잡는 방법도 고려해봐야겠다. 아, 이 과제에선 기획자가 나였지??? 😂 


&nbsp;
### 😙 변수 연습!
> 지난번 과제에서 변수를 사용하지 않은 것이 아쉽다는 피드백을 받았었는데 이번에는 슬비쌤이 넣어주신 theme.css 를 활용하면서 변수 대잔치가 펼쳐짐 ㅎㅎㅎㅎ 나도 이제 변수를 잘 활용하는 프론트엔드 개발자가 되었ㄷ...되...되겠지!!  
> 어떤 값을 변수에 넣는게 더 효율적일지를 고민해보는 것도 많이 해봐야 늘 것 같다.