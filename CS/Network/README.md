# Network

<details>
<summary> HTTPS이 보안이 뛰어난 이유 </summary>
<div markdown="1">
<br>
  
- ‘HTTP vs HTTPS 차이’는 바로 **SSL 인증서**
- SSL 인증서는 사용자가 사이트에 제공하는 정보를 암호화하는데, 쉽게 말해서 **데이터를 암호로** 바꾼다고 생각하면 쉽다.
- 따라서 중간에 누가 훔쳐봐도 기본적인 보안 대응이 가능함.
- 이렇게 전송된 데이터는 중간에서 누군가 훔쳐 낸다고 하더라도 **데이터가 암호화되어있기 때문에 해독할 수 없다.**

- 그 외에도 HTTPS는 **TLS(전송 계층 보안) 프로토콜을 통해서도 보안을 유지**한다.
- TLS은 데이터 무결성을 제공하기 때문에 데이터가 전송 중에 수정되거나 손상되는 것을 방지
- 사용자가 자신이 의도하는 웹사이트와 통신하고 있음을 입증하는 인증 기능도 제공
    - 부연설명: TLS때문에 나쁜사용자가 라우터에서 IP주소를 조작하더라도 HTTPS를 쓰면 무결성 때문에 올바른 서버주소와 통신을 할 수 있게 해준다!!
- 즉, 내가 원하는 서버IP 주소와 통신할 수 있는 것은 TLS때문이고, 데이터를 훔쳐봐도 해독할 수 없게 해주는것은 SSL때문이다.

<br>
</div>
</details>

<details>
<summary> HTTP Connections에서 Non-Persistent 와 Persistent </summary>
<div markdown="1">
<br>
  
- `Non-Persistent`
    - TCP 연결 한번에 **최대 하나의 객체**를 전송할 수 있다.
    - 필요할 때에 TCP연결을 한다.
    - 오브젝트마다 2번의 RTT+전송타임이 걸린다고 볼 수 있음.

- `Persistent`
    - TCP 연결 한번에 **여러개의 객체**를 전송할 수 있다.
    - 한번 TCP연결을 하고 종료 될때까지 재사용 한다.
    - 여러번의 오브젝트를 보낼 수 있다.
    - 평균적으로는 1번의 RTT+전송타임이 걸린다고 볼 수 있음.
  
<br>
</div>
</details>

<details>
<summary> TCP/UDP 차이 </summary>
<div markdown="1">
<br>

- TCP는 UDP에 비해 하는일이 많아서 헤더가 기본적으로 UDP보다 복잡하고 크다.
- TCP는 Connection Oriented 기반이라 handshaking과정이 있고, UDP는 연결과정은 없음.
- TCP는 신뢰가 보장된 프로토콜이고, UDP도 헤더에 체크썸이 있어 기본적인 비트에러감지정돈 해준다.
- 그외에도 TCP는 congestion control, flow control, 3 duplicate ack, 등등 한다고 햇음

<br>

  ![스크린샷 2022-03-28 오후 10 15 02](https://user-images.githubusercontent.com/74236080/161303983-0919112a-5839-4f42-88d0-d517d9345393.png)

<br>
</div>
</details>






