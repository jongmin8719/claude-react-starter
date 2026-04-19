# claude-react-starter

React 19 + TypeScript + Vite 기반 프론트엔드 스타터킷입니다.

## 기술 스택

| 항목 | 라이브러리 |
|------|-----------|
| 프레임워크 | React 19 |
| 언어 | TypeScript 6 |
| 빌드 도구 | Vite 8 |
| 라우팅 | React Router v7 |
| 전역 상태관리 | Zustand |
| 서버 상태/API | TanStack Query + Axios |

## 시작하기

```bash
# 의존성 설치
npm install

# 개발 서버 실행
npm run dev

# 빌드
npm run build
```

## 환경 변수

`.env.local` 파일을 생성하여 환경 변수를 설정합니다.

```env
VITE_API_BASE_URL=https://api.example.com
```

## 폴더 구조

```
src/
├── api/            # API 클라이언트, QueryClient 설정
│   ├── client.ts   # Axios 인스턴스
│   └── queryClient.ts
├── components/     # 공통 컴포넌트
├── hooks/          # 커스텀 훅
├── layouts/        # 레이아웃 컴포넌트
├── pages/          # 페이지 컴포넌트
├── stores/         # Zustand 스토어
├── types/          # 타입 정의
└── router.tsx      # 라우터 설정
```

## 경로 별칭

`@/`를 `src/` 경로 별칭으로 사용합니다.

```ts
import { useAppStore } from '@/stores/useAppStore';
import apiClient from '@/api/client';
```

## 스타일링 설정

이 스타터킷은 스타일링 도구를 포함하지 않습니다. 프로젝트에 맞게 아래 중 하나를 선택하세요.

### Tailwind CSS v4

```bash
npm install tailwindcss @tailwindcss/vite
```

`vite.config.ts`에 추가:
```ts
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

`src/index.css` 상단에 추가:
```css
@import "tailwindcss";
```

### SCSS

```bash
npm install -D sass
```

`.scss` 파일을 생성하여 바로 import해 사용합니다.

```ts
import './styles/main.scss';
```

### Plain CSS

별도 설치 없이 `.css` 파일을 생성하여 사용합니다.

## 새 페이지 추가

1. `src/pages/` 에 페이지 컴포넌트 생성
2. `src/router.tsx` 에 라우트 등록

```tsx
// src/pages/AboutPage.tsx
const AboutPage = () => <h1>About</h1>;
export default AboutPage;

// src/router.tsx
import AboutPage from '@/pages/AboutPage';

{ path: 'about', element: <AboutPage /> }
```

## API 사용 예시

```ts
// src/api/posts.ts
import apiClient from '@/api/client';
import type { ApiResponse } from '@/types';

export const getPosts = () =>
    apiClient.get<ApiResponse<Post[]>>('/posts').then((res) => res.data);

// 컴포넌트에서 사용
import { useQuery } from '@tanstack/react-query';
import { getPosts } from '@/api/posts';

const { data, isLoading } = useQuery({
    queryKey: ['posts'],
    queryFn: getPosts,
});
```

## Zustand 스토어 추가

```ts
// src/stores/useUserStore.ts
import { create } from 'zustand';

interface UserState {
    user: User | null;
    setUser: (user: User | null) => void;
}

const useUserStore = create<UserState>((set) => ({
    user: null,
    setUser: (user) => set({ user }),
}));

export default useUserStore;
```

## Claude Code 플러그인

이 프로젝트에는 아래 Claude Code 플러그인이 기본 포함되어 있습니다. [Claude Code](https://claude.ai/code)에서 프로젝트를 열면 자동으로 활성화됩니다.

| 플러그인 | 용도 |
|---------|------|
| superpowers | 브레인스토밍, 플래닝, TDD 등 Claude Code 워크플로우 스킬 |
| context7 | 라이브러리/프레임워크 최신 문서 자동 참조 |
| playwright | 브라우저 자동화 및 UI 테스트 |

## MCP 설정

Figma 연동이 필요한 경우 `figma-mcp/figma-mcp-setup.md`를 참조하세요.

- **figma** (공식 Remote MCP): 디자인 읽기/캡처/생성
- **figma-rest-api** (커스텀 로컬 MCP): 댓글, 컴포넌트, 스타일 등 REST API
