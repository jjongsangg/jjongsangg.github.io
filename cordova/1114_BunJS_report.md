># Bun?
- 매우 빠른 Javascript Runtime.
- Bundle, transpile, PackageManager, TypeScript 기본제공

>자칭 "all-in-one js runtime".

### 특징
---
Node API와 90% 호환 되고 Deno와 다르게 node를 그대로 호환시켜 성능향상을 할 수 있었다고 합니다.

#### Butn의 철학
- 빠르게 시작가능
- 새로운 레벨의 성능
- 편리하게 툴 모두 제공

#### 목표
- node or deno와 비슷하지만, 브라우저 외 환경에서 js를 제공하고, 개발자 생산성 극대화 !

### Bun 이 내장하는 것
---
- Web API, fetch, WebSocket, ReadableStream etc.
- Bun.Transpiler
	- TypeScript, Bun 내에서 file이 기본적으로 transpiled 된다고 함.
	- Transpiler를 API형태로도 사용가능 (Bun.Transpiler)
- Bun.Write
	-system call 이 빠르다. 특히 파일 관련 api들(write, copy, pipe, sen, clone ...)
- .env
	- 기본적으로 .env 제공
- bun:sqlite
	- SQLite3 client을 빌트인 으로 들고 있다.
- Node-API - node native module 90%제공(Bun메인 홈피 주장에 따르면 90%)
- bun:ffi(Foreign Function Interface)
- node호환?
	- node:fs, node:path 와 같이 node.js에서 제공되던걸 제공?

### Bun 내부구현은?
---

- webkit(JavascriptCore)을 javascript engine으로 가진다.
	- 당연히 javascript runtime이니 가져야겠지!
	- v8보다 빠르다. - https://twitter.com/jarredsumner/status/1499225725492076544
- Bun은 ZIG언어로 구현되어 있다.
	- 2022-08-15기준으로 ZIG는 0.9.1 버전이다.
	- 참고로 Deno는 Rust(22.08-15기준 - 1.63.0)로 구현되어 있다.
- Bun이 빠른 이유 자체가 ZIG언어의 특징(low level memory관리 및 simple한 control flow)에 있다고 한다.

## Bun 간략한 사용법

### 설치하기(install 스크립트)

```
curl https://bun.sh/install | bash
```
Bun의 HTTP 서버는  Request and Response 객체를 내장하고 있음

```
// http.js
export default {
  port: 3000,
  fetch(request) {
    return new Response("Welcome to Bun!");
  },
};
```
Bun 실행
```
$ bun run http.js
```
브라우저에서 http://localhost:3000 으로 접속해서 확인(”Welcom to Bun!”)가능.

기타 bun create으로 프로젝트 제공하는 부분

Create a new Next.js project:
```
bun create next ./app
```
Create a new React project:
```
bun create react ./app
```
Create from a GitHub repo:
```
bun create ahfarmer/calculator ./app
```
To see a list of examples, run:
```
bun create
```
