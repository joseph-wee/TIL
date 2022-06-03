# 7주차 React 라이브러리 Ch07.07 ~ Ch08.10

## GraphQL 심화
- Apollo GraphQL: 프론트와 서버를 모두 제공하는 라이브러리
- GraphQL서버: apollo-server graphql
- 스키마: 프론트와 쉐어할 데이터 구조
- 데이터 소스: REST API(기본 캐싱 O), DB (캐싱X)
- 리졸버: 쿼리요청에 대한 응답 생성
- 페이지네이션: 서버 부하를 줄임
- 뮤테이션 리졸버: 로그인, 예약
- SQLite: 데이터 축적됨
- 프론트엔드 연결: ApolloClient
- sueQuery: data, loading, error
- 페이지네이션, 캐시: fetchMore, InMomryCache
- useMutation, makeVar: 뮤테이션, client 로컬 상태 관리

## Next.js 소개
- Next.js: React Framework
- Vercel: Frontend Deploy platform
- SSR, CSR: 보이질 화면을 그리는 주체
- SSR 장점: SEO, 렌더속도, 기타

## 환경 설정 및 프로젝트 생성
- CSR vs SSR: Next.js로 둘다 가능
- 쇼케이스: Next.js실제 사용 예
- SSG vs SSR: getStaticProps vs getSErverSideProps
- 예시: github

## Next.js 기본
- Next.js: 다양한 기능을 추상화해서 제공
- Navigate, prefetching: <a> with <link> / code spliting
- Image , Head: "next,image" , "next,head" - meta
- built in styling, global: CSS modules, sass, styled-jsx
- hydration: js 실행으로 interactive 할 준비 과정
- SSG: Build time에 서버에서만 동작
- SSR: Request time에 동작,  TTFB slow
- CSR: Request time 이후 동작 SWR
- Dynamic Routes: getStaticPaths
- 키 값: 동적으로 만들어서 대응
- fallback: false 면 404, true면 router.isFallback
- API Routes: /pages/api/hello.js

## Next.js 심화
- Pages: Pre-rendring, Dynamic routes
- getStaticProps: revalidate(ISR), redirect, notFound
- getStaticPaths: [fallback: 'bloking']
- getServerSideProps: req.cookies
- Layouts: Page.getLayout
- Optimization: Image, Font, Script
- Static fiel, Fast Refresh: public, 똑똑하게 reload 판단
- 기타: ESLint, Typescriot, 환경 변수
- Next.js의 라우팅: pages 폴더의 file system 활용
- Dynamic Routes: [ slug ] / [ ...slug ] / [[ ...slug ]]
- Router: 직접 라우터를 조작 가능 push / shallow
- API Routes: API 서버로의 동작 middlewares

