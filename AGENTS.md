<!--
템플릿 사용법
1. 이 저장소(https://github.com/LocalXtend/LXIUM_sample)를 복사해 새 저장소 LXIUM_<게임 id>를 만들고,
   LXIUM 저장소의 `optimizeMods/LXIUM_<게임 id>/`에 clone합니다.
2. 모든 파일의 {{GAME_NAME}}을 게임 이름(예: 마법소녀의 마녀재판)으로, {{GAME_ID}}를 게임 id(예: manosaba)로 바꿉니다.
   게임 id 규칙: 영문 소문자·숫자·`-`만 사용 (LXIUM 저장소 docs/ai/addon.md 3장 `game.id`)
3. 파일 이름을 바꿉니다: `LXIUM_sample.lxconfig` → `LXIUM_<게임 id>.lxconfig`, `docs/*/game.md` → `docs/*/<게임 id>.md`
4. `lxium.json`의 game.exe·steamAppId·variants를 채웁니다. 아이콘 `addon.png`(256x256)를 저장소 루트에 둡니다.
5. README.md를 아래 "Readme 작성법"대로 다시 씁니다.
6. 이 주석을 지웁니다.
-->
## 에이전트 개요
{{GAME_NAME}} 최적화 프로젝트 LXIUM_{{GAME_ID}}, 최적화와 모드 호환성을 동시에 지키는 것이 목적.

## 프로젝트 설명
LXIUM 프로젝트라는 최적화 게임 프로젝트의 일부분입니다.
{{GAME_NAME}} 최적화 프로젝트 LXIUM_{{GAME_ID}}

ver.txt에 버전을 작성합니다.

## 애드온 구조 (필수)
이 프로젝트의 결과물은 LXIUM 런처가 설치·제거하는 애드온 패키지입니다.
- 규격: LXIUM 저장소의 `docs/ai/addon.md` (https://github.com/LocalXtend/LXIUM/blob/dev/docs/ai/addon.md. LXIUM 저장소의 `optimizeMods/` 안에 clone했으면 `../../docs/ai/addon.md`). 빌드·패키징 작업 전에 반드시 읽고 따릅니다.
- 이 프로젝트의 값: `id` = `LXIUM_{{GAME_ID}}`, `game.id` = `{{GAME_ID}}`.
- 저장소 루트: `lxium.json`(원본), `addon.png`(아이콘), `LXIUM_{{GAME_ID}}.lxconfig`(설정 설명). 빌드가 셋 다 zip 루트에 넣음.
- 규격으로 해결되지 않는 것이 있으면 임의로 확장하지 말고 규격 수정을 먼저 제안합니다.

## 설정 (다국어)
- 설정은 로더의 설정 기능으로 만들고(BepInEx `Config.Bind(섹션, 키, 기본값)`), 설정 파일에는 설명을 쓰지 않습니다.
- 형식·기본값·범위·언어별 설명은 `LXIUM_{{GAME_ID}}.lxconfig`에 둡니다. 규격: LXIUM `docs/ai/lxconfig.md`, 이 저장소 안내: `docs/ai/config.md`.
- 설정 항목을 더하거나 바꾸면 같은 커밋에서 `.lxconfig`도 고칩니다. 최소 `ko`·`en` 설명과 이름을 둡니다.

## 문서
- `docs/human/`은 사람용, `docs/ai/`는 AI용 문서입니다. 같은 주제는 같은 파일 이름으로 양쪽에 두고, 한쪽을 고치면 다른 쪽도 같은 커밋에서 고칩니다.
- `{{GAME_ID}}.md`: 게임 분석 (엔진·백엔드·구조·무거운 곳과 근거)
- `config.md`: 설정과 `.lxconfig` 쓰는 법

## 코드 작성법
- 생각을 위한 주석이 아닌 코드를 설명하는 주석을 작성하세요.
- 공개 저장소의 일부이므로 비밀값, 이 PC의 경로(`C:\Users\...`), 개인 정보를 코드에 넣지 않습니다.

## 버전 관리

버전은 x.y.z형태로 작성합니다. 
x: 프로젝트에 뿌리 자체가 변경되어 많은 변화가 예상될 때
(예시: 언어 변경(c++ -> c#), 새로운 전환 업데이트(지금까지 이것과 관련한 것만 있었는데 더 확장된 기능을 담당하거나) 같은)
y: 프로젝트에 새로운 기능이 생겼을 때 (기능 확장과 새로운 기능에 근본적인 차이는 새로운 기능은 그 배이스를 바탕이자만, 기능 확장은 새로운 배이스와 라이브러리를 별도 제작하는 경우)
z: 프로젝트에 오류나 원래 있던 기능이 달라졌을 때

## git 관리
git은 dev 브렌치를 사용합니다.
기본적으로 git 행위를 지속적으로 업데이트합니다.
항상 코드 수정을 할 때마다 git을 합니다.

git 저장소는 이 프로젝트 전용입니다 (LXIUM_{{GAME_ID}}). 런처·규격 문서가 있는 LXIUM 저장소와 따로 커밋합니다.
로컬에서는 LXIUM 저장소의 `optimizeMods/LXIUM_{{GAME_ID}}/`에 clone해 둡니다. LXIUM 저장소는 `optimizeMods/`를 git에서 제외합니다.
릴리즈 태그·제목은 `<id>-v<버전>` 형식이고, 태그는 그 버전 커밋에 둡니다 (런처가 태그의 `lxium.json`·`addon.png`를 읽음).
릴리즈에는 `dist/<id>-<버전>.zip`을 올리고, 본문은 LXIUM 저장소 AGENTS.md의 "git 릴리즈에 관해서" 형식을 따릅니다.
이 저장소가 애드온 모음(catalog.json)에 등록되어 있으면 런처가 새 릴리스를 알아서 찾습니다. 처음 한 번만 모음에 저장소를 등록합니다 (LXIUM `docs/ai/catalog.md`).

## Readme 작성법
이 저장소의 README.md는 아래 내용을 그대로 씁니다. 버전 줄만 바꿉니다.
(현재 = 방금 릴리즈한 버전)
```
# LXIUM_{{GAME_ID}}

{{GAME_NAME}} 게임의 최적화를 진행합니다.
또한 모드 호환성을 지켜냅니다.

## 버전
> 현재: `n.m.k`

- 2026 ⓒ iyu.e — https://iyu-e.tistory.com/
```
