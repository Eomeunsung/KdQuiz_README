# KdQuiz_졸업작품

#키득퀴즈(KdQuiz)
본 프로젝트는 졸업작품으로 진행된 퀴즈 기반 학습 플랫폼입니다.
실시간 플레이 기능은 구현하지 못하였으며, 퀴즈 생성·수정·삭제 및 참여자 관리 등 기본 기능 위주로 개발하였습니다.

## Repository
- **Front**: https://github.com/Eomeunsung/Kquiz-Front.git (아직 반영안함)
- **BackEnd**: https://github.com/Eomeunsung/Kquiz-Back.git (아직 반영안함)

## 팀원
- **보고서** : 2명
- **프로젝트 초기 버전 및 초기 환경 구성** : 1명
- **프론트엔드** : 1명
- **백엔드** : 1명 (본인)
  
## 주요 기능 
- **로그인 / 회원가입 기능**
회원가입은 이메일, 비밀번호, 이름을 입력받아 진행하며, 이메일 인증 절차를 거친 후 가입이 완료된다. 로그인 시 입력한 이메일과 비밀번호를 DB에서 확인하여 일치하면 마이페이지로 이동한다.

- **퀴즈 프로젝트 라이브러리 기능**
로그인 후 마이페이지에서 본인이 만든 퀴즈 프로젝트를 라이브러리 탭에서 확인할 수 있다. 프로젝트가 없을 경우 ‘퀴즈 프로젝트가 존재하지 않음’ 메시지와 함께 생성 버튼이 표시되며, 생성 버튼 클릭 시 프로젝트명을 입력하고 편집 페이지로 이동한다.

- **퀴즈 프로젝트 생성 및 편집 기능**
편집 페이지에서는 PowerPoint와 유사한 방식으로 슬라이드와 퀴즈를 추가할 수 있다. 퀴즈는 객관식, 주관식, 끝말잇기, 초성 퀴즈 등 다양한 유형을 선택할 수 있으며, 시간 제한, 점수 설정, 답변 재선택 등의 옵션을 지정할 수 있다. 슬라이드는 텍스트와 이미지를 자유롭게 배치할 수 있다. 생성 완료 시 진행 상황이 DB에 저장된다.

- **퀴즈 프로젝트 시작 및 참여**
게임 생성자는 라이브러리에서 프로젝트를 선택하여 게임을 시작할 수 있다. 참여자는 PIN 번호 입력 또는 QR코드 스캔으로 닉네임을 설정한 뒤 게임에 입장한다.
퀴즈 종료 후 생성자는 전체 참여자의 점수와 순위를 확인할 수 있으며, 참여자는 본인의 점수와 현재까지 퀴즈를 푼 플레이어들의 순위를 확인할 수 있다.

## 기술 스택
- **Frontend**: TypeScript, Next.js, Antd, chakraUi, Node.js, AWS
- **Backend**: JAVA, Spring Boot, MySql, Redis
- **Version Control**: Git, GitHub

## 프로젝트 후기
아직 반영 안함

## 구현시 어려웠던 부분
- **문제**: 웹 소켓을 활용한 실시간 퀴즈 플레이 구현 초기에는 각 클라이언트(참여자 및 호스트)에게 각 개별적인 문제 데이터를 전송하여, 퀴즈 풀이 하도록 하였습니다. 하지만 네트워크 지연시 타이머 불일치, 문제도 데이터 불일치 등 동기화 및 오류가 발생하였습니다.
  
- **해결**: 모든 문제 데이터 전송 및 타이머 기준을 호스트 중심으로 변경했습니다. 호스트가 웹  소켓을 통해 문제 데이터를 요청하면 서버가 조회 후 구독중인 모든 클라이언트에게 동일한 데이터를 전송 하도록 했습니다. 타이머 역시 서버에서 호스트 기준으로 전송하여 모든 클라이언트가 동기화 되도록 구현했습니다.
  
- **결과**: 네트워크 상태가 불안정해도 모든 클라이언트는 동일한 문제를 보고, 남은 시간도 일치하게 되어 안정적인 실시간 퀴즈 플레이가 가능해졌습니다.

## ERD다이어그램
<img width="1161" height="543" alt="스크린샷 2025-08-02 15 30 32" src="https://github.com/user-attachments/assets/377df189-5e16-4c1b-a13e-8c813b4c49d7" />

