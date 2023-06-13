---
layout: post
title: "[S2-Unit09] StatesAirline Client 회고"
date: 2023-06-13 12:00:00 +900
lastmod: 2023-06-13 12:00:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02, 회고]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/46e84e24-3591-4710-aa65-d0846d8d919c
  width: 1154
  alt: StatesAirline Client 회고
---

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/892956cd-5ba4-4aac-b044-306542a80919" width="80%" />
</center>

데이터 흐름 개념을 활용하여 항공편 검색 기능을 구현하는 과제다. 이 과제의 핵심은 네트워크 요청을 통해 항공편 리스트를 받아오고, 도착지 정보 검색 기능을 구현하는 것이다. 

기능 구현을 위해서 다음과 같은 고민을 한다.
- 상태 갱신 함수를 어디로 전달할지
- Effect hook을 어떻게 활용할 수 있을 지

**Component**

- `Main` : 메인 컴포넌트
- `Search.js` : 검색 도구 컴포넌트
- `getFlight` : 항공편 데이터를 REST API로 호출하는 컴포넌트

## Part 1: 항공권 목록 필터링

> 🦋 **Main 컴포넌트에서 항공편을 조회한다.**
> 
> 1. Main 컴포넌트 내 `search` 함수는 검색 조건을 담고 있는 상태 객체 `condition` 을 업데이트해야 한다.
>
> 🦋 **Search 컴포넌트를 통해 상태 끌어올리기를 학습한다.**
>
> 2. 검색 화면이 Search 컴포넌트로 분리되어야 한다.
> 3. Search 컴포넌트에는 상태 변경 함수 `search` 가 `onSearch` props로 전달되어야 한다.
> 4. 상태 변경 함수 `search` 는 Search 컴포넌트의 `검색` 버튼 클릭 시 실행되어야 한다.

부모인 `Main` 컴포넌트에서 자식 컴포넌트인 `Search` 에 search 함수를 props로 전달하고, `Search` 컴포넌트는 전달받은 search 함수를 사용한다.

`Search` 에서 검색 버튼을 클릭 시 search 함수가 업데이트될 수 있도록 **state 끌어올리기**를 연습하는 부분이다.

### Main Component

```jsx
export default function Main() {
  // 항공편 검색 조건을 담고 있는 상태
  const [condition, setCondition] = useState({
    departure: "ICN",
  });
  const [flightList, setFlightList] = useState(json);

  // 주어진 검색 키워드에 따라 condition 상태를 변경시켜주는 함수
  const search = ({ departure, destination }) => {
    if (
      condition.departure !== departure ||
      condition.destination !== destination
    ) {
      console.log("condition 상태를 변경시킵니다");

      // TODO: search 함수가 전달 받아온 '항공편 검색 조건' 인자를 condition 상태에 적절하게 담아보세요.
      // 1. Main 컴포넌트 내 `search` 함수는 검색 조건을 담고 있는 상태 객체 `condition`을 업데이트해야 한다.
      setCondition({ departure, destination });
    }
  };

  const filterByCondition = (flight) => {
    let pass = true;
    if (condition.departure) {
      pass = pass && flight.departure === condition.departure;
    }
    if (condition.destination) {
      pass = pass && flight.destination === condition.destination;
    }
    return pass;
  };

  global.search = search; // 실행에는 전혀 지장이 없지만, 테스트를 위해 필요한 코드입니다. 이 코드는 지우지 마세요!

  // TODO: 테스트 케이스의 지시에 따라 search 함수를 Search 컴포넌트로 내려주세요.
  return (
    <div>
      <Head>
        <title>States Airline</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <main>
        <h1>여행가고 싶을 땐, States Airline</h1>
        {/* 2. 검색 화면이 Search 컴포넌트로 분리되어야 한다. */}
        <Search onSearch={search} />
        <div className="table">
          <div className="row-header">
            <div className="col">출발</div>
            <div className="col">도착</div>
            <div className="col">출발 시각</div>
            <div className="col">도착 시각</div>
            <div className="col"></div>
          </div>
          <FlightList list={flightList.filter(filterByCondition)} />
        </div>

        <div className="debug-area">
          <Debug condition={condition} />
        </div>
        <img id="logo" alt="logo" src="codestates-logo.png" />
      </main>
    </div>
  );
}
```

