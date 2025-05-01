# 개발 환경 주의사항 및 가이드라인

## 1. 개발 환경 설정

### Node.js 버전 관리

- 프로젝트는 Node.js 20 버전을 사용합니다.
- `nvm`(Node Version Manager)을 사용하여 버전을 관리하는 것을 권장합니다.
- 윈도우: [nvm-windows](https://github.com/coreybutler/nvm-windows)
- 맥: [nvm](https://github.com/nvm-sh/nvm)

### 의존성 관리

- 새로운 패키지 설치 시 `npm install` 대신 `npm ci` 사용을 권장합니다.
- 이는 `package-lock.json`에 명시된 정확한 버전을 설치합니다.
- 의존성 업데이트가 필요한 경우 `npm audit`을 실행하여 보안 취약점을 확인하세요.

## 2. Git 작업 시 주의사항

### 줄바꿈 문자(Line Endings)

- 프로젝트는 `.gitattributes`를 통해 줄바꿈 문자를 자동으로 관리합니다.
- 윈도우 사용자는 Git의 `core.autocrlf` 설정이 `true`로 되어 있는지 확인하세요:
  ```bash
  git config --global core.autocrlf true
  ```

### 커밋 메시지

- 커밋 메시지는 명확하고 이해하기 쉽게 작성하세요.
- 변경사항의 내용과 이유를 포함하세요.

## 3. 코드 작성 가이드라인

### 파일 경로

- 파일 경로를 하드코딩할 때는 `/`를 사용하세요 (윈도우에서도 작동합니다).
- `path.join()`이나 `path.resolve()`를 사용하면 더 안전합니다.

  ```typescript
  import path from "path";

  // 권장
  const filePath = path.join("src", "components", "Button.tsx");

  // 비권장
  const filePath = "src\\components\\Button.tsx";
  ```

### 환경 변수

- `.env` 파일을 사용하는 경우, 양쪽 환경에서 동일한 환경 변수를 사용하도록 주의하세요.
- 민감한 정보는 절대 커밋하지 마세요.

## 4. 크로스 플랫폼 개발 시 주의사항

### 운영체제별 특이사항

- 맥: `.DS_Store` 파일이 자동으로 생성되지 않도록 `.gitignore`에 설정되어 있습니다.
- 윈도우: 파일 경로 관련 이슈가 발생할 수 있으므로 위의 파일 경로 가이드라인을 준수하세요.

### 개발 서버 실행

- 개발 서버는 `npm run dev`로 실행합니다.
- 포트 충돌이 발생할 경우 `vite.config.ts`에서 포트를 변경할 수 있습니다.

## 5. 배포 관련

### GitHub Pages 배포

- `main` 브랜치에 푸시하면 자동으로 배포가 시작됩니다.
- 배포 상태는 GitHub Actions에서 확인할 수 있습니다.
- 배포된 사이트는 https://linekiller89.github.io/linekiller89.github.io/ 에서 확인할 수 있습니다.

## 6. 문제 해결

### 일반적인 이슈

1. 의존성 관련 문제

   - `node_modules` 폴더 삭제 후 `npm ci` 실행
   - `package-lock.json` 삭제 후 `npm install` 실행

2. 타입스크립트 관련 문제

   - `tsc --noEmit`으로 타입 체크 실행
   - IDE의 타입스크립트 서버 재시작

3. 빌드 실패
   - 캐시 삭제: `npm cache clean --force`
   - `dist` 폴더 삭제 후 재빌드

### 지원

- 문제 발생 시 이슈를 생성하여 팀원들과 공유하세요.
- 긴급한 문제는 팀 채팅을 통해 공유하세요.
