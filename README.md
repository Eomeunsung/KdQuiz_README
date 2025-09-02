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
<img width="599" height="546" alt="스크린샷 2025-09-02 12 50 42" src="https://github.com/user-attachments/assets/8009dea9-4f39-4ec5-93df-79c79ab7d88e" />


## 유스케이스다이어그램
<img width="648" height="232" alt="image" src="https://github.com/user-attachments/assets/c88aecab-e56f-4ce6-9161-dde76c6d3ff0" />

## 시퀀스 다이어그램
<table>
    <tr>
    <td>
      <img width="605" height="542" alt="image" src="https://github.com/user-attachments/assets/969eb60b-9a35-406a-aca3-a4212667f2a0" />
    </td>
    <td>
      <img width="605" height="515" alt="image" src="https://github.com/user-attachments/assets/71ea0edc-cd83-4413-a097-4a054ebfde18" />
    </td>
  </tr>
  <tr>
    <td align="center">로그인</td>
    <td align="center">회원가입</td>
  </tr>
  
  <tr>
    <td>
      <img width="558" height="732" alt="image" src="https://github.com/user-attachments/assets/dd30c2b9-6e0a-45fc-a475-32db0b53e750" />
    </td>
    <td>
      <img width="605" height="520" alt="image" src="https://github.com/user-attachments/assets/5c19f7af-2eb4-4b1b-bd13-20d01572cbeb" />
    </td>
  </tr>
  <tr>
    <td align="center">로그아웃</td>
    <td align="center">개인정보 수정</td>
  </tr>

  <tr>
    <td>
      <img width="605" height="496" alt="image" src="https://github.com/user-attachments/assets/89105d84-6c3c-474e-b4a0-a03e24735356" />
    <td>
      <img width="671" height="601" alt="스크린샷 2025-08-26 14 32 09" src="https://github.com/user-attachments/assets/e223e4ba-5bf0-4340-9094-82a56aec8cb7" />
    </td>
  </tr>
  <tr>
    <td align="center">Quiz 제작 및 수정</td>
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

<img width="605" height="339" alt="image" src="https://github.com/user-attachments/assets/3d2e33d0-c57f-45c3-8378-c4368d4c33ad" />

- **메인화면**
---

<img width="605" height="339" alt="image" src="https://github.com/user-attachments/assets/a1f68adf-3c36-4292-9374-5118a0f1b721" />

- **로그인 화면**
---

<img width="605" height="339" alt="image" src="https://github.com/user-attachments/assets/d6f06b0d-f242-40c9-a845-e8923f101181" />

- **회원가입 화면**
---

<img width="605" height="340" alt="image" src="https://github.com/user-attachments/assets/114f362b-b13f-496a-9c65-880f651c1417" />

- **프로젝트 라이브러리 화면**
---

<img width="1440" height="809" alt="스크린샷 2025-09-02 13 41 15" src="https://github.com/user-attachments/assets/de180ce7-a2bd-428d-9c34-c56c3fb93002" />

- **퀴즈 제작 화면**
---

<img width="1440" height="809" alt="스크린샷 2025-09-02 13 41 29" src="https://github.com/user-attachments/assets/8ac6ce67-aff9-4279-8591-fc72b016a05f" />

- **게임 참여**
---

<img width="1440" height="809" alt="스크린샷 2025-09-02 13 41 34" src="https://github.com/user-attachments/assets/6433ca5b-16dc-4b10-b293-a474a568a53b" />
<img width="1440" height="809" alt="스크린샷 2025-09-02 13 43 51" src="https://github.com/user-attachments/assets/6781a2a7-9229-4cd4-b303-4718fde88b64" />

- **게임 플레이 화면**
---

<img width="1440" height="809" alt="스크린샷 2025-09-02 13 44 01" src="https://github.com/user-attachments/assets/94f8e7f2-4e69-4fc4-808f-f2a18443b8cd" />

- **점수 및 랭킹 화면**
---


