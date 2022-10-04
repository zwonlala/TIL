# performance?


내가 개발하고 있는 서비스가 느리다는 사용자들의 피드백과  
나도 개발시 느리다고 느낄 때가 있다...


그런데,

- 느리다(성능이 좋지 않다)의 기준
- 측정 지표
- 어떻게 개선하는가?

에 대해 알아보고 싶어 정리하는 readme.


&nbsp;
&nbsp;

----

&nbsp;
&nbsp;


## 읽어볼 글

- rladpwl0512 님 velog
	- [[우아한테크코스] 모락팀의 성능 최적화, 왜 해야해?](https://velog.io/@rladpwl0512/%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC%EC%BD%94%EC%8A%A4-%EB%AA%A8%EB%9D%BD%ED%8C%80%EC%9D%98-%EC%84%B1%EB%8A%A5-%EB%A6%AC%ED%8F%AC%ED%8A%B8-%EC%84%B1%EB%8A%A5-%EC%B5%9C%EC%A0%81%ED%99%94-%EC%99%9C-%ED%95%B4%EC%95%BC%ED%95%B4)
	- [[우아한테크코스 미션] 성능최적화 1 - 요청 크기 줄이기(소스코드, 이미지 중심)](https://velog.io/@rladpwl0512/%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC%EC%BD%94%EC%8A%A4-%EB%AF%B8%EC%85%98-%EC%84%B1%EB%8A%A5%EC%B5%9C%EC%A0%81%ED%99%94-1-%EC%9A%94%EC%B2%AD-%ED%81%AC%EA%B8%B0-%EC%A4%84%EC%9D%B4%EA%B8%B0%EC%86%8C%EC%8A%A4%EC%BD%94%EB%93%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EC%A4%91%EC%8B%AC)


- 👌[TECH CONCERT: FRONT END 2019 - 오늘부터 나도 FE 성능분석가](https://www.youtube.com/watch?v=cpE1dwJgS4c&ab_channel=naverd2) 

- 👌 [[10분 테코톡] 🍺 서니의 프론트엔드 성능 측정](https://www.youtube.com/watch?v=A6J74xLWqYg&t=634s&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9CTech)


- 👌 [20190129 김명신 youtube "자바스크립트 성능 최적화 기법"](https://www.youtube.com/watch?v=9MZl8Uq9Gmw&ab_channel=%EA%B9%80%EB%AA%85%EC%8B%A0)
	- 뒷 부분에 코드 베이스로 성능 최적화를 비교해주는 섹션이 있어 좋음
	- 다만 ~~2019년도~~(OMG 2019 년도 영상도 아닌 2014년도 영상임;;) 영상이라 현재의 기술 스택인 React.js 가 아닌 jQuery 기반 소스 코드 설명임.... OTL
	- 브라우져도 이전 IE 기반 설명이라 현재와 다른 부분도 있을 수 있음
	- 라이트한 설명 느낌이라 초반에 개략적인 개념잡기 좋은듯


- 👌 [20190214 NHN Cloud youtube "[2018] 프런트엔드 성능 최적화"](https://www.youtube.com/watch?v=G1IWq2blu8c&ab_channel=NHNCloud)
	- 강의 슬라이드 : [https://www.slideshare.net/NHNFORWARD/2018-130108045](https://www.slideshare.net/NHNFORWARD/2018-130108045)

	<details>
	<summary>강의 정리본</summary>


		FE 최적화에는 크게 두가지가 있음
		  1. 로딩 최적화: 리소스를 어떻게 최적화?
		  2. 렌더링 최적화


		1. 로딩 최적화

			1) 브라우져 기준 최적화
				1)) JS 로드시점 최적화
				2)) CSS 최적화
			
			2) 사용자 기준 최적화

				W3C에 "페인트 타이밍 이벤트"
				
				***(중요) "First Meaningful Piant" 시점을 보다 앞당겨야 함. => 사용자 기준 최적화


				Ex) SSR - SPA 로 많이들 개발.
						F.M.P를 앞당기기 위해 쓰는 방식이 SSR
						(브라우져가 HTML을 요청하는 시점에 바로 HTML을 생성해서 응답으로 내려보내고, 브라우져가 의미있는 콘텐르를 로딩.)

				SSR vs 프리렌더러

					- SSR : HTML 요청한 런타임 시점에, HTML & CSS 생성 후, 응답 내려보냄

					- 프리렌더러 : 런타임이 아닌 빌드타임 / webpack을 쓰게되면 HTML webpack 플러그인과 함께 사용
					  (webpack pre-render-loader)

					  	-> DOM Content Loaded 가 살짝 느려지지만,
						   사용자 관점 최적화에서는 의미 없는 것이다. (∵ 사용자에게 의미있는 콘텐츠를 이미 보여주고 있어서)

			3) PWA 사례

		

		2. 렌더링 최적화
			1) 레이아웃 쓰레싱

				fps가 30 정도로 살짝 버벅 거림
				=> "강제 동기 Layout"이 발생하였기 때문

				"강제 동기 Layout" ... Critical Rendering Path ... DOM을 변경하지 않음에도 불구하고 LAYOUT 과정을 강제로 타게 되어 강제 동기 Layout이라고 함

				Ex) 특정 DOM Element의 프로퍼티를 읽기만 해도 이 과정이 발생됨..

				이 "강제 동기 Layout"이 매우 빈번하게 발생한 경우 "레이아웃 쓰레싱" 이라고 한다!

			2) Virtual DOM

			3) 웹 워커

	</details>

- 👌 [[NHN FORWARD 2021] Lighthouse 성능 지표를 사용한, '웹 애플리케이션 성능 측정 자동화 모듈' 개발기](https://www.youtube.com/watch?v=34T0IU18R6c&ab_channel=NHNCloud)
	- 프론트 엔드 최적화를 통해 성능을 향상 시키는 것도 중요하지만, 
		- 향상된 성능을 계속 유지하는 것
		- 성능이 안좋아 질 경우 어느 시점에 안좋아졌는지
		- 성능의 변화(개선 혹은 악화?) 추이를 보는 것
		도 중요한 것 같은데 위 고민에 대한 한 개발자의 개발기를 보는 영상이라 매우 좋았음
		- [강의 자료](https://rlqof7ogm.toastcdn.net/references/2021_session_13.pdf)


- [20210908 Akamai Technologies youtube "웹 프론트 엔드 최적화를 위한 다양한 성능 개선 방법과 CDN의 소개"](https://www.youtube.com/watch?v=9Sq9y4ljmPI&ab_channel=AkamaiTechnologies)


- the RED "김태곤" 
	- 1) 프론트엔드 개발자가 왜 성능을 신경써야하나요?
	- 2) 코드 바깥의 성능
	https://fastcampus.co.kr/courses/202919/clips/ 34:33/50:04
	- 3) 애니메이션 성능
	- 4) JavaScript 코드의 성능


- [[프론트엔드] 초기 로딩 최적화 하기(GZip 이용)](https://www.youtube.com/watch?v=qaLCplPCy3c&ab_channel=HoYongLim) ?? 뭐하는 건지 잘 모르겠네...



- 문서
	- 👌 [Toast UI "성능 최적화"](https://ui.toast.com/fe-guide/ko_PERFORMANCE#%EC%84%B1%EB%8A%A5-%EC%B5%9C%EC%A0%81%ED%99%94)
