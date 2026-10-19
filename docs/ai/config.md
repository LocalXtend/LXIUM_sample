# 설정과 .lxconfig (AI용)

- 사람용 문서: `../human/config.md`
- 규격: LXIUM `docs/ai/lxconfig.md` (https://github.com/LocalXtend/LXIUM/blob/dev/docs/ai/lxconfig.md). 이 문서는 이 모드 프로젝트에서 지킬 것만 다룸

## 규칙

1. 설정 등록은 로더 기능으로, 설명 없이
   - BepInEx: `Config.Bind(섹션, 키, 기본값)` (description 인자 없음). 플러그인 GUID = `LXIUM_{{GAME_ID}}` → `BepInEx/config/LXIUM_{{GAME_ID}}.cfg`
   - MelonLoader: `MelonPreferences.CreateCategory(섹션)`, `category.SetFilePath("UserData/LXIUM_{{GAME_ID}}.cfg")`, `CreateEntry(키, 기본값)`
2. 저장소 루트 `LXIUM_{{GAME_ID}}.lxconfig`에 모든 설정을 `Section`/`Set`으로 적음
   - 형식 대응: `bool` → `Bool`, `int` → `Int`, `float`·`double` → `Float`, `string` → `String`, C# enum → `Enum` + `Values`(enum 이름, `|` 구분)
   - 범위가 정해진 숫자는 `Range 최소 최대` (런처가 슬라이더와 저장 전 검사에 씀)
   - 기본값은 코드와 같은 값, 숫자는 `.` 소수점
3. 모든 설정·섹션에 최소 `ko`·`en`의 `Lang`(설명)·`Name`(표시 이름)
4. 다른 섹션에 같은 키가 있으면 `Name`·`Lang`에서 `섹션.키`로 적음
5. 코드의 설정 등록을 바꾸면 같은 커밋에서 .lxconfig도 고침
6. Release 빌드가 `.lxconfig`·`addon.png`를 zip 루트에 넣음 (LXIUM `docs/ai/addon.md` 2장)

## 확인

- [ ] .lxconfig의 섹션·키·기본값 = 코드의 등록 (빠진 것·남는 것 없음)
- [ ] 모든 항목에 `ko`·`en` 설명과 이름
- [ ] 게임을 실행하지 않은 상태에서 런처 모드 설정 창이 열리고, 저장하면 설정 파일이 생기며, 게임을 실행하면 그 값이 적용됨
