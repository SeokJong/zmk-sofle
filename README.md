# Sofle 키보드 펌웨어

ZMK 기반 Eyelash Sofle 분리형 키보드 펌웨어입니다.

## 업데이트 내역

- **2025/08/22**
  1. 소프트 오프(Soft Off) 기능 추가. Q, S, Z 키를 동시에 2초간 누르면 키보드가 딥 슬립 상태로 진입합니다. 이 상태에서는 키를 눌러도 깨어나지 않습니다. 외출 시 유용하며, 리셋 스위치를 한 번 누르면 다시 활성화됩니다.
  2. 우측 키보드 화면의 GIF 애니메이션 제거로 전력 소비가 크게 감소했습니다.

- **2025/03/30**
  - 절전 모드 진입 시간을 1시간으로 증가
  - 디바운스 시간 추가
  - 절전 후 전력 소비 최적화

- **2024/12/21**
  - ZMK Studio 지원 추가 (왼손 키보드만 플래싱하면 사용 가능)

- **2024/10/24**
  1. 전원 공급 모드 수정으로 전력 소비 감소
  2. RGB 전원 자동 차단 기능 수정

> ⚠️ 2025년 8월 22일 이전에 업데이트한 경우, 최신 펌웨어로 업데이트하세요.

## 연락처

3D 프린팅 모델 파일이 필요하거나 키보드에 문제가 있으면 [380465425@qq.com](mailto:380465425@qq.com)으로 연락하세요.

## 키맵 레이아웃

![Sofle 키맵](keymap-drawer/eyelash_sofle.svg)

## 프로젝트 구조

```
zmk-sofle/
├── boards/arm/eyelash_sofle/    # 보드 정의 파일
│   ├── eyelash_sofle.keymap     # 기본 키맵 파일
│   ├── eyelash_sofle.dtsi       # 디바이스 트리 설정
│   ├── eyelash_sofle_left.dts   # 왼손 키보드 설정
│   └── eyelash_sofle_right.dts  # 오른손 키보드 설정
├── config/
│   ├── eyelash_sofle.conf       # ZMK 설정 파일
│   ├── eyelash_sofle.keymap     # 사용자 키맵 파일
│   ├── eyelash_sofle.json       # 키맵 JSON 설정
│   └── west.yml                 # West 매니페스트
├── keymap-drawer/               # 키맵 시각화 파일
├── .github/workflows/           # GitHub Actions 워크플로우
│   ├── build.yml                # 펌웨어 빌드 워크플로우
│   └── draw.yml                 # 키맵 그리기 워크플로우
└── zephyr/module.yml            # Zephyr 모듈 설정
```

## 주요 기능

### 레이어 구성
- **Layer 0**: 기본 QWERTY 레이어
- **Layer 1**: 기능키(F1-F12), 마우스 제어, RGB 설정
- **Layer 2**: 블루투스 설정, 시스템 제어
- **Layer 3-4**: 사용자 정의 레이어

### 하드웨어 기능
- **로터리 인코더**: 볼륨 조절 (Layer 0), 스크롤 (Layer 1-4)
- **RGB 언더글로우**: 시작 시 꺼짐, 최대 밝기 90%
- **마우스 포인팅**: 트랙패드/마우스 에뮬레이션 지원
- **백라이트**: 시작 시 켜짐, 밝기 100%

### 전원 관리
- 1시간 후 자동 절전 모드
- RGB 유휴 시 자동 꺼짐
- 소프트 오프 기능 (Q+S+Z 2초 유지)

## 빌드 방법

이 저장소는 GitHub Actions를 통해 자동으로 펌웨어를 빌드합니다.

1. 저장소를 포크합니다
2. `config/eyelash_sofle.keymap` 파일을 수정합니다
3. 변경사항을 푸시하면 자동으로 빌드가 시작됩니다
4. Actions 탭에서 빌드된 펌웨어를 다운로드합니다

### 빌드 산출물
- `eyelash_sofle_left-nice_view.uf2`: 왼손 키보드 (일반)
- `eyelash_sofle_studio_left-nice_view.uf2`: 왼손 키보드 (ZMK Studio 지원)
- `eyelash_sofle_right-nice_view.uf2`: 오른손 키보드
- `nice_nano_v2-settings_reset.uf2`: 설정 초기화용

## 키맵 수정

### 기본 키 변경
`config/eyelash_sofle.keymap` 파일에서 키 바인딩을 수정할 수 있습니다.

### ZMK Studio 사용
ZMK Studio가 활성화된 왼손 펌웨어를 사용하면 웹 UI를 통해 실시간으로 키맵을 변경할 수 있습니다.

## 블루투스 설정

| 키 조합 | 기능 |
|---------|------|
| `BT_SEL 0-4` | 블루투스 프로필 선택 |
| `BT_CLR` | 현재 프로필 페어링 초기화 |
| `BT_CLR_ALL` | 모든 프로필 초기화 |
| `OUT_USB` | USB 출력 모드 |
| `OUT_BLE` | 블루투스 출력 모드 |

## 문제 해결

### 키보드가 연결되지 않음
1. 설정 초기화 펌웨어 플래싱
2. 양쪽 키보드 재페어링

### 절전 모드에서 깨어나지 않음
- 소프트 오프 상태일 수 있습니다
- 리셋 스위치를 눌러 활성화하세요

## 라이선스

MIT License

---

원본 프로젝트: [ZMK Firmware](https://zmk.dev/)
