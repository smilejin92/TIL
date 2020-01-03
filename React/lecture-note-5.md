유튜브 로그인

/signin 이메일, password, 로그인 버튼

/signup 회원가입 폼 (이메일, 패스워드), 가입 버튼

/user 빈 페이지

/ 빈페이지



로컬 스토리지 vs. 쿠키

쿠키는 서버에 데이터를 전송하기 위해 필요 (사용자 동의 필수)



세션

암호화돼있는 인증 정보 (유효 기간)



로그인 요청 성공시 (why use post? - get 사용시 url에 정보가 노출됨)

1. 서버가 토큰을 보내주고, 프론트엔드에서 쿠키를 만듦
   * JSON WEB TOKEN (JWT) : 클라이언트의 데이터를 신뢰할 수 없기 때문에 사용
   * [js-cookie](https://github.com/js-cookie/js-cookie) 라이브러리: 하위 호환, 크로스브라우징이 되는 쿠키 생성 라이브러리
2. 서버가 토큰과 쿠키를 만듦



http vs. https

http 사용시 post를 써도 페이로드를 도청할 수 있음.

https는 페이로드까지 암호화하여 노출을 방지함.



### JWT

Bearer, Basic, JWT

로그인 세션에 대한 검증 혹은 

클라이언트에서 서버로 보내지는 데이터는 위변조가 가능 

데이터의 기밀성 보장: 데이터 자체를 노출시키지 않음 (encrypt) 따라서 JWT는 여기에 해당안됨. jwt.io 가서 decode하면 다 보임. 따라서 기밀 데이터는 JWT에 담으면 안된다.

데이터의 무결성 보장: 



쿠키가 유효한 쿠키인지 jwt.verify()를 쓴다 (검증하기 위한 키가 필요하다)



`npm i jsonwebtoken` 

`npm i react-hook-form`