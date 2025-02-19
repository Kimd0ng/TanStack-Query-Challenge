# 🌴 TanStack-Query-Challenge 🌴
TanStack-Query-Challenge 를 통해, React 내 custom hook과 Tanstack-Query의 주요 로직을 파악합니다. 최대한 공식문서만을 참고하여, `생성형 AI의 도움 없이` 직접 코드를 작성합니다. `도망친 곳에 낙원은 없습니다.😄`


## 주요 목표

1. `useQuery` 의 주요 기능 제작

- [ ] fetching 과 동시에 queryKey 등록 & 캐시 시간 등록
- [ ] 공통 로딩 상태 관리 isLoading (isPending 과 굳이 구분하지 않아도 됩니다 😄)
- [ ] 공통 에러 상태 관리 Error

2. `useMutation` 의 주요 기능 제작

- [ ] onSuccess / onError 기능
- [ ] invalidateQueries 함수 활용

3. `Context API`를 통해서 전역적으로 쓸 수 있게 만들어주는 `useQueryClient` 제작 (많이 어려우면 2번까지만!!)

## 제공 코드

- 쿼리 캐시 저장소 역할을 해주는 QueryCache 이용
- invalidQueries 제공

```javascript
// 쿼리 캐시 저장소 역할을 해주는 QueryCache 이용
class QueryCache {
  constructor() {
    this.queries = new Map();
    this.mutations = new Map();
  }

  // 쿼리 캐시 저장소에 쿼리 추가
  addQuery(key, query) {
    this.queries.set(key, query);
  }

  // 쿼리 캐시 저장소에서 쿼리 가져오기
  getQuery(key) {
    return this.queries.get(key);
  }

  // 캐시 무효화 로직
  invalidateQueries(keyPattern) {
    Array.from(this.queries.keys()).forEach((key) => {
      if (key.match(keyPattern)) {
        this.queries.get(key).invalidate();
      }
    });
  }
}

/* 근데 이걸 어떻게 쓰냐.. class 는 첨 보는데 싶죠? 아래처럼 쓰면 됩니다! React는 원래 Class 기반이었다는 거 알고 있나요? 😄 */
QueryCache().addQuery("queryKey", query);
QueryCache().getQuery("queryKey");
QueryCache().invalidateQueries("queryKey");
```

##
