# HTML/CSS 과제
form 요소를 활용한 네이버 로그인 레이아웃 작업하기


## _과제내용_
네이버 로그인 페이지를 구현하자
- form 요소를 활용한 로그인 페이지 구현
- 미디어쿼리를 활용한 반응형 구현
- rem 단위 익히기
- form 요소에 마우스 및 키보드로 접근하는 방법 익히기

&nbsp;

## _과제 수행 결과_
[naver.html 페이지 확인 클릭!]

&nbsp;

[naver.html 페이지 확인 클릭!]: <https://hammadam.github.io/homework/naver/naver.html>



\< 과제 수행 과정 \>
## 1. 구조설계
### 1-1. 피그마에서 마크업 설계 짜보기

![initial](https://github.com/hammadam/homework/blob/main/naver/images/html_structure_design01.png?raw=true) 

- 모바일 환경에서는 가로로 꽉차는 구조지만 데스크탑에서는 가운데에 콘텐츠가 배치될 수 있도록 `div.login-wrapper` 로 묶기
- logo는 `h1` 요소 안의 `a>img` 로 구현하기, svg를 지원하지 않는 환경을 대비한 png 이미지도 준비해서 `srcset` 로 제공하기
- `form`을 감싸는 `section` 요소와 제목 `h2` 요소를 만들기
- `form > fieldset > legend + div.login-form-group` 구조로 틀을 짠 다음 내부에 각각 `div.input-group`로 감싼 `label+input[type="email"]` 과 `label+input[type="password"]` 로 구성하기
- 로그인 버튼은 `button[type="submit"].login-botton` 으로 작업
- 로그인 버튼 하단의 로그인상태유지, IP보안 ON/OFF 는 크게 `div.login-state-group` 로 묶고 각각 `div.login-state` 로 묶기
- 로그인상태유지는 체크박스로 처리하되, 왼쪽 체크박스의 디자인을 구현하기 위해 체크박스를 `display:none` 처리하면 키보드로 포커스를 이동했을 때 접근이 불가능하기 때문에 `appearance: none`로 처리하고 체크박스 이미지는 `label` 왼쪽에 배경이미지로 넣어서 처리하기


![initial](https://github.com/hammadam/homework/blob/main/naver/images/html_structure_design02.png?raw=true) 
- 로그인상태유지는 모바일에서는 오른쪽에 배치, 데스크탑에서는 왼쪽에 배치되게 하기
- IP 보안은 `a`태그로 작업하되 새창으로 열리게끔 `[target="_blank"]` 속성 부여
- ON/OFF 스위치는 접근성 측면에서 input 을 활용해야할 것 같은데 어떤 input을 활용해야할지 정리가 안 됨. 우선 `radio` 버튼으로 작업해보기로 함


&nbsp;

### 1-2. HTML <!DOCTYPE> 선언

```
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>네이버 로그인</title>
</head>
<body>
  
</body>
</html>
```
&nbsp;


### 1-3. html 마크업
피그마에서 설계했던 내용을 토대로 마크업 작업을 진행했다.
> ON/OFF 스위치는 처음에 `radio` 버튼으로 마크업 했었는데  
> 키보드(방향키)로는 구현이 되었지만 오히려 마우스 클릭으로는 스위치가 바뀌는게 어려워서  
> 결국 `checkbox`로 다시 마크업함

```
<body>
  <div class="login-wrapper">
    <h1 class="logo">
      <a href="/">
        <picture>
          <source srcset="logo.png 1x, logo@2x.png 2x, logo@3x.png 3x" />
          <img src="logo.svg" alt="NAVER" />
        </picture>
      </a>
    </h1>
    <section class="login-form-wrapper">
      <h2 class="sr-only">로그인</h2>
      <form action="/" class="login-form">
        <fieldset>
          <legend class="sr-only">네이버 로그인 폼</legend>
          <div class="login-form-group">
            <div class="input-group">
              <label for="user-id" class="sr-only">아이디(이메일)</label>
              <input type="email" class="input-form" name="user-id" id="user-id" placeholder="아이디(이메일)" required />
            </div>
            <div class="input-group">
              <label for="user-password" class="sr-only">비밀번호</label>
              <input type="password" class="input-form" name="user-password" id="user-password" placeholder="비밀번호" required />
            </div>
          </div>
          <button type="submit" class="login-button">로그인</button>
          <div class="login-state-group">
            <div class="login-state">
              <input type="checkbox" id="stay-login" />
              <label for="stay-login">로그인 상태유지</label>
            </div>
            <div class="ip-security">
              <a href="ip_security.html" target="_blank">IP 보안</a>
              <input type="checkbox" name="ip-security" id="ip-security-chk" />
              <label for="ip-security-chk">IP 보안</label>
            </div>
          </div>
        </fieldset>
      </form>
    </section>
  </div>
</body>
```
&nbsp;

&nbsp;

## 2. 스타일 지정
- css코드는 `줄바꿈`으로 작성해보기  
: 지난 과제에서 css를 한줄로 선언하는 방식은 코드의 가독성 측면에서 바람직하지 않다는 슬비쌤의 피드백을 받음
- `중첩방식`으로 작성하는 연습해보기

### 2-1. 스타일 지정을 위해 naver.css 파일을 연결
```
<link rel="stylesheet" href="naver.css" />
```
&nbsp;


### 2-2. user agent style 초기화
- 에이전트 스타일 reset
- 숨김텍스트 `sr-only`(스크린온리) style 지정

```
/* reset */
*{
  box-sizing:border-box;
}
*:focus, input:focus{
  outline:0;
}
*:focus-visible, input:focus-visible{
  outline:1px solid #24388d;
  outline-offset:0;
}
a{
  text-decoration:none;
  color:inherit;
}
input, button{
  margin:0;padding:0;
}
fieldset{
  margin:0;
  padding:0;
  border:0;
}

/* sr-only */
.sr-only{
  position:absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  clip: rect(0,0,0,0);
  clip-path: polygon(0 0, 0 0, 0 0);
  overflow: hidden;
  padding: 0;
  white-space: nowrap;
  border-width: 0;
}

```
&nbsp;

### 2-3. 모바일 환경 레이아웃 style 작업
- 모바일 화면(768px 미만)을 먼저 디자인
- 단위는 최대한 rem 단위 활용
- 모바일 환경에서 IP 보안 ON/OFF 스위치는 사용자에게 제공되지 않도록 `.ip-security`를 `display:none` 처리
```
/* 네이버 로그인 */
body{
  margin:0;
  font-size:1rem;
  color:#181818;
}

.login-wrapper{
  padding:6.25rem 1.25rem 0;
}

.logo{
  width:14.375rem;
  inline-size:14.375rem;
  margin:0 auto;

  img{
    width:100%;
    vertical-align:top;
  }
}

.login-form{
  margin-top:3.125rem;
}

.input-form{
  width:100%;
  inline-size:100%;
  height:2.8125rem;
  block-size:2.8125rem;
  font-size:0.875rem;
  line-height:2.8125;
  padding:0.5rem 1rem;
  margin-top:0.625rem;
  background:#fff;
  border:1px solid #dadada;

  &:focus{
    background:#e9f0fd;
    border:1px solid #03cf5d;
  }
}

.login-button{
  width:100%;
  font-size:1rem;
  line-height:2.8125rem;
  color:#fff;
  background:#03cf5d;
  margin-top:1.25rem;
  border:0;
}

.login-state-group{
  margin-top:0.625rem;
  display: flex;
  flex-flow:row nowrap;
  justify-content:right;
  align-items: center;

  .login-state{

    input[type="checkbox"]{
      position:absolute;
      appearance: none;
      width:1.5rem;
      inline-size:1.5rem;
      height:1.5rem;
      block-size:1.5rem;
    }

    label{
      display:block;
      background:url(icons/unchecked.svg) no-repeat 0 0 /contain;
      padding-left:1.8125rem;
      padding-top:0.1875rem;
      line-height:1.3125rem;
    }

    input[type="checkbox"]:checked +label{
      background-image:url(icons/checked.svg);
    }
  }
}

.ip-security{
  display:none;
}
```
&nbsp;


### 2-4. 데스크탑 환경 레이아웃 style 작업
- 데스크탑 환경 화면 디자인
- 데스크탑 로그인 폼의 가로 크기는 500px(좌/우 여백 각 20px 포함)
- ON/OFF 스위치를 표현하기 위해 `input[type="checkbox"]::before` 가상요소를 활용

```
/* 데스크탑 스타일 */
@media (min-width:768px){
  .login-wrapper{
    width:31.25rem;
    inline-size:31.25rem;
    margin:0 auto;
  }
  .login-state-group{
    justify-content: space-between;
  }

  .ip-security{
    display:block;

    > *{
      float:left;
    }
    a{
      padding-top:0.125rem;
      line-height:1.375rem;
    }

    input[type="checkbox"]{
      margin-left:0.5rem;
      appearance: none;
    }
    label{
      text-indent:-9999em;
    }

    input[type="checkbox"]::before{
      content:'OFF';
      display:block;
      font-size: 1rem;
      line-height:1.5rem;
    }

    input[type="checkbox"]:checked::before{
      content:'ON';
      color:#03cf5d;
    }
    input[type="checkbox"]:focus{
      outline:0;
    }
    input[type="checkbox"]:focus-visible::before{
      outline:1px solid #24388d;
    }
  }
}
```


&nbsp;

## heading 구조 확인, Validate_local_html 체크

![initial](https://github.com/hammadam/homework/blob/main/naver/images/html_heading.png?raw=true) 
![initial](https://github.com/hammadam/homework/blob/main/naver/images/Validate_local_html.png?raw=true) 

&nbsp;

# 어려웠던 부분, 성장한 부분

### 🙃 ON/OFF 스위치를 구현하느라 시간을 많이 허비함
> 처음에 라디오 버튼으로 구현했을 때 의외로 키보드로는 쉽게 구현되었지만 마우스로는 제대로 기능을 동작시킬 수 없었다.  
마크업하느라 시간 쓴게 아까워서 마크업은 유지하고 css 수정으로 어떻게든 구현하고 싶었다.  
피곤하니 일단 자고 내일 다시 하자는 마음으로 눕다말고 다시 벌떡 일어나서  
라디오버튼으로 구현한 코드를 과감히 지워버리고 체크박스로 마크업했더니 금방 구현할 수 있었다. 허허허...  
가끔 이렇게 과감하게 지우는 것도 필요한 듯.  
(라디오 버튼으로 작업했던거 완전히 지우지말고 남겨둬서 md 파일에 남길껄 그랬나..?)


&nbsp;
### 🤓 스크린리더 설치해서 직접 들어보고 코드를 수정함
> 크롬 확장프로그램에서 스크린리더를 설치해서 내가 작업한 페이지를 들어보았다.  
생각보다 잘 구현한 것 같은 뿌듯함.. ㅎㅎㅎ  
하지만 ON/OFF 스위치 되는 부분에서 label에 가상요소를 넣어서 작업했더니  
스크린리더로 들어보면 이게 무슨 체크박스인지, 그리고 체크박스가 제대로 눌러진건지 헷갈릴 수도 있겠다 싶었다.  
급히 label에 적용했던 가상요소 before를 checkbox에 직접 부여했더니  
스크린리더가 "IP 보안 체크박스 선택안함", "IP 보안 체크박스 선택됨"라고 제대로 들려줘서 기분이 좋아졌다. ㅎㅎ


&nbsp;
### 😎 분명하다. 어제의 나보다 성장했다
> 예전에도 체크박스의 디자인을 이미지로 대체해서 작업한 적 많이 있었다.  
그때는 그냥 체크박스를 display:none 시켜버리고 디자인적으로만 처리를 했었는데,  
그렇게 하면 키보드로 접근이 어렵다는걸 수업에서 처음 알게 됐다. 충격..  
이번 과제를 통해서 그 부분을 다시한번 복습하게 되어 좋았다.  
이제 현업에 가면 체크박스는 display: none 이 아니라 `appearance: none` 으로 숨길 수 있겠지!  
rem 단위 계산하는 것도 수업을 들으면서  
아 이렇게 쉽게 할 수 있구나~ 이런 계산으로 하면 되는구나 라는걸 알게 되어서 좋다.  
ㅎㅎ 재밌다!