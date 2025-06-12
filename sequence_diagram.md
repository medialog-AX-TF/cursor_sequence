# 커서 AI 시퀀스 다이어그램

> **참고:** AI 엔진은 커서 에디터 내부(또는 확장/플러그인 형태)에서 동작하며, 커서와 긴밀하게 통합되어 있습니다. 사용자의 명령은 커서 내부의 AI 엔진으로 전달되어 해석·처리되고, 필요시 외부 LLM 및 MCP Tools와 통신하여 결과를 반환합니다.

아래는 커서 AI의 주요 동작 흐름을 나타내는 상세 시퀀스 다이어그램입니다.

```mermaid
sequenceDiagram
    participant User as "사용자"
    participant UI as "커서 에디터 UI"
    participant AI as "AI 엔진"
    participant LLM as "LLM(대형 언어 모델)"
    participant MCP as "MCP Tools"
    participant Codebase as "코드베이스"

    User->>UI: 명령 입력(자연어/코드)
    UI->>AI: 명령 전달 및 기본 컨텍스트 정보 제공
    Note right of UI: 컨텍스트 정보 예시\n- 현재 파일\n- 선택 영역\n- 커서 위치\n- 프로젝트 구조 등
    AI->>LLM: 명령 해석 및 의도 파악 요청
    LLM-->>AI: 해석 결과 및 의도 반환
    AI->>MCP: 코드 검색/파일 읽기/편집 등 도구 요청
    MCP->>Codebase: 실제 코드베이스에 접근(검색, 읽기, 편집 등)
    Codebase-->>MCP: 요청 결과 반환
    MCP-->>AI: 도구 실행 결과 반환
    AI->>LLM: 코드 생성/수정/설명 요청(필요시)
    LLM-->>AI: 생성/수정/설명 결과 반환
    AI->>UI: 최종 결과 반환
    UI->>User: 결과 표시 및 적용
``` 