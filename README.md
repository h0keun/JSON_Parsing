## JSON - GSON
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

```
JSON으로 받은 응답 데이터는 문자열로 되어 있으므로 그 응답 데이터 중에서 특정 속성의 값을 찾아내려면 문자열 처리를 해주어야 한다.  
어떤 객체 안에 들어있는 속성을 찾아내기 위해 중괄호나 콜론, 콤마 등을 이용해야 하는 의미이다.  
따라서 indexOf나 substring과 같은 메소드들이 사용되고 아주 복잡하고 많은 양의 코드가 만들어지게 된다.  
그런데 자바스크립트에서는 JSON 문자열을 자바스크립트 객체로 만드는 것이 메소드 호출 하나로 끝난다.  
자바스크립트의 객체 포맷과 JSON 기본 구조가 같고 둘 간에 쉽게 변환할 수 있도록 미리 만들어두었기 때문이다.  
자바에서 Gson을 사용하면 한 줄의 코드만으로도 JSON 문자열을 자바 객체로 바꾸어줄 수 있다.  
```
  
### GSON
JSON 데이터는 그대로 JavaScript로 바꿔쓸 수 있기 때문에 Node.js나 웹 브라우저에서 바로 사용이 가능한 장잠이 있다.  
반면 안드로이드의 경우 JavaScript가 아닌 Java를 사용하기 때문에 JSON 문자열이 넘어오면그 문자열 데이터를 자바 객체로 바꿔주는 작업이 필요하다.  
이때 사용하는 여러 라이브러리가 있는데 대표적으로 구글에서 지원하는 GSON 라이브러리를 사용한다.

## GSON 사용
GSON은 JSON 문자열을 객체로 변환해 주는 라이브러리이다. 다시말해 JSON 문자열을 JAVA객체로 만들어준다.  
Volley를 이용해 웹서버로부터 JSON응답을 받으면 GSON을 이용해 자바 객체로 바꾸고, 그 객체안에 들어있는 데이터를 사용하게 된다.  

1. 우선 GSON이 외부라이브러리이기 때문에 Build.gradle에 GSON을 추가
2. JSON 문자열의 속성에 맞는 자바 클래스를 정의  
  (자바스크립트는 객체의 포맷이 객체 안에 속성들이 들어가 있는 구조를 가지고 있지만 자바의 객체는 그런 구조가 아니라서  
  JSON 문자열을 자바 객체로 변환하기 위해서는 먼저 자바 클래스를 정의해야 한다)  
  ```JAVA
  public class MovieList {
    MovieListResult boxOfficeResult;
  }
  ```
  응답 데이터의 가장 바깥이 중괄호이므로 이 객체를 변환할 클래스로 MovieList라는 이름의 클래스를 정의한다.  
  이 클래스 안에는 boxOfficeResult라는 이름의 변수를 추가하고, 여기에서 변수의 이름은 JSON 문자열에서 속성의 이름과 같다.  
  그리고 변수의 자료형은 JSON 문자열에서 속성값의 자료형과 같다. JSON 문자열에서 boxOfficeResult 속성의 값이 다시 객체이므로   
  이 객체를 변환하여 담을 클래스를 MovieListResult라는 이름으로 만들고 boxOfficeResult 속성의 자료형으로 지정한다.
  ```JAVA
  public class MovieListResult {
    String boxofficeType;
    String showRange;
    ArrayList<Movie> dailyBoxOfficeList = new ArrayList<Movie>();
  }
  ```
3. JSON 문자열에서 배열의 표현
  JSON 문자열의 속성 중에서 값이 배열인 경우, 즉 대괄호로 표시된 경우에는 자바 클래스를 정의할 때 ArrayList 자료형을 사용할 수 있다.  
그리고 그 배열 안에 다시 객체들이 들어가는 경우 해당 객체들을 위한 자바 클래스를 또 만들어야 한다. 이 클래스는 ArrayList의 제네릭 타입으로 지정된다.
```JAVA
ArrayList<Movie> dailyBoxOfficeList = new ArrayList<Movie>();
```
여기서 배열안에 들어가는 Movie객체는 다음과 같이 영화 정보를 담을 변수들을 포함하게 된다.  
```JAVA
public class Movie {
    String rnum;
    String rank;
    String rankInten;
    String rankOldAndNew;
    String movieCd;
    String movieNm;
    String openDt;
    String salesAmt;
    String salesShare;
    String salesInten;
    String salesChange;
    String salesAcc;
    String audiCnt;
    String audiInten;
    String audiChange;
    String audiAcc;
    String scrnCnt;
    String showCnt
}
```
4. GSON으로 변환
```JAVA
Gson gson = new Gson();
MovieList movieList = gson.fromJson(response, MovieList.class);
```
