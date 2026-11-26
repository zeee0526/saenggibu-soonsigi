# GitHub에 소스 올리기

## 설치 파일과 소스 파일을 구분하세요

- soonsigi-setup-0.4.2-beta-win-x64.exe: 일반 사용자 설치용. Releases에 첨부합니다.
- soonsigi-0.4.2-beta-source.zip: 화면·기능까지 수정할 수 있는 소스입니다. Releases에 그대로 첨부하면 누구나 소스를 내려받아 수정할 수 있습니다.
- GitHub의 Code 탭에서도 코드를 읽고 수정 제안을 받으려면 이 소스 ZIP을 압축 해제해 안의 파일·폴더를 저장소에 올립니다.

## 브라우저에서 올리기

1. ZIP을 압축 해제하고 soonsigi-0.4.2-beta-source 폴더를 엽니다.
2. GitHub 저장소의 첫 화면에서 Add file → Upload files를 누릅니다.
3. 먼저 README.md, LICENSE.md, package.json 등 최상위 파일들을 올립니다. Windows 탐색기에서 숨김 항목을 켜면 .gitignore, .npmrc, .env.example도 볼 수 있습니다. 여기의 .env.example 값은 비어 있는 설명용 예시입니다.
4. 다음으로 app, lib, components, hooks, scripts, tests, public, presets, skills, docs 폴더를 차례로 올립니다. 각각 저장소 첫 화면에서 드래그하면 폴더 구조가 유지됩니다.
5. 변경 설명을 쓰고 Commit changes 또는 화면에 표시된 변경 저장 버튼을 누릅니다.

브라우저 업로드는 한 번에 최대 100개 파일이므로 모든 폴더를 한꺼번에 넣지 말고 나눠 올립니다. 이 소스는 각 최상위 폴더가 100개 미만이므로 폴더별로 올릴 수 있습니다. GitHub Desktop이나 Git을 사용한다면 한 번에 커밋할 수도 있습니다.

같은 위치에 같은 이름이 있으면 새 내용으로 교체합니다. 이미 올린 README·docs도 이번 소스에 든 파일로 맞추면 개발 안내 링크까지 연결됩니다. ZIP의 바깥 폴더 자체를 올리지 말고 그 안의 내용물을 저장소 최상위에 놓으세요.

GitHub 파일 업로드 안내: https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository

## 공개 범위

학생 자료·개인 설정·개인 백업·개인 인증 정보는 포함하지 않았습니다. 공식 기재요령 PDF·기본 프롬프트·글꼴과 이용 조건은 포함했습니다. 개발 의존성과 실행 후 만든 data·work 폴더는 추가로 올리지 않습니다.

소스를 공개해도 LICENSE.md의 개인 수정·무료 배포 허용, 유료 판매·배포 금지 조건은 그대로 적용됩니다. 수정·실행·테스트·EXE 빌드 방법은 DEVELOPMENT.md에 정리했습니다.
