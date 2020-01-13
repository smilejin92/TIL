# GraphQL

`GraphiQL` : GraphQL을 위한 PostMan 같은거라 생각하면됨

일반적인 쿼리: CRUD

GraphQL: READ ONLY

Mutation: CRD



relay vs. apollo

relay - restricted schema/query (fb)

apollo - flexible



### using apollo

`npm i apollo-client apollo-cache-inmemory`

모든 요청이 단일 주소로 정해져있기 때문에 브라우저에서 캐시화를 할 수 없다.

따라서 `apollo-cache-inmemory`와 `apollo-link-http`를 함께 설치한다

`graphql`

`graphql-tag`

`react-apollo`



### Apollo Client vs. Boost

Boost: cli, cacheInMemory, linkHttp, linkError를 포함

`npm i apollo-boost`



### React Hook 기반 프로젝트에서의 Apollo 사용

`npm i @apollo/react-hooks`

아폴로 Organization의 react-hooks를 설치

