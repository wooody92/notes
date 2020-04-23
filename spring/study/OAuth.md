## OAuth

### Oauth 란?

- 나의 서비스(내가 만든 어플리케이션)가 사용자의 다른 서비스(구글, 페이스북 등)의 API를 사용하기 위해 권한을 받는 것
- 사용자는 다른 사비스의 아이디 패스워드를 나의 서비스에 공개없이 안전하게 이용 할 수 있다.

### 역할

- Client : 나의 서비스, 우리가 만든 신규 서비스, 구글 정보를 이용하여 로그인하고 사용자 정보를 가져온다.
- Resource Server (+ Authorization Server) : 다른 서비스, 구글, 인증 정보와 데이터를 모두 갖고있다.
- Resource Owner : 사용자, 리소스 서버에 로그인 가능한 일반 사용자.

### 등록

- OAuth를 사용하려면 클라이언트 앱을 리소스 서버에 등록을 해야한다.
- 클라이언트가 리소스 서버에 등록하기 위한 필수요소 : Client ID, Client Secret, Authorized Redirect URIs

### 과정

- 사용자가 나의 서비스에 접속하여 구글의 기능을 사용하고자 한다.
- 나의 서비스는 구글 인증 허가 링크를 사용자에게 요청한다.
- 사용자는 구글에 로그인하고 나의 서비스가 해당 API들을 요청했는데 허가 할 것인지 사용자의 동의를 구한다.
- 구글은 클라이언트 아이디와 리다이렉트 유알엘이 일치하는 지 확인한다.
- 사용자가 허가하면 구글은 나의 서비스가 해당 API를 사용 할 수 있도록 DB 혹은 서버에 등록한다.
- 구글은 사용자에게 authorization code를 부여하고 사용자는 그 코드를 가지고 나의 서비스에 접속한다.
- 이제 나의 서비스는 사용자로부터 받은 코드와 클라이언트 ID, Secret, URL 을 기반으로 구글에 액세스 토큰을 요청한다.
-  구글은 정보가 모두 일치하는 지 확인 후 나의 서비스에 액세스 토큰을 부여한다. (authorization code는 이제 필요 없으므로 양쪽 모두 삭제된다.)


### Github OAuth

#### 공식문서

- https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/

#### 참고 링크

- https://gist.github.com/blossun/5057cf64f85b809fd76c1c1c750e8cdf
