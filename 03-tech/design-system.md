# Design System Draft

## Status

Draft

## Prototype

`prototypes/design-system.html`

## Scope

Milestone 1 개발 전에 사용할 Theme 초안입니다.

Android, iOS, macOS 모두 하나의 DesignSystem을 공유합니다.

플랫폼별로 별도의 색상, typography, shape 체계를 만들지 않습니다. 플랫폼 차이는 navigation, window/sheet/modal 표현, 화면 폭에 따른 layout adaptation 수준에서만 처리합니다.

DesignSystem 모듈은 다음 foundation을 먼저 제공합니다.

- Color
- Typography
- Shape
- Spacing
- Elevation
- Basic components

## Font

앱의 기본 폰트는 Pretendard만 사용합니다.

```text
fontFamily = Pretendard
```

Compose 구현 시에도 DesignSystem의 typography token에서 Pretendard를 기본값으로 사용합니다.

## Platform Policy

하나의 DesignSystem을 모든 플랫폼에 적용합니다.

| Platform | DesignSystem | Allowed Adaptation |
| --- | --- | --- |
| Android | Shared | 화면 폭, system inset, modal/sheet 표현 |
| iOS | Shared | 화면 폭, safe area, modal/sheet 표현 |
| macOS | Shared | window layout, sidebar/detail layout |

금지:

- Android 전용 color palette
- iOS 전용 typography scale
- macOS 전용 shape scale
- 플랫폼별로 다른 의미를 가진 semantic token

허용:

- 같은 token을 사용한 반응형 layout
- 같은 component contract를 사용하는 플랫폼별 container
- compact/medium/expanded width에 따른 배치 변경

## Adaptive Layout Tokens

DesignSystem은 화면 폭에 따른 layout 기준을 제공합니다.

| Token | Range | Usage |
| --- | --- | --- |
| `Compact` | `< 600` | phone 중심, 단일 column |
| `Medium` | `600 - 899` | large phone, tablet compact |
| `Expanded` | `>= 900` | tablet, desktop, macOS window |

Milestone 1의 macOS prototype은 `Expanded` 기준입니다.

## Color Tokens

### Neutral

| Token | Value | Usage |
| --- | --- | --- |
| `Background` | `#F4F5F7` | 앱 외부 배경 |
| `Surface` | `#FFFFFF` | 기본 패널, 카드, modal |
| `SurfaceSoft` | `#F8FAFC` | 보조 패널, 비활성 배경 |
| `SurfaceRaised` | `#FBFCFE` | toolbar, modal header |
| `Line` | `#D9DEE8` | 기본 border |
| `LineStrong` | `#C4CCD8` | 강조 border |
| `TextPrimary` | `#172033` | 주요 텍스트 |
| `TextSecondary` | `#334155` | 보조 주요 텍스트 |
| `TextMuted` | `#687385` | 보조 설명 텍스트 |

### Semantic

| Token | Value | Usage |
| --- | --- | --- |
| `Primary` | `#2563EB` | 주요 액션, 선택 상태 |
| `PrimarySoft` | `#EAF1FF` | 선택 배경 |
| `Success` | `#0F8A63` | 완료, 성공 |
| `SuccessSoft` | `#E8F7F1` | 성공 배경 |
| `Warning` | `#B7791F` | 검토, 주의 |
| `WarningSoft` | `#FFF6DF` | 주의 배경 |
| `Danger` | `#D14343` | 삭제, 위험 액션 |
| `DangerSoft` | `#FFF0F0` | 위험 배경 |

## Typography Tokens

| Token | Size | Weight | Usage |
| --- | --- | --- | --- |
| `DisplaySmall` | 28 | 800 | 화면 제목 |
| `TitleLarge` | 22 | 800 | 상세 패널 제목 |
| `TitleMedium` | 18 | 800 | modal 제목 |
| `TitleSmall` | 15 | 750 | section 제목 |
| `BodyMedium` | 14 | 500 | 기본 본문 |
| `BodySmall` | 13 | 500 | 카드 메타, form label |
| `LabelMedium` | 13 | 750 | 버튼, label |
| `LabelSmall` | 12 | 700 | chip, 상태 |
| `Caption` | 11 | 650 | 보조 정보 |

## Shape Tokens

| Token | Value | Usage |
| --- | --- | --- |
| `None` | 0 | full bleed, reset |
| `Xs` | 4 | checkbox, small control |
| `Sm` | 6 | segmented item |
| `Md` | 7 | button, nav item |
| `Lg` | 8 | card, field, chip container |
| `Xl` | 12 | app window, modal |
| `Pill` | 999 | chip, status pill |

## Spacing Tokens

| Token | Value |
| --- | --- |
| `Space2` | 2 |
| `Space4` | 4 |
| `Space6` | 6 |
| `Space8` | 8 |
| `Space10` | 10 |
| `Space12` | 12 |
| `Space14` | 14 |
| `Space16` | 16 |
| `Space18` | 18 |
| `Space20` | 20 |
| `Space22` | 22 |
| `Space24` | 24 |
| `Space26` | 26 |
| `Space28` | 28 |
| `Space32` | 32 |

## Elevation Tokens

| Token | Value | Usage |
| --- | --- | --- |
| `Window` | `0 18px 55px rgba(26, 36, 58, 0.16)` | macOS window mockup |
| `Modal` | `0 28px 90px rgba(15, 23, 42, 0.28)` | modal |
| `Selected` | `0 8px 20px rgba(15, 23, 42, 0.12)` | swiped/raised task row |

## Component Defaults

### Button

- Height: 30 or 36
- Shape: `Md`
- Primary background: `Primary`
- Secondary background: `Surface`
- Destructive background: `Danger`

### Text Field

- Height: 38 for single line
- Shape: `Lg`
- Border: `LineStrong`
- Focus border: `Primary` soft outline

### Card

- Shape: `Lg`
- Background: `Surface`
- Border: `Line`
- Selected border: `Primary` soft border

### Modal

- Shape: `Xl`
- Background: `Surface`
- Header background: `SurfaceRaised`
- Elevation: `Modal`

### Task Row

- Height: at least 74
- Shape: `Lg`
- Selected state uses `PrimarySoft` and left accent line
- Swipe delete reveals `Danger` action on the right

## Compose Implementation Notes

DesignSystem 모듈은 최소 다음 객체를 제공합니다.

```text
NoteColors
NoteTypography
NoteShapes
NoteSpacing
NoteElevation
NoteBreakpoints
NoteTheme
```

기능 UI 모듈은 색상, 폰트, shape 값을 직접 정의하지 않고 DesignSystem token을 사용합니다.

## Compose Theme Shape

구현 시 Theme은 다음 구조를 권장합니다.

```text
NoteTheme(
  colors = NoteColors.light(),
  typography = NoteTypography.pretendard(),
  shapes = NoteShapes.default(),
  spacing = NoteSpacing.default(),
  elevation = NoteElevation.default(),
  content = content
)
```

Milestone 1에서는 light theme만 정의합니다.

Dark theme은 후속 마일스톤에서 검토합니다.
