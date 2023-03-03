---
title: CSS 강좌(2) - CSS AnimationCSS
author: JHStudy
date: 2023-03-02 16:14:00 +0800
categories: [JHStudy, CSS]
tags: [CSS]
---


이글은 CSS 애니매이션 이다


## 사용하기
#### `animation` 단일 속성(등등)
- <a href="" style="color:gray;">animation-name</a> : 애니메이션의 중간 상태를 지정하기 위한 이름을 정의합니다. 중간 상태는 <code class="language-plaintext highlighter-rouge" style="color:red;">@keyframes</code> 규칙을 이용하여 기술합니다.
- <a href="" style="color:gray;">animation-duration</a> : 한 싸이클의 애니메이션이 얼마에 걸쳐 일어날지 지정합니다.
- <a href="" style="color:gray;">animation-delay </a> :엘리먼트가 로드되고 나서 언제 애니메이션이 시작될지 지정합니다.
- <a href="" style="color:gray;">animation-direction </a> : 애니메이션이 종료되고 다시 처음부터 시작할지 역방향으로 진행할지 지정합니다.
- <a href="" style="color:gray;">animation-iteration-count</a> : 애니메이션이 몇 번 반복될지 지정합니다. 
    <code class="language-plaintext highlighter-rouge" style="color:red;">infinite</code> 로 지정하여 무한히 반복할 수 있습니다.
- <a href="" style="color:gray;">animation-play-state</a> : 애니메이션을 멈추거나 다시 시작할 수 있습니다.
- <a href="" style="color:gray;">animation-timing-function</a> : 중간 상태들의 전환을 어떤 시간간격으로 진행할지 지정합니다.
- <a href="" style="color:gray;">animation-fill-mode</a> : 애니메이션이 시작되기 전이나 끝나고 난 후 어떤 값이 적용될지 지정합니다.


{% highlight ruby %}
    /* 단일 속성 */
    .object {
        animation-name: 1s;
        animation-duration: 2s;
        animation-delay: 1s;
        animation-direction: alternate;
        animation-iteration-count: 3;
        animation-play-state: paused;
        animation-timing-function: 1s;
        animation-fill-mode: both;
    }
    /* 속기형 */
    animation: name | duration | timing-function | delay | iteration-count | direction | fill-mode | play-state> [,...];
{% endhighlight %}
#### 키프레임 활용한 애니메이션(마우스 휠 만들기)

{% highlight ruby %}
    /* 마우스 휠 움직임 */
    .scroll span.wheel-down {
        animation: cursor-down 1.15s;
        /* 반복여부 => infinite : 무한, initial: 초기화*/
        animation-iteration-count : 1;
        /* 효과의 시간당 속도를 설정 => linear : 일정한 속도로 진행,  */
        animation-timing-function : linear;
        transform: translateY(1rem);
    }
    .scroll span.wheel-up {
        animation: cursor-up 1.15s;
        animation-iteration-count : 1;
        animation-timing-function : linear;
        transform: translateY(-1rem);
    }

    @keyframes cursor-up {
        0% {
            opacity: 0;
            transform: translateY(1rem);
        }

        100% {
            opacity: 1;
            transform: translateY(-1rem);
        }
    }
    @keyframes cursor-down {
        0% {
            opacity: 0;
            transform: translateY(-1rem);
        }

        100% {
            opacity: 1;
            transform: translateY(1rem);
        }
    }
{% endhighlight %}

## 태그 생성 및 수정

{% highlight ruby %}
    keyframe01 : (value100 , color_name) => {
        var config = `@keyframes stack1{
            0% { width: 0; color:${color_name};}
            40% {color:rgba(255,255,255,1);}
            to {width: ${value100}%; }
            `
        return config;
    }
{% endhighlight %}

## 텍스트 애니메이션 적용
#### transition속성 정리
- transition : 선택자가 변화되는 것을 시간의 흐름을 줘서 변화시키는 속성 
    - 아래 속성들을 한번에 처리하는 속기법
- transition-delay : 변화되는 시간을 지연시키는 속성
    - transition-delay: 1s; => 1초지연
- transition-duration : 변화되는 시간을 작성하는 속성
    - transition-duration: 1s; => 초단위
- transtion-property : 변화되는 CSS를 구분하여 따로 처리
- transition-timing-function : 변화되는 시간에 ease(가속감속)처리

#### 텍스트 뒤늦게(설정한시간 지나고 또는 동안) 나오게하기
{% highlight ruby %}
    a {
        animation-name: mainMenuAtag; // 적용할 애니메니션 키프레임 이름
        animation-duration: 4s;  // 얼마동안 지속될거냐(없으면 실행X)
        /* animation-delay : 2s; */ // 얼마나 지연되고 실행될꺼냐
    } 
    @keyframes mainMenuAtag {
        0%   {opacity : 0} // opacity  텍스트 나타내기 0(없음)
        100% {opacity : 1} // opacity  텍스트 나타내기 1(있음)
    }

    JS의 Jquery 에서 실행
    $(this).children("a").css({
        'animation-name': 'mainMenuAtag',
        'animation-duration': '3s',
        // 'animation-delay' : '2s'
    });
{% endhighlight %}

#### 텍스트 아래에서 위로 올라오면서 보여주기
{% highlight ruby %}
    .main section .section-title p {
        overflow: hidden;
        height: 70px;
        /* animation: 2s anim-lineUp ease-out infinite;
        animation-iteration-count: 1; */
    }

    @keyframes anim-lineUp {
        0% {
            opacity: 0;
            transform: translateY(80%);
        }
        20% {
            opacity: 0;
        }
        50% {
            opacity: 1;JS에서 Jquery로 실행
            transform: translateY(0%);
        }
        100% {
            opacity: 1;
            transform: translateY(0%);
        }
    }


    JS에서 Jquery로 실행
    let subText = "그린훼스코(주)는 ESG 경영에 Premium을 더하는 친환경 기업입니다.";
    let subTitle = $(".section-title p");
    subTitle.append(subText)
    subTitle.css({
        'animation': '2s anim-lineUp ease-out infinite',
        'animation-iteration-count': 1,
    });
{% endhighlight %}
#### 텍스트 오른쪽으로 지정한 단어마다 생성하면서 보여주기
{% highlight ruby %}
    .main section .section-title.on h1 b {
        opacity: 1;
        -webkit-transform: translateX(0);
        transform: translateX(0);
    }

    .main section .section-title h1 b {
        display: inline-block;
        opacity: 0;
        -webkit-transform: translateX(-200px);
        transform: translateX(-200px);
        -webkit-transition: all 2s; /*글자 보여지는 속도*/
        transition: all 2s;
    }



    JS에서 Jquery로 실행
    setTimeout(function () { // 시작하면 클래스 on 추가
        $(".section-title").addClass("on");
    });

    let mainText = ["Green, New Deal, Of, GreenFesco"];

    textDelay(mainText);

    function textDelay(wordArray) {
        wordArray.forEach((word, index) => {

            let Title = $(".section-title h1");
            textSplit(word).forEach((text, index) => {
                Title.append("<b>&nbsp;&nbsp;" + text + "</b>")
                Title.find("b").eq(index).css({
                    "transitionDelay": (0.7 * index) + "s"
                })
            })
        });
    }
    function textSplit(word) {
        var textAddr = word.split("");
        return textAddr;
    }
{% endhighlight %}
## 가로게이지바
#### 심플하게 만들기
{% highlight ruby %}

{% endhighlight %}

#### 참고한 코드
{% highlight ruby %}

{% endhighlight %}