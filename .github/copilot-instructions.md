## 목적

이 파일은 이 레포지토리에서 AI 코딩 에이전트가 곧바로 생산적으로 작업할 수 있도록 핵심 컨텍스트와 규칙을 간결하게 제공합니다.

## 프로젝트 개요 (한 줄 요약)

- 학습용 정적 React 예제 모음입니다. 번들러나 패키지 매니저 없이 CDN으로 React/ReactDOM과 Babel(standalone)을 사용해 브라우저에서 JSX를 바로 실행합니다.
- 주요 파일: `index.html`, `index2.html`, ..., `index5.html`, `vanilla.html` — 각 파일은 독립적인 수업/예제입니다.

## 아키텍처와 설계 의도

- 브라우저에서 직접 JSX를 해석하기 위해 `@babel/standalone`을 사용합니다. 따라서 프로젝트에는 `package.json`이나 빌드 파이프라인이 없습니다.
- 목적은 빠른 학습/실험: 각 HTML 파일이 독립된 스테이지(lesson)로 동작합니다. 변경은 해당 HTML 파일을 복사/수정해 새 예제를 추가하는 방식으로 이뤄집니다.

## 중요한 개발 워크플로우

- 로컬에서 확인: 단순히 브라우저로 파일을 열어도 동작하지만 CORS/파일 경로 문제를 피하려면 간단한 정적 서버를 사용하세요.

PowerShell 예시:
```powershell
# Python이 설치된 경우
python -m http.server 3000

# 또는 npm이 설치된 경우 (http-server가 없다면 먼저 'npm i -g http-server')
npx http-server -p 3000
```

- 브라우저에서 `http://localhost:3000/index5.html` 처럼 열어 테스트합니다.

## 코드패턴 & 규약 (이 프로젝트에 특화된 사항)

- JSX/ESNext 코드를 직접 HTML에 둡니다: <script type="text/babel"> ... </script>.
- React는 CDN(UNPKG)에서 로드합니다. 예: React 17 / ReactDOM 17 / PropTypes / Babel.
- 각 HTML 파일은 #root 같은 루트 DOM 노드를 사용해 마운트합니다.
- 파일 이름 규칙: index*.html은 단계별 예제(lesson). 새로운 예제는 기존 파일을 복사해 숫자를 증가시키는 방식으로 추가하세요.

## 구체적 예시 (repo에서 관찰한 패턴)

- `index5.html`의 `Btn` 컴포넌트:
  - Props: `text`(string, required), `fontSize`(number, default 14). PropTypes를 사용해 런타임 검증.
  - 스타일 객체를 직접 인라인으로 선언.
  - `console.log`를 이용해 렌더 확인(학습/디버깅용).

- 주의: `index5.html`은 `react.development.js`와 함께 `react-dom.production.min.js`를 포함하고 있습니다. 개발 중에는 둘 다 development 빌드를 쓰는 것이 디버깅에 더 낫습니다. (일관된 빌드 유형을 권장)

## 통합 포인트 / 외부 의존성

- 전부 CDN(UNPKG)을 통해 제공됩니다. 네트워크가 차단된 환경에서는 동작하지 않을 수 있습니다.
- 외부 서비스 연동은 현재 없음(예: 백엔드 API). 추가할 경우 CORS와 정적 서버 정책을 고려해야 합니다.

## 변경/확장 시 권장 사항

- 장기적으로 패키지 매니저와 번들러(예: Vite/CRA)를 도입하면 모듈형 개발과 테스팅이 쉬워집니다. 하지만 현재 레포는 학습 목적이므로 즉시 바꾸지 마세요.
- 새로운 예제를 만들 땐 기존 `indexX.html`을 복사하고 파일 상단의 스크립트(React/ReactDOM/PropTypes/Babel) 포함 순서를 지키세요.

## 디버깅 팁

- 브라우저 개발자 도구 콘솔을 사용해 Babel-컴파일 에러와 런타임 에러를 확인하세요.
- 네트워크 탭에서 CDN 스크립트가 제대로 로드되는지 확인합니다.

## 예시 명령(요약)

```powershell
python -m http.server 3000
# 또는
npx http-server -p 3000
# 브라우저에서 열기: http://localhost:3000/index5.html
```

## 마무리 및 요청

- 이 파일은 레포지토리의 명확한 상태(정적, CDN 기반, 학습용)를 요약합니다. 누락된 정보(예: 특정 브라우저 호환성, 추가 의존성, 의도한 React/ReactDOM 버전 매칭 등)가 있다면 알려주세요. 수정해 반영하겠습니다.
