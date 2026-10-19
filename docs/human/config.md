# 설정과 다국어 설명 (.lxconfig)

LXIUM 런처는 모드 설정을 런처 화면에서 바꿀 수 있게 해 줍니다. 여러 언어로 설명을 보여 주고, 게임을 한 번도 실행하지 않았어도 설정을 바꿀 수 있습니다.
그러려면 모드가 아래 두 가지를 지키면 됩니다.

> 정확한 규칙은 AI용 문서 [`../ai/config.md`](../ai/config.md)와 LXIUM 규격 [lxconfig.md](https://github.com/LocalXtend/LXIUM/blob/dev/docs/human/lxconfig.md)에 있습니다.

## 1. 코드: 설명 없이 등록

```csharp
// BepInEx 6 플러그인
TargetFps = Config.Bind("FrameRate", "TargetFps", 0);
Quality = Config.Bind("Render", "Quality", QualityMode.Balanced);
ChangeOnly = Config.Bind("Render", "ChangeOnly", true);
```

설정 파일(`BepInEx/config/LXIUM_{{GAME_ID}}.cfg`)에는 설명을 달지 않습니다. 설명은 한 언어로만 쓸 수 있기 때문입니다.

## 2. .lxconfig: 형식·기본값·설명

저장소 루트의 `LXIUM_{{GAME_ID}}.lxconfig`에 적습니다. 빌드가 애드온 zip에 넣습니다.

```
Section FrameRate
Name FrameRate ko "프레임"
Set TargetFps Int 0 Range -1 360
Name TargetFps ko "목표 fps"
Name TargetFps en "Target FPS"
Lang TargetFps ko "0 = 모니터 주사율에 맞춤, -1 = 제한 없음"
Lang TargetFps en "0 = match the monitor, -1 = unlimited"

Section Render
Set Quality Enum Balanced Values Fast|Balanced|Original
Set ChangeOnly Bool true
```

| 줄 | 뜻 |
|---|---|
| `Section 이름` | 아래 설정들의 섹션 (코드의 Bind 첫 번째 값) |
| `Set 키 형식 기본값` | 설정 하나. 형식 `Bool` `Int` `Float` `String` `Enum` |
| `Range 최소 최대` | 숫자 범위 → 런처가 슬라이더로 보여 줌 |
| `Values a\|b\|c` | Enum 선택지 (C# enum 이름 그대로) |
| `Lang 키 언어 "설명"` | 언어별 설명 (`ko` `en` `ja` `zh-Hans` `zh-Hant`) |
| `Name 키 언어 "이름"` | 언어별 표시 이름. 섹션 이름을 쓰면 섹션 제목 |

## 지킬 것

- 코드의 섹션·키·기본값과 `.lxconfig`가 똑같아야 합니다. 설정을 바꾸면 두 곳을 같은 커밋에서 고칩니다.
- 최소 한국어(`ko`)와 영어(`en`) 설명·이름을 적습니다.
- 다른 섹션에 같은 키가 있으면 `섹션.키`로 적습니다.
