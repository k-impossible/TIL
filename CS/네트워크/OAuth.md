## OAuth
전통적으로 직접 작성한 서버에서 인증을 처리해 주는 것과는 달리 OAuth는 인증을 중개해 주는 메커니즘이다. 보안된 리소스에 액세스하기 위해 클라이언트에게 권한을 제공하는 프로세스를 단순화하는 프로토콜이다. 이미 사용자 정보를 가지고 있는 웹 서비스(Naver, Kakao, Google 등)에서 사용자의 인증을 대신해 주고 접근 권한에 대한 토큰을 발급한 후 이를 이용해 내 서버에서 인증이 가능해진다.
### OAuth의 장점
- 쉽고 안전하게 새로운 서비스를 이용할 수 있다.
  - 사용자는 OAuth를 통해 특정 사이트에 아이디, 비밀번호 등의 정보를 일일이 입력하지 않아도 간편하게 가입할 수 있어 편리하다.
  - 정보를 해당 서비스에 직접 노출하는 것이 아니기 때문에 직접 가입하는 것보다 안전하다.
  - 어플리케이션 입장에서도 회원의 정보를 직접 가지고 있음으로 인해 발생할 수 있는 정보 유출의 위험성에서 부담을 덜 수 있다.
- 권한 영역을 설정할 수 있다.
  - OAuth인증을 허가한다고 해서 새로운 서비스가 사용 중이던 서비스의 모든 정보에 접근이 가능한 것은 아니다. 사용자는 원하는 정보에만 접근을 허락할 수 있어 보다 더 안전하다.
  - OAuth 설정 페이지에서는 어플리케이션에서 필요한 정보를 선택할 수 있다. 사용자는 이 중 원하는 정보만 선택적으로 제공할 수 있다.
## OAuth 작동 메커니즘
### OAuth의 주체
- Resource Owner
  - OAuth인증을 통해 소셜 로그인을 하고 싶어 하는 사용자
  - Resource는 사용자의 이름, 전화번호 등의 정보를 뜻한다.
- Resource Server & Authorization Server
  - 사용자가 소셜 로그인을 하기 위해서 사용하는 이미 사용 중인 서비스(Naver, Kakao 등)의 서버 중 사용자의 정보를 저장하고 있는 서버를 Resource Server 라고 한다.
  - 이미 사용 중인 서비스의 서버 중 인증을 담당하는 서버를 Authorization Server 라고 한다.
- Application
  - 사용자가 소셜 로그인을 활용해 이용하고자 하는 새로운 서비스
  - 경우에 따라서 클라이언트와 서버로 세분화해서 지칭하기도 한다.
### OAuth 인증 방식의 종류와 흐름
#### Implicit Grant Type
소셜로그인에서 Implicit Grant Type은 잘 사용하지 않는다. 기존 서비스에 로그인만 되어있다면 새로운 서비스에 바로 액세스 토큰을 내어주기 때문에 보안성이 떨어지기 때문이다. 그래서 보통은 여기에 인증 단계를 한 단계 추가한 인증 방식인 Authorization Code Grant Type을 주로 사용하게 된다.
- 사용자가 Application에 접속한다.
- Application에서 Authorization Server로 인증 요청을 보낸다.
- Authorization Server는 유효한 인증 요청인지 확인한 후 액세스 토큰을 발급한다.
- Authorization Server에서 Application으로 액세스 토큰을 전달한다.
- Application은 발급받은 액세스 토큰을 담아 Resource Server로 사용자의 정보를 요청한다.
- Resource Server는 Application에게서 전달받은 액세스 토큰이 유효한 토큰인지 확인한다.
- 유효한 토큰이라면 Application이 요청한 사용자의 정보를 전달한다.

#### Authorization Code Grant Type
Implicit Grant Type과 비교해보면 Authorization Code를 사용한 인증 단계가 추가로 있기 때문에 비교적 더 안전하다. 원한다면 중간에 Local Server를 통해 토큰을 클라이언트에 노출시키지 않고 서버에서만 관리하도록 만들 수도 있다. 그런데 사용자가 새로운 서비스를 이용하다가 액세스 토큰이 만료되었을 때, 매번 이 과정을 거쳐서 액세스 토큰을 다시 발급받아야 한다면 사용자 편의성에 있어서는 좋지 않다. 그래서 액세스 토큰을 발급해 줄 때 리프레시 토큰을 같이 발급해주기도 한다. 이때 리프레시 토큰을 사용해서 액세스 토큰을 받아오는 인증 방식을 Refresh Token Grant Type이라고 한다.
- 사용자가 Application에 접속한다.
- Application에서 Authorization Server로 인증 요청을 보낸다.
- Authorization Server는 유효한 인증 요청인지 확인한 후 `Authorization Code`를 발급한다.
- Authorization Server에서 Application으로 `Authorization Code`를 전달한다.
- Application이 Authorization Server로 발급받은 `Authorization Code`를 전달한다.
- Authorization Server는 유효한 `Authorization Code`인지 확인한 후 액세스 토큰을 발급한다.
- Authorization Server에서 Application으로 액세스 토큰을 전달한다.
- Application은 발급받은 액세스 토큰을 담아 Resource Server로 사용자의 정보를 요청한다.
- Resource Server는 Application에게서 전달받은 액세스 토큰이 유효한 토큰인지 확인한다.
- 유효한 토큰이라면 Application이 요청한 사용자의 정보를 전달한다.

#### Refresh Token Grant Type
Application에서 Authorization Server로 리프레시 토큰을 보내주면 Authorization Server는 리프레시 토큰을 검증한 다음 액세스 토큰을 다시 발급해 주게 된다. Application은 다시 발급받은 액세스 토큰을 사용해 Resource Server에서 사용자의 정보를 받아오게 된다.