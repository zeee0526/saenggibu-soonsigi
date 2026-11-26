# 소스 수정과 빌드

이 폴더는 생기부 쓰는 순식이 **v0.4.2-beta**의 수정 가능한 개발 소스입니다. 배포용 EXE·로컬 실행 ZIP과 용도가 다릅니다. 이용 조건은 프로젝트 루트의 LICENSE.md를 확인하세요. 개인 수정과 무료 재배포를 허용하며, 수정본은 원저작자의 공식 배포본으로 오인되지 않도록 표시해야 합니다.

## 1. 소스에 포함한 것

- 화면·기능 코드, 기본 프롬프트 7개와 입력·검토 지침
- 공식 기재요령 PDF·요약 프리셋, 글꼴과 각 이용 조건
- MCP 연결 코드, 로컬 저장 코드, Windows 설치기 소스
- 자동 테스트, 의존성 잠금 파일, 사용자 설명서와 안내 그림

학생 입력·개인 설정·첨부 자료·로그·백업·인증 정보·원래 컴퓨터의 호스팅 설정·node_modules·빌드 캐시는 포함하지 않습니다. work와 data는 실행 후 필요한 때 생성됩니다. 생성 가능한 lib/widget-html.ts도 제외하며 아래 명령으로 다시 만듭니다.

## 2. 개발 환경 준비

Node.js **22.18 이상**과 pnpm이 필요합니다. 이 프로젝트의 packageManager는 **pnpm 11.25.0**으로 지정되어 있습니다. 개발용 소스의 최초 의존성 설치에는 인터넷이 필요합니다. 다른 운영체제의 node_modules를 복사해서 사용하지 마세요.

터미널에서 package.json이 있는 이 폴더로 이동한 뒤 실행합니다.

```text
pnpm install --frozen-lockfile
pnpm build:widget
pnpm typecheck
pnpm test
pnpm lint
```

pnpm build:widget은 app/widget-entry.tsx와 전체 화면·글꼴을 묶어 lib/widget-html.ts를 만듭니다. 테스트는 먼저 임시 work 폴더를 준비합니다. 테스트가 쓰는 가상 자료는 작업용 폴더에 생성되며 GitHub에 커밋하지 않습니다.

## 3. 로컬 화면 실행

```text
pnpm dev
```

브라우저에서 http://127.0.0.1:5173 을 엽니다. 종료할 때는 실행 중인 터미널에서 Ctrl+C를 누릅니다. 브라우저는 화면 입력·편집용이며, GPT 처리에는 지원되는 Work·Codex의 MCP 연결이 별도로 필요합니다. 웹 화면을 실행한 것만으로 GPT까지 연결됐다고 판단하지 마세요.

독립된 임시 저장 폴더로 테스트하려면 실행 전에 환경변수 SAENGGIBU_DATA_DIR을 지정할 수 있습니다. 예를 들어 PowerShell에서는 다음과 같이 합니다.

```powershell
$env:SAENGGIBU_DATA_DIR = Join-Path (Get-Location) 'work/dev-data'
pnpm dev
```

.env.example은 옵션 설명이며 값은 비어 있습니다. 실행 코드가 .env 파일을 자동으로 읽는다는 뜻은 아닙니다. 별도의 AI API 키는 사용하지 않습니다.

## 4. 어떤 파일을 수정하나요?

| 변경하려는 것 | 주요 파일 |
| --- | --- |
| 전체 화면·작성/첨삭 이동·설정 | app/studio.tsx |
| 한 명 작성·여러 학생 작성 | app/single-student-pane.tsx, app/batch-pane.tsx |
| 첨삭 입력·결과 | app/proofreading-pane.tsx, app/proofreading-result.tsx |
| 디자인·색상·글씨 | app/globals.css, lib/themes.ts, lib/preferences.ts |
| 기본 프롬프트·교사 문체 | lib/area-prompts.ts, lib/writing-style.ts |
| 고정 입력 순서·첨삭 지침 | lib/prompt-input.ts, lib/proofreading-workflow.ts |
| 학교급·기록 영역·기재요령 | lib/areas.ts, lib/school-records.ts, lib/official-guide.ts |
| 자료 판독·저장·MCP 도구 | lib/files.ts, lib/service.ts, lib/mcp.ts |
| 저장 폴더·설치·배포 | scripts/storage-location.mjs, scripts/windows-installer/, scripts/package-plugin.mjs |

설치된 프로그램에서 프롬프트만 바꾸려면 개발 환경 없이 설정의 프롬프트 편집을 사용해도 됩니다.

## 5. 수정한 플러그인 만들기

화면 코드를 바꾼 뒤 MCP에서 테스트할 때는 pnpm build:widget으로 화면 묶음을 다시 만듭니다. 소스의 MCP 명령은 다음과 같습니다.

```text
pnpm mcp
```

MCP는 JSON-RPC를 처리하는 연결용 프로세스이며, 이 명령만으로 데스크톱 플러그인 목록에 자동 등록하는 것은 아닙니다. 사용자 테스트용 설치본을 만들려면 다음 절차를 사용합니다.

```text
pnpm package:plugin --output-dir ./work/release
pnpm package:windows --output-dir ./work/release
```

첫 명령은 로컬 플러그인 ZIP을, 둘째 명령은 그 ZIP을 포함한 Windows 설치 EXE를 만듭니다. Windows x64 설치기 빌드는 Windows x64 컴퓨터와 scripts/windows-installer/build.mjs가 사용하는 .NET Framework C# 컴파일러가 필요합니다. Node.js 및 PDF·이미지 판독 도구를 설치 EXE에 포함하므로 빌드하는 Node의 플랫폼도 확인하세요.

웹용 개발·프로덕션 빌드는 pnpm build와 pnpm start를 사용합니다. GPT의 실제 연결·판독·작성 품질은 Work·Codex에서 별도로 확인해야 합니다.

## 6. 공개용으로 정리한 부분

원래 개발 폴더의 로컬 호스팅 설정과 캐시를 제외하고, next-env.d.ts에서 이전 캐시 경로를 제거했습니다. 테스트 실행 전 빈 work 폴더를 준비하는 단계를 추가했습니다. 앱의 입력·작성·첨삭·프롬프트 동작은 그대로 유지합니다. 배포용 widget-html.ts는 소스로부터 재생성합니다.

새 코드를 GitHub에 올릴 때 data, work, node_modules, .env와 로컬 설정 폴더가 포함되지 않았는지 확인하세요. .gitignore에 이 제외 규칙을 포함했습니다. 직접 웹 업로드하는 경우에도 같은 폴더를 올리지 않습니다.
