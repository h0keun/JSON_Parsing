## JSON
웹서버로부터 응답을 받았을 때 응답 데이터의 포맷이 JSON이라는 포맷으로 되어 있는 경우가 많다.  
JSON은 자바스크립트 객체 포맷의 데이터를 주고받을 때 사용할 수 있도록 만든 것이다.  
따라서 자바스크립트 객체 포맷과 거의 동일하다.  
약간의 차이가 있다면 문자열 형식으로 표현하면서 속성의 이름과 문자열에 큰따옴표를 사용한다는 점이 다르다.

자바스크립트 객체는 중괄호({, })를 이용해 만들 수 있다. JSON 포맷에서도 동일하다.  
그리고 객체 안에는 여러 개의 속성이 들어갈 수 있다. 속성은 속성 이름과 속성 값이 콜론(:)으로 구분된다.  
즉, 콜론 뒤에 값이 들어갈 수 있는데 문자열이나 숫자와 같은 기본 자료형의 값이 올 수도 있고 객체가 올 수도 있다.  
만약 객체가 온다면 콜론 뒤에 다시 중괄호가 오게 된다.  
만약 여러 개의 객체가 들어있는 배열을 넣어두고 싶다면 대괄호([, ])를 사용한다.  
대괄호 안에 중괄호로 감싼 객체들이 콤마로 구분되어 들어가게 된다.

### JSON 요청하기  
  본예제에서는 영화진흥위원회에서 제공하는 Open API를 사용하며 주소는 다음과 같다. [주소](http://kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=f5eef3421c602c6cb7ea224104795888&targetDt=20120101)  
  실제 이 웹서버에 요청하려면 개발자 등록을 하고 키 값을 할당 받아야 하지만 이 샘플 주소는 그런과정 없이  
  응답 데이터를 확인해볼 수 있다.
  
```JAVASCRIPT
{
  "boxOfficeResult": {
    "boxofficeType": "일별 박스오피스",
    "showRange": "20120101~20120101",
    "dailyBoxOfficeList": [
      {
        "rnum": "1",
        "rank": "1",
        "rankInten": "0",
        "rankOldAndNew": "OLD",
        "movieCd": "20112207",
        "movieNm": "미션임파서블:고스트프로토콜",
        "openDt": "2011-12-15",
        "salesAmt": "2776060500",
        "salesShare": "36.3",
        "salesInten": "-415699000",
        "salesChange": "-13",
        "salesAcc": "40541108500",
        "audiCnt": "353274",
        "audiInten": "-60106",
        "audiChange": "-14.5",
        "audiAcc": "5328435",
        "scrnCnt": "697",
        "showCnt": "3223"
      },
      {
        "rnum": "2",
        "rank": "2",
        
             ...
        
```
  
### JSON 응답  
  응답 데이터는 JSON 포맷의 문자열 형식으로 받게 된다.  
  응답 데이터는 한 줄로 표시되지만 크롬 브라우저에서 JSONView와 같은 확장프로그램(Extension)을 설치하면 
  깔끔하게 정리된 모양으로 볼 수 있다.  
  응답 데이터는 하나의 객체로 되어 있으며 그 객체 안에 boxOfficeResult라는 속성이 들어가 있다.  
  이 속성의 값은 다시 객체여서 중괄호가 다시 시작된다.  
  그 안에는 boxOfficeType과 showRange 그리고 dailyBoxOfficeList라는 이름의 속성이 들어가 있다.  
  그 중에 dailyBoxOfficeList 속성의 값은 배열이라 대괄호로 된 값이 들어가 있다.  
  그 배열 안에 들어가 있는 각각의 객체가 하나의 영화 정보입니다.
