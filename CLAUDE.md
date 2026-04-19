# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 필수 규칙

1. 질문이 모호할 시 억지로 답변하지 말고, 재질문을 통해 의도를 명확히 한 후 답변할 것.
2. 정보 제공 시 출처가 불분명하거나 출처 없이 답변하지 말 것.

작업 전 `.claude/docs/project-guide.md`를 참조할 것.

## 포함 모듈

### figma-mcp
Figma 연동을 위한 MCP 서버 설정 모음.
- `figma` (공식 Remote MCP): 디자인 읽기/캡처/생성
- `figma-rest-api` (커스텀 로컬 MCP): 댓글, 컴포넌트, 스타일 등 REST API

설정 방법: `figma-mcp/figma-mcp-setup.md` 참조.

### figma-plugin
Figma에 캡처된 텍스트 노드의 폰트를 **Pretendard로 일괄 변환**하는 로컬 플러그인.
`generate_figma_design`으로 Gothic A1 폰트로 캡처 후, 이 플러그인으로 Pretendard로 변환하는 워크플로우에서 사용.

생성/설치 방법: `figma-plugin/CLAUDE.md` 참조.

### converter
Figma에 커스텀 폰트(Pretendard)를 적용하기 위한 워크플로우 피드백 문서.
`use_figma`는 클라우드 전용이라 로컬 폰트 직접 적용 불가 → Gothic A1로 캡처 후 플러그인으로 변환하는 우회 방식을 정리.

상세 워크플로우: `converter/feedback_figma_custom_font.md` 참조.