### Search Component
```jsx
// 3. Search 컴포넌트에는 상태 변경 함수 `search`가 `onSearch` props로 전달되어야 한다.
function Search({ onSearch }) {
  const [textDestination, setTextDestination] = useState("");

  const handleChange = (e) => {
    setTextDestination(e.target.value.toUpperCase());
  };

  const handleKeyPress = (e) => {
    if (e.type === "keypress" && e.code === "Enter") {
      handleSearchClick();
    }
  };

  const handleSearchClick = () => {
    console.log("검색 버튼을 누르거나, 엔터를 치면 search 함수가 실행됩니다");

    // TODO: 지시에 따라 상위 컴포넌트에서 props를 받아서 실행시켜 보세요.
    // 4. 상태 변경 함수 `search`는 Search 컴포넌트의 `검색` 버튼 클릭 시 실행되어야 한다.
    onSearch({ departure: "ICN", destination: textDestination });
  };

  return (
    <fieldset>
      <legend>공항 코드를 입력하고, 검색하세요</legend>
      <span>출발지</span>
      <input id="input-departure" type="text" disabled value="ICN"></input>
      <span>도착지</span>
      <input
        id="input-destination"
        type="text"
        value={textDestination}
        onChange={handleChange}
        placeholder="CJU, BKK, PUS 중 하나를 입력하세요"
        onKeyPress={handleKeyPress}
      />
      <button id="search-btn" onClick={handleSearchClick}>
        검색
      </button>
    </fieldset>
  );
}

export default Search;
```

<br>

## Part 2: AJAX 요청

> 🦋 **Side Effect는 useEffect에서 다뤄야한다.**
> 
> 1. 검색 조건이 바뀔 때마다, FlightDataApi의 getFlight를 검색 조건과 함께 요청해야 한다.
> 2. getFlight의 결과를 받아, flightList 상태를 업데이트해야 한다.
> 3. 더이상, 컴포넌트 내 필터 함수 `filterByCondition` 를 사용하지 않는다.
> 4. 더이상, 하드코딩된 flightList JSON을 사용하지 않는다. (초기값은 빈 배열로 둔다.)
> 5. getFlight 요청이 다소 느리므로, 로딩 상태에 따라 LoadingIndicator 컴포넌트를 표시해야 한다.
>
> 🦋 **FlightDataApi에서 기존 구현 대신, REST API를 호출하도록 바꾼다.**
>
> 6. 검색 조건과 함께 StatesAirline 서버에서 항공편 정보를 요청(fetch) 한다.

<br>

우선 `getFlight` 컴포넌트에서 REST API를 호출하여 항공편 데이터를 가져온다. 

컴포넌트 내에서 fetch를 사용한다는 것은 Side Effect가 발생한 것이라고 이야기 한다. 그래서 `useEffect()` 를 사용하여, 로딩 화면과 필터링 하는 조건을 수행한다. 참고로 `useEffect(함수, [condition])` 중 배열 안에 있는 condition은 이 condition이 업데이트 될 때만 실행된다.

<br>