## 흐름도
<table>
    <tr>
    <td>
      <img width="562" height="362" alt="스크린샷 2025-08-26 18 24 40" src="https://github.com/user-attachments/assets/e7978416-ba54-43b7-9b63-0dd9f1ed3bc3" />
    </td>
    <td>
       <img width="697" height="452" alt="스크린샷 2025-08-26 18 59 24" src="https://github.com/user-attachments/assets/8632da2a-9208-457f-8a1c-0a1afc1a19c9" />
    </td>
  </tr>
  <tr>
    <td align="center">로그인</td>
    <td align="center">회원가입</td>
  </tr>
  
  <tr>
    <td><img width="448" height="663" alt="quiz create" src="https://github.com/user-attachments/assets/8c7419fa-5dbd-47d0-ab3d-8bd0cf377674" /></td>
    <td><img width="335" height="585" alt="스크린샷 2025-07-23 13 29 40" src="https://github.com/user-attachments/assets/c4b038e0-1cfb-4676-a365-07e188ed3832" /></td>
  </tr>
  <tr>
    <td align="center">Quiz 생성</td>
    <td align="center">Quiz 수정(아직 반영 안함)</td>
  </tr>

  <tr>
    <td>
      <img width="392" height="629" alt="스크린샷 2025-07-23 13 25 31" src="https://github.com/user-attachments/assets/67dfd1ad-45aa-4f4a-b3d0-50c81f991320" />
      </td>
    <td>
      <img width="671" height="601" alt="스크린샷 2025-08-26 14 32 09" src="https://github.com/user-attachments/assets/e223e4ba-5bf0-4340-9094-82a56aec8cb7" />
    </td>
  </tr>
  <tr>
    <td align="center">Quiz 삭제</td>
    <td align="center">게임 생성</td>
  </tr>

  
  <tr>
    <td>
      <img width="403" height="554" alt="스크린샷 2025-08-26 17 20 11" src="https://github.com/user-attachments/assets/41b4b475-c91f-4e5b-ba09-b81d6cc1c77d" />
    </td>
    <td>
      <img width="390" height="631" alt="스크린샷 2025-08-26 17 55 13" src="https://github.com/user-attachments/assets/7fe9372f-e1e1-45eb-a838-bed7ee376293" />
    </td>
  </tr>
  <tr>
    <td align="center">게임 참여</td>
    <td align="center">게임 플레이</td>
  </tr>

</table>

## 프로젝트 결과물
<img width="1404" height="807" alt="main" src="https://github.com/user-attachments/assets/4bbca513-707c-49dc-adac-1ffd46ecd0b4" />

- **메인화면**
---
  
<img width="1404" height="807" alt="signUp" src="https://github.com/user-attachments/assets/c66a5589-c96d-4a51-a7c4-89f37e2c3f6b" />

- **회원가입 화면**
---

<img width="1404" height="807" alt="signIn" src="https://github.com/user-attachments/assets/90a24e79-355f-4b8b-b9c3-70c92f3467bb" />

- **로그인 화면**
---

<img width="1404" height="807" alt="quiz create" src="https://github.com/user-attachments/assets/e8f849de-144a-4f84-9b3d-f261c5834d6b" />

- **퀴즈 생성 화면**
---

<img width="1404" height="807" alt="quiz create2" src="https://github.com/user-attachments/assets/b3b78e4f-b32f-4cd1-a79b-80c166396a5b" />

- **퀴즈 제작 화면(AI 힌트 사용)**
---

<img width="1404" height="807" alt="quiz create3" src="https://github.com/user-attachments/assets/36d90d86-43f2-4d5a-9572-e26b1f15f2d5" />


- **퀴즈 제작 화면2**
---

<img width="1404" height="807" alt="quiz create main" src="https://github.com/user-attachments/assets/5544d4f4-127c-43f2-96cc-a87535ca1a94" />

- **개인 채팅 화면**
---

<img width="1404" height="807" alt="game create" src="https://github.com/user-attachments/assets/3aba3557-e23c-41bd-b184-7799363c2abf" />

- **게임 생성 화면**
---

<img width="1404" height="807" alt="lobby" src="https://github.com/user-attachments/assets/491a9122-2f0a-494b-b128-0ff42ac689cb" />

- **호스트 로비 화면**
---

<img width="1404" height="807" alt="lobby2" src="https://github.com/user-attachments/assets/491a9122-2f0a-494b-b128-0ff42ac689cb" />

- **참여자 게임 참여 화면**
---

<img width="1404" height="807" alt="lobby3" src="https://github.com/user-attachments/assets/09ac8ff7-4513-48fa-b98d-8e7362203774" />

- **참여자/호스트 로비 화면**
---

<img width="1095" height="506" alt="스크린샷 2025-08-27 11 45 31" src="https://github.com/user-attachments/assets/f1267ccb-fa7b-49f9-a835-59a564cdb525" />

- **강퇴 기능**
---

<p align="center">
  <img src="https://github.com/user-attachments/assets/a6f2f88d-1f3d-4191-87dc-c890b1e12e20" width="45%" />
  <img src="https://github.com/user-attachments/assets/9f7e45d6-5a0c-4b47-aadb-645e00bbd9ff" width="45%" />
</p>


- **문제 풀이**
---

<img width="1432" height="583" alt="스크린샷 2025-08-27 12 09 21" src="https://github.com/user-attachments/assets/efbccfec-166a-467b-a54f-f9b00088b598" />

- **게임 종료 후 랭킹 반환**
---

<img width="1390" height="781" alt="스크린샷 2025-08-27 12 45 11" src="https://github.com/user-attachments/assets/0e4984d0-fcfb-4123-a0c9-6fef92ebdd4d" />

- **관리자 기능**
---
  
<img width="1390" height="781" alt="스크린샷 2025-08-27 12 45 24" src="https://github.com/user-attachments/assets/d4f01982-14fa-4927-957d-e2450223c735" />

- **관리자 유저 설정**
---

<img width="1390" height="781" alt="스크린샷 2025-08-27 12 45 29" src="https://github.com/user-attachments/assets/f6264d7b-9602-4c7a-8650-64496ad9bee8" />

- **관리자 퀴즈 설정**
---

