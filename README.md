# OBS 한국 시간·한국 지역 날씨 오버레이

OBS 장면에 한국 시간과 국내 여러 도시의 날씨를 표시하는 HTML 오버레이입니다. 투명 배경과 맑은 고딕 글꼴을 사용하며, 모든 디자인은 흰색과 검정색으로 제공됩니다.

- 시계 4가지와 날씨 7가지 디자인, 총 22개 HTML 파일
- 시계는 년·월·일과 24시간제 시·분·초를 매초 갱신
- 날씨는 지역명, 기온, 상태, 단색 아이콘을 표시하고 8초마다 도시를 전환
- OBS에서 로컬 파일로 사용 가능. 시계는 오프라인에서도 동작하고 날씨는 인터넷 연결 필요

## 미리보기

[공개 미리보기 열기](https://vrc-yuram.github.io/obs-clock-weather/)

저장소를 ZIP으로 내려받아 압축을 푼 뒤 [index.html](index.html)을 브라우저에서 열면, 모든 디자인을 흰색과 검정색으로 나란히 비교할 수 있습니다. 미리보기에는 예시 값이 표시됩니다.

GitHub Pages를 켜둔 경우 저장소의 **Settings → Pages**에서 공개 미리보기 주소를 확인할 수 있습니다.

## OBS에 추가하기

1. 미리보기에서 원하는 디자인 아래의 **흰색 HTML** 또는 **검정색 HTML**을 눌러 저장합니다.
2. OBS에서 **소스 → + → 브라우저**를 선택합니다.
3. **로컬 파일**을 체크하고 내려받은 HTML을 지정합니다.
4. 아래 표에 있는 **너비 × 높이**를 입력하고, 장면에서 위치와 크기를 조절합니다.
5. 시계와 날씨를 함께 쓰려면 브라우저 소스를 두 개 만들어 각각 추가합니다.

GitHub Pages로 공개했다면 로컬 파일 대신 Pages에 게시된 개별 HTML의 주소를 브라우저 소스의 **URL**에 넣을 수도 있습니다. 예를 들어 공개 미리보기 주소가 `https://사용자명.github.io/저장소명/`이면, 뒤에 `obs-clock-date-rounded-white.html`을 붙입니다.

## 시계 디자인

| 디자인 | OBS 권장 크기 | 색상 |
|---|---:|---|
| 한 줄형 | 460 × 64 | [흰색](obs-clock-date-inline-white.html) · [검정색](obs-clock-date-inline-black.html) |
| 시간 강조형 | 290 × 114 | [흰색](obs-clock-date-stack-white.html) · [검정색](obs-clock-date-stack-black.html) |
| 날짜 강조형 | 340 × 92 | [흰색](obs-clock-date-date-focus-white.html) · [검정색](obs-clock-date-date-focus-black.html) |
| 둥근 테두리형 | 320 × 130 | [흰색](obs-clock-date-rounded-white.html) · [검정색](obs-clock-date-rounded-black.html) |

시계는 PC의 시스템 시간을 한국 시간대(`Asia/Seoul`)로 변환해 표시합니다. 시간이 어긋나면 Windows의 날짜 및 시간 동기화 설정을 확인하세요.

## 날씨 디자인

| 디자인 | OBS 권장 크기 | 색상 |
|---|---:|---|
| 둥근 테두리 · 한 줄 | 360 × 64 | [흰색](obs-weather-round-pill-white.html) · [검정색](obs-weather-round-pill-black.html) |
| 둥근 테두리 · 기온 강조 | 280 × 102 | [흰색](obs-weather-round-card-white.html) · [검정색](obs-weather-round-card-black.html) |
| 둥근 테두리 · 세로 | 220 × 154 | [흰색](obs-weather-round-stack-white.html) · [검정색](obs-weather-round-stack-black.html) |
| 가운데 · 한 줄 | 360 × 58 | [흰색](obs-weather-center-inline-white.html) · [검정색](obs-weather-center-inline-black.html) |
| 가운데 · 기온 강조 | 280 × 88 | [흰색](obs-weather-center-pair-white.html) · [검정색](obs-weather-center-pair-black.html) |
| 가운데 · 세로 | 210 × 132 | [흰색](obs-weather-center-stack-white.html) · [검정색](obs-weather-center-stack-black.html) |
| 미니멀 아이콘 | 300 × 89 | [흰색](obs-weather-minimal-white.html) · [검정색](obs-weather-minimal-black.html) |

기본 순서는 서울 → 인천 → 춘천 → 대전 → 광주 → 대구 → 부산 → 제주입니다. 날씨 데이터는 10분마다 갱신하며, 일시적으로 연결이 끊기면 마지막으로 받아온 값에 `이전 정보`를 표시합니다.

### 지역과 전환 효과 바꾸기

HTML을 메모장 같은 텍스트 편집기로 열고 `settings`와 `cities`를 수정합니다. 저장한 뒤 OBS 브라우저 소스를 새로고침하세요.

```js
const settings = { transition: "up", secondsPerCity: 8 };
const cities = [
  ["서울", 37.5665, 126.9780],
  ["부산", 35.1796, 129.0756],
];
```

| 설정 | 입력값 |
|---|---|
| `transition` | `"up"` 위로, `"down"` 아래로, `"none"` 즉시 전환 |
| `secondsPerCity` | 도시를 보여주는 시간(초) |
| `cities` | 도시명, 위도, 경도 순으로 입력. 도시 하나만 넣으면 그 도시를 고정 표시 |

### 날씨 데이터 출처

무료 Open-Meteo API는 비상업용입니다. 방송에서 날씨를 표시하면 방송 설명란 등 시청자가 확인할 수 있는 곳에 출처를 적어 주세요. [Open-Meteo 이용 조건](https://open-meteo.com/en/pricing)

> 날씨 데이터 제공: [Open-Meteo](https://open-meteo.com/) · [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). 기온을 정수로 반올림하고 날씨 코드를 한국어 상태와 아이콘으로 표시합니다.