### Main Component
```jsx
export default function Main() {
  const [condition, setCondition] = useState({
    departure: "ICN",
  });
  const [flightList, setFlightList] = useState([]);

  // 로딩 컴포넌트를 보여주기 위한 상태 변수 생성
  const [isLoading, setIsLoading] = useState(true);

  const search = ({ departure, destination }) => {
    if (
      condition.departure !== departure ||
      condition.destination !== destination
    ) {
      console.log("condition 상태를 변경시킵니다");

      setCondition({ departure, destination });
    }
  };

  const filterByCondition = (flight) => {
    let pass = true;
    if (condition.departure) {
      pass = pass && flight.departure === condition.departure;
    }
    if (condition.destination) {
      pass = pass && flight.destination === condition.destination;
    }
    return pass;
  };

  global.search = search; // 실행에는 전혀 지장이 없지만, 테스트를 위해 필요한 코드입니다. 이 코드는 지우지 마세요!

  // TODO: Effeck Hook을 이용해 AJAX 요청을 보내보세요.
  // TODO: 더불어, 네트워크 요청이 진행됨을 보여주는 로딩 컴포넌트(<LoadingIndicator/>)를 제공해보세요.

  // 1. 검색 조건이 바뀔 때마다, FlightDataApi의 getFlight를 검색 조건과 함께 요청해야 한다.
  // 2. getFlight의 결과를 받아, flightList 상태를 업데이트해야한다.
  useEffect(() => {
    setIsLoading(true);
    getFlight(condition).then((filterData) => {
      setFlightList(filterData);
      setIsLoading(false);
    });
  }, [condition]);

  return (
    <div>
      <Head>
        <title>States Airline</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <main>
        <h1>여행가고 싶을 땐, States Airline</h1>
        <Search onSearch={search} />
        <div className="table">
          <div className="row-header">
            <div className="col">출발</div>
            <div className="col">도착</div>
            <div className="col">출발 시각</div>
            <div className="col">도착 시각</div>
            <div className="col"></div>
          </div>
          {/* 
              더이상, 컴포넌트 내 필터 함수 `filterByCondition`를 사용하지 않는다. (밑에 부분 수정)
              { <FlightList list={flightList.filter(filterByCondition)} />}
          
              5. getFlight 요청이 다소 느리므로, 로딩 상태에 따라 LoadingIndicator 컴포넌트를 표시해야 한다.
          */}
          {isLoading ? <LoadingIndicator /> : <FlightList list={flightList} />}
        </div>

        <div className="debug-area">
          <Debug condition={condition} />
        </div>
        <img id="logo" alt="logo" src="codestates-logo.png" />
      </main>
    </div>
  );
}
```

### getFlight Component
```jsx
export function getFlight(filterBy = {}) {
  // HINT: 가장 마지막 테스트를 통과하기 위해, fetch를 이용합니다. 아래 구현은 완전히 삭제되어도 상관없습니다.
  // TODO: 아래 구현을 REST API 호출로 대체하세요.

  // 6. 검색 조건과 함께 StatesAirline 서버에서 항공편 정보를 요청(fetch) 한다.
  let query = "";
  if (filterBy.departure) {
    query += `departure=${filterBy.departure}&`;
  }
  if (filterBy.destination) {
    query += `&destination=${filterBy.destination}`;
  }

  let endPoint = `http://ec2-13-124-90-231.ap-northeast-2.compute.amazonaws.com:81/flight?${query}`;

  return fetch(endPoint).then((res) => res.json());
}
```

<br>

## Feelings ...

다른 사람들은 잘 모르겠지만.. 나는 개념을 이해하는 부분에서 계속해서 몇 번이고 읽어서 겨우 이해했다. 오히려 Part 1은 어떤 식으로 문제를 접근해야되지? 라는 생각이 들어서 조금 오래걸렸고, Part 2는 비교적 손쉽게 문제를 풀어나갔다. 하지만 여기서 더 어려운 심화 문제가 나오면 내가 할 수 있을까? 라는 생각이 들어서 React 공부는 더 해야될 것 같다..!!!!!

> _그리고 ... 제일 중요한 건.... 구조분해할당 공부가 필요할 것 같다.... 
(문법 이해 불가능.....)_


## Findings ...

Part 2의 제목은 AJAX 요청이고, 부제목은 REST API를 호출한다고 되어있었다. 

그러다 Rest API와 RESTful API의 개념이 머릿속에 섞이게 되었고, 우리가 구현한 AJAX는 Restful API이 될 수있을까? 라는 궁금증이 생겼고 찾아보게 되었다.

결론부터 말하자면 **우리는 CRUD와 HTTP 메소드를 사용했기 때문에 AJAX는 Rest API와 Restful API이라고 할 수 있다.** Rest 성숙도 모델에서 2단계까지만 적용해도 좋은 API 디자인이라고 말하기 때문에 같다고 말할 수 있다.

> **Rest API와 RestFul API의 차이** <br>
> `Rest API` : REST의 특징을 기반으로 서비스 API를 구현한 것 <br>
> `Restful API` : REST의 설계 규칙을 잘 지켜서 설계된 API

즉, REST의 원리를 잘 따르는 시스템을 RESTful이란 용어로 지칭된다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
