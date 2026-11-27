# Wild Haven Idle — 와일드 헤이븐

[![Android CI](https://github.com/jeiel85/wild-haven-idle-android/actions/workflows/android.yml/badge.svg)](https://github.com/jeiel85/wild-haven-idle-android/actions/workflows/android.yml)
[![Release](https://img.shields.io/badge/GitHub%20Release-APK%20%2B%20AAB-31543d)](https://github.com/jeiel85/wild-haven-idle-android/releases/latest)

> **숲속 보호구역을 복원하고, 다친 야생동물을 돌보는 방치형 힐링 게임**

작은 야생동물 보호구역의 관리자가 되어 보호 포인트를 모으고, 구조 동물의 회복을 지원하며, 도감을 채워 나가는 Android 방치형 성장 시뮬레이션입니다.

Wild Haven Idle is a local-first Android idle simulation about restoring a wildlife sanctuary.

<p align="center">
  <img src="docs/assets/wild-haven-icon-source.png" alt="Wild Haven Idle app icon" width="220">
</p>

## 공개 링크

| 항목 | 링크 |
|---|---|
| GitHub Pages | <https://jeiel85.github.io/wild-haven-idle-android/> |
| 개인정보처리방침 | <https://jeiel85.github.io/wild-haven-idle-android/privacy.html> |
| 최신 GitHub Release | <https://github.com/jeiel85/wild-haven-idle-android/releases/latest> |
| 스토어 그래픽 자료 | [store-graphics](store-graphics/README.md) |

## 프로젝트 상태

| 항목 | 상태 |
|---|---|
| 개발 단계 | MVP 공개 빌드 개선 중 |
| 플랫폼 | Android |
| Application ID | `com.jeiel85.wildhavenidle` |
| 현재 버전 | `0.6.4` |
| 저장 방식 | 로컬 우선 |
| 권한/SDK 정책 | 네트워크, 로그인, 광고, 결제, 분석 SDK 없음 |
| CI | GitHub Actions |
| 릴리즈 산출물 | APK, AAB |
| Pages source | `main` 브랜치 `/docs` |

## 최신 버전 하이라이트

`v0.6.4`는 최신 리뉴얼 UI 진입점과 공개 자료를 다시 확인해 내려받아 검증하기 쉬운 패치 버전입니다.

- 앱 진입점이 리뉴얼 화면(`renew.MainActivity`)인지 AAB 내부 manifest 기준으로 재확인
- Google Play용 512px 아이콘, 기능 그래픽, 스크린샷 묶음 정리
- GitHub Release에 signed APK/AAB 자동 업로드
- Pages는 `/docs` 정적 사이트로 배포되며 Jekyll 변환을 우회

## 게임 소개

플레이어는 작은 보호구역의 관리자가 됩니다. 접속하지 않는 동안에도 보호 포인트가 쌓이고, 다시 돌아오면 오프라인 보상을 확인한 뒤 보호구역을 개선하거나 구조 동물의 회복 단계를 올릴 수 있습니다.

핵심 플레이 루프:

```text
앱 접속
→ 오프라인 보상 확인
→ 보호 포인트 수령
→ 회복 지원 또는 보호구역 개선
→ 신규 구조 동물/서식지 해금
→ 도감 업데이트
→ 다시 방치
```

## MVP 범위

| 기능 | MVP | 현재 상태 |
|---|---:|---|
| 보호 포인트 자동 생산 | 포함 | 완료 |
| 오프라인 보상 계산 | 포함 | 완료 |
| 구조 동물 5종 | 포함 | 완료 |
| 회복 단계 시스템 | 포함 | 완료 |
| 보호구역 레벨업 | 포함 | 완료 |
| 도감 화면 | 포함 | 완료 |
| 동물 회복 목록 | 포함 | 완료 |
| 로컬 저장 | 포함 | 완료 |
| 설정 화면 + 데이터 초기화 | 포함 | 완료 |
| 화면 간 이동 (Navigation) | 포함 | 완료 |
| 로그인/클라우드/서버 | 제외 | 제외 |
| 광고/결제/분석 SDK | 제외 | 제외 |
| 푸시 알림 | 제외 | 제외 |

## 핵심 시스템

### 보호 포인트

`carePoint`는 MVP의 기본 성장 재화입니다. 보호구역 레벨과 구조 동물의 회복 단계에 따라 초당 생산량이 증가합니다.

### 구조 동물

| ID | 이름 | 희귀도 | 기본 보너스 | 해금 조건 |
|---|---|---|---:|---|
| `rabbit_001` | 숲토끼 | COMMON | 0.2/sec | 최초 시작 |
| `fox_001` | 붉은여우 | COMMON | 0.5/sec | carePoint 300 보유 |
| `deer_001` | 어린 사슴 | UNCOMMON | 1.2/sec | 숲토끼 회복 단계 5 |
| `owl_001` | 밤부엉이 | UNCOMMON | 1.8/sec | 총 생산량 5/sec |
| `lynx_001` | 스라소니 | RARE | 3.5/sec | 보호 중 동물 4종 |

### 회복 단계

| 단계 | 명칭 | 의미 |
|---:|---|---|
| 1 | 구조 직후 | 보호구역에 막 도착한 상태 |
| 5 | 안정 | 기본적인 회복을 마친 상태 |
| 10 | 적응 | 서식지에 적응한 상태 |
| 20 | 보호 완료 | 보호구역에서 안정적으로 지내는 상태 |

## 기술 스택

| 영역 | 선택 |
|---|---|
| 언어 | Kotlin |
| UI | Jetpack Compose, Material 3 |
| 아키텍처 | MVVM 또는 MVI-lite |
| 비동기 | Kotlin Coroutines / Flow |
| 로컬 저장 | AndroidX DataStore |
| DI | 수동 DI 우선, 필요 시 Hilt 검토 |
| 빌드 | Gradle Kotlin DSL |
| 테스트 | JUnit |
| CI/CD | GitHub Actions |
| 최소 SDK | 26 |
| Target SDK | 36 |

## 저장소 구조

```text
app/
  src/main/java/com/jeiel85/wildhavenidle/
    core/           공통 시간, 포맷, 디자인 유틸
    data/           로컬 저장소와 데이터 모델
    domain/         밸런스 계산, 정의, 유스케이스
    presentation/   Compose 화면과 ViewModel
    navigation/     화면 전환 구조
docs/               기획, 기술, 밸런스, 아트, 윤리 정책 문서
.agent/             AI 에이전트 작업 상태와 의사결정 기록
.github/workflows/  Android CI와 release build workflow
```

## 빠른 시작

필수 환경:

- JDK 17 이상
- Android SDK Platform 36
- Android Build Tools 36.0.0
- Windows에서는 `gradlew.bat`, Linux/macOS/CI에서는 `./gradlew` 사용

로컬 SDK 경로가 자동 인식되지 않으면 저장소 루트의 `local.properties`에 개인 환경 경로를 설정합니다. 이 파일은 커밋하지 않습니다.

```properties
sdk.dir=C\:\\Users\\<you>\\AppData\\Local\\Android\\Sdk
```

검증:

```bash
./gradlew test
./gradlew assembleDebug
```

Windows PowerShell:

```powershell
.\gradlew.bat test
.\gradlew.bat assembleDebug
```

## 릴리즈 빌드

릴리즈 APK/AAB는 keystore를 저장소 밖에 보관하고, 로컬 환경 변수 또는 GitHub Actions Secrets로만 주입합니다.

필요한 환경 변수:

```text
ANDROID_RELEASE_KEYSTORE_PATH
ANDROID_RELEASE_KEYSTORE_PASSWORD
ANDROID_RELEASE_KEY_ALIAS
ANDROID_RELEASE_KEY_PASSWORD
```

로컬 release 빌드:

```bash
./gradlew assembleRelease bundleRelease
```

GitHub Actions에서는 다음 Secrets를 사용합니다.

```text
ANDROID_RELEASE_KEYSTORE_BASE64
ANDROID_RELEASE_KEYSTORE_PASSWORD
ANDROID_RELEASE_KEY_ALIAS
ANDROID_RELEASE_KEY_PASSWORD
```

현재 release workflow:

- `Android CI`: PR/main 검증, debug APK, signed release APK/AAB artifact 생성
- `Android Release`: 수동 실행 또는 `v*` 태그 푸시로 signed release artifact 생성
- `Play release`: `v*` 태그 푸시(또는 수동 실행)로 Play용 AAB를 빌드해 Play 테스트 트랙(현재 `alpha` = 비공개 테스트)에 올림

### Play 업로드

`v*` 태그 하나를 올리면 두 워크플로가 따로 돕니다. `Android Release`는 GitHub 릴리스(APK)만 만들고 Play에는 올리지 않으며, Play 업로드는 `Play release`만 합니다. 그래서 같은 태그로 Play에 두 번 올라가지 않습니다.

- `Play release`는 GitHub 환경 `play`에서 돌고, 이 환경은 jeiel85의 승인을 받아야 시작합니다(배포 정책: `main` 브랜치·`v*` 태그만). 서명 키(`ANDROID_RELEASE_*`)와 `PLAY_SERVICE_ACCOUNT_JSON`은 이 환경의 Secrets에 있습니다.
- 태그 `vX.Y.Z`는 `app/build.gradle.kts`의 `versionName`과 같아야 하고, `store-release-notes/vX.Y.Z.txt`(`<ko-KR>`·`<en-US>` 블록, 각 500자 이내)가 있어야 합니다. 둘 중 하나라도 어긋나면 빌드 전에 멈춥니다.
- 순서: 시험 → `bundleRelease` → 키스토어 인증서 SHA-256이 Play 업로드 키(`D6:75:4C:…:7C:A5`)와 같은지 확인 → 트랙 상태 조회 → 첫 트랙에 AAB 업로드(AAB 서명 지문·versionCode 재확인) → 나머지 트랙에 같은 versionCode 붙이기 → 트랙 상태 조회. 키스토어는 마지막에 지웁니다. 업로드 스크립트는 [tools/play-publish.ps1](tools/play-publish.ps1)(전역 `play-publish` 스킬의 복사본)입니다.
- Actions 화면에서 `Play release`를 수동 실행할 때 `dry_run`을 켜면 빌드·서명 확인·트랙 조회까지만 하고 올리지 않습니다.
- Play 업로드는 이 워크플로가 맡으므로, 로컬에서 `play-publish`로 같은 버전을 다시 올리거나 바탕화면 AAB를 Play Console에 손으로 올리지 않습니다. 같은 versionCode는 Play가 거부합니다. 워크플로가 실패했을 때만 원인을 고친 뒤 수동 실행으로 다시 올립니다.

## Play Store 준비 자료

스토어 등록에 필요한 공개 자료는 저장소에 함께 정리되어 있습니다.

| 자료 | 위치 |
|---|---|
| 앱 아이콘 512px | [store-graphics/icon-512.png](store-graphics/icon-512.png) |
| 기능 그래픽 1024×500 | [store-graphics/feature-graphic-1024x500.png](store-graphics/feature-graphic-1024x500.png) |
| 휴대전화 스크린샷 | [store-graphics/screenshots](store-graphics/screenshots/) |
| 현재 Play Console 업로드 묶음 | [store-graphics/play-console-current](store-graphics/play-console-current/) |
| 버전별 출시 노트 | [store-release-notes](store-release-notes/) |
| 개인정보처리방침 | [docs/privacy.html](docs/privacy.html) |

## 개발 원칙

Wild Haven Idle은 야생동물 보호구역 복원 게임입니다. 동물을 소유물처럼 다루거나 접속하지 않았다는 이유로 피해를 주는 구조를 만들지 않습니다.

MVP에서는 다음을 추가하지 않습니다.

- 네트워크 권한
- 로그인 또는 계정
- 클라우드 동기화
- 광고 SDK
- 결제 SDK
- 분석 SDK
- 푸시 알림
- 실제 기부 또는 현실 단체 연계 암시

자세한 정책은 [IP and Ethics](docs/IP_AND_ETHICS.md)를 확인하세요.

## 문서

| 문서 | 내용 |
|---|---|
| [AGENTS.md](AGENTS.md) | AI 코딩 에이전트 작업 규칙 |
| [GAME_DESIGN.md](docs/GAME_DESIGN.md) | 게임 기획과 MVP 범위 |
| [TECH_SPEC.md](docs/TECH_SPEC.md) | Android 기술 설계 |
| [BALANCE.md](docs/BALANCE.md) | 생산량, 비용, 해금 밸런스 |
| [ART_DIRECTION.md](docs/ART_DIRECTION.md) | 아트 방향과 금지 표현 |
| [ASSET_LICENSES.md](docs/ASSET_LICENSES.md) | 에셋 출처와 라이선스 기록 |
| [IP_AND_ETHICS.md](docs/IP_AND_ETHICS.md) | IP 안전성과 윤리 정책 |
| [ROADMAP.md](docs/ROADMAP.md) | 단계별 개발 계획 |
| [MIGRATION.md](docs/MIGRATION.md) | 저장 데이터 마이그레이션 정책 |

## 작업 흐름

1. `main`을 최신 상태로 동기화합니다.
2. 작업별 브랜치를 만듭니다.
3. 코드와 관련 문서를 함께 갱신합니다.
4. `./gradlew test`와 필요한 빌드를 실행합니다.
5. 변경 범위를 확인한 뒤 커밋합니다.
6. PR에서 GitHub Actions 결과를 확인합니다.

## 라이선스

코드 라이선스는 [LICENSE](LICENSE)를 확인하세요.

이미지, 아이콘, 사운드 등 에셋은 별도 출처와 사용 권한을 [ASSET_LICENSES.md](docs/ASSET_LICENSES.md)에 기록합니다.
