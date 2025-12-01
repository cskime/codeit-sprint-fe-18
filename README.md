# CodeIt Sprint FE 18

## Overview

- 코드잇 스프린트 부트캠프 Frontend 과정 18기
- 학습 기간 : 2025.06.10 ~ 2025.12.05 (26주)
- 학습 기술
  - HTML, CSS, JavaScript
  - React, Next.js (Page Router)
  - TypeScript
  - styled-components, CSS modules, Tailwind CSS
  - Zustand, React Query
  - overlay-kit

## Projects

- 스프린트 기간 중 3번의 협업 프로젝트 진행
- 모든 프로젝트를 주도적으로 리드하며 다양한 역할 수행
  - 프로젝트 초기 설정 및 배포
  - 팀원 별 실력 차이를 고려한 R&R 분배
  - 개발 일정 관리
  - 팀원들이 올리는 PR 검토 및 코드 리뷰
  - 프로젝트 중 발생하는 문제 해결
- 프로젝트에 적극적으로 참여하고 원활하게 소통하며 팀원들에게 긍정적인 피드백을 받음

### [Rolling: 롤링 페이퍼 커뮤니티 플랫폼](https://github.com/cskime/rolling)

10주차에 2주간 진행한 기초 프로젝트

- 역할 : 팀원
- 경험 : 
- 기여 : 

### [Taskify: 커뮤니티 일정 관리 및 공유 서비스](https://github.com/cskime/Taskify)

17주차에 2주간 진행한 중급 프로젝트

- 역할 : 팀장
- 경험 : 
- 기여 : 

### [Coworkers: 업무 배정 및 현황 공유 서비스](https://github.com/cskime/coworkers)

22주차에 4주간 진행한 심화 프로젝트

- 역할 : 팀장
- 경험 : 
- 기여 : 

### 프로젝트 종료 후 동료 평가

<img src="./images/peer-review-1.png" />

---

<img src="./images/peer-review-2.png" />

## 활동

### Study

코드잇 강의 내용 외에 더 깊이있게 공부하기 위해 동기들과 함께 JavaScript 및 React 스터디 진행

- [코어 자바스크립트 도서 스터디](https://github.com/cskime/study-log/tree/main/core-javascript)
- [React 공식 문서 스터디](https://github.com/FE18-Survivor/react-docs-study)

### 리팩터링 릴레이 이벤트

<img src="./images/refactoring-relay.png" alt="refactoring relay" width="500" />

- 중급 프로젝트에서 구현했던 코드 중 개선 사례를 스프린트 동기들과 공유
- TypeScript에서 `enum`을 사용했을 때 문제점과 union literal type을 활용한 개선 사례 공유
- 리팩터링 대상 코드
  ```typescript
  // 📂 components/menu/index.tsx
  export enum Direction {
    Left = "directionLeft",
    Right = "directionRight",
  }

  interface Props extends PropsWithChildren {
    items: ReactNode[];
    direction?: Direction;
  }

  export function Menu({ items, children, direction = Direction.Left }: Props) { ... }

  // 실제 사용 예시
  <Menu
    items={[MenuItem.edit(onEdit), MenuItem.delete(onDelete)]}
    direction={Direction.Right}
  >
    <MoreIcon color={Color.Gray300} />
  </Menu>
  ```
- 리팩터링 후 코드
  ```typescript
  // 📂 components/menu/index.tsx
  interface Props extends PropsWithChildren {
    items: ReactNode[];
    direction?: "left" | "right";
  }
  
  export function Menu({ items, children, direction = "left" }: Props) { ... }
  
  // 실제 사용 예시
  <Menu
    items={[MenuItem.edit(onEdit), MenuItem.delete(onDelete)]}
    direction="right"
  >
    <MoreIcon color={Color.Gray300} />
  </Menu>
  ```
- 리팩터링 포인트 & 이유
  - 리팩토링 포인트 : TypeScript의 enum을 union literal type로 변경
  - 이유 
    - 열거형은 제한된 갯수의 값을 안전하게 사용할 수 있는 것이 핵심 기능
    - 하지만, TypeScript의 열거형은 JavaScript 객체로 변환되므로 열거형 문법이 아닌 일반 값도 할당할 수 있어서 불완전함
      - `number` type 값을 갖는 enum에는 어떤 숫자도 전달할 수 있음
      - enum에 정의된 case 이외에 값을 할당하게 되면 runtime에 error가 발생할 수 있음
    - Union literal type을 사용하면 정해진 값을 안전하게 사용할 수 있고 IDE의 자동완성 기능을 활용하여 생산성도 향상됨
    - 열거형은 별도의 Direction type을 따로 만들어야 하고 Direction.Right와 같이 작성해야 하는 등 코드가 장황해질 수 있지만, union literal type을 사용하면 값만 간단하게 사용할 수 있음