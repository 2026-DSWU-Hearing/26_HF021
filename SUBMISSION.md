# 한이음 공모전 제출 소스 통합 기록

2026-10-19 기준, 아래 원본 브랜치의 최신 커밋에서 추적 중인 파일만 복사했습니다. 원본 저장소에는 쓰기 작업을 수행하지 않았으며, 원본 Git 이력과 `.git` 메타데이터는 포함하지 않았습니다. 기존 루트 `README.md`는 그대로 보존했습니다.

| 제출 폴더 | 원본 저장소 | 브랜치 | 원본 커밋 | 복사 파일 수 |
| --- | --- | --- | --- | ---: |
| `frontend/` | `2026-DSWU-Hearing/HEARING-FE` | `main` | [`86b843d702a7`](https://github.com/2026-DSWU-Hearing/HEARING-FE/commit/86b843d702a7e468e21f6748b9c07a2cd9d66cb9) | 420 |
| `backend/` | `2026-DSWU-Hearing/HEARING-BE` | `dev` | [`abde76d66eb8`](https://github.com/2026-DSWU-Hearing/HEARING-BE/commit/abde76d66eb82a0be93a6290c4c5ded8c3448b5b) | 130 |
| `ai/` | `2026-DSWU-Hearing/HEARING-MODEL` | `main` | [`777df6cadf33`](https://github.com/2026-DSWU-Hearing/HEARING-MODEL/commit/777df6cadf334571a81d654e9a96abd3d31d0b3f) | 23 |
| `hardware/` | `2026-DSWU-Hearing/HEARING-HW` | `develop` | [`bad9ffcced19`](https://github.com/2026-DSWU-Hearing/HEARING-HW/commit/bad9ffcced19ada26f58041b02ab2848763eebe7) | 39 |
| `dashboard/` | `2026-DSWU-Hearing/HEARING-DASHBOARD` | `main` | [`23fa7bc26be1`](https://github.com/2026-DSWU-Hearing/HEARING-DASHBOARD/commit/23fa7bc26be1746281e3db4c0bfd3bceea79ee29) | 107 |

복사한 소스·설정·문서·에셋은 총 **719개**입니다. 이 중 715개는 원본과 SHA-256이 같으며, 아래 4개만 API 키 제거와 설정 지원을 위해 제출본에서 수정했습니다. 추가한 루트 파일은 `.gitignore`와 이 문서 2개입니다.

## 제출본의 API 키 제거

- `frontend/src/shared/firebase/settingFCM.ts`: 하드코딩된 Firebase 웹 API 키를 `VITE_FIREBASE_API_KEY`로 대체하고, 동일한 공개 웹 키를 서비스 워커 등록 URL에 전달합니다.
- `frontend/public/firebase-messaging-sw.js`: 하드코딩된 API 키 대신 등록 URL의 `apiKey` 파라미터를 읽습니다.
- `frontend/example.env`: 실제 값이 없는 `VITE_FIREBASE_API_KEY=` 예시를 추가했습니다.
- `frontend/src/vite-env.d.ts`: 추가 환경변수의 타입을 선언했습니다.

실행 시 `frontend/example.env`를 로컬 `.env`로 복사하고 Firebase 웹 API 키와 나머지 필수 설정을 입력하세요. 이 키는 웹 클라이언트용이며 브라우저에 노출됩니다. 서버 비밀키나 서비스 계정 키를 입력하면 안 됩니다. FCM은 별도 Firebase 설정과 VAPID 공개키가 필요합니다. 실제 `.env`와 개인 인증정보는 제출하지 않습니다.

나머지 각 폴더의 실행 방법은 해당 원본 README 및 설정 예시를 따릅니다. 하드웨어는 `hardware/src/secrets_example.h`를 로컬 `secrets.h`로 복사해 설정합니다. 의존성 파일, 잠금 파일, Docker·배포 설정, 펌웨어 모델 데이터 및 런타임 3D·이미지 에셋은 유지했습니다.

## 실제 제외 파일

추적 파일 733개 중 다음 14개를 제외했습니다.
- `HEARING-FE/.claude/settings.local.json` — Machine-local tool settings
- `HEARING-MODEL/app/__pycache__/__init__.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/__pycache__/main.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/api/__pycache__/__init__.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/api/__pycache__/audio.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/core/__pycache__/__init__.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/core/__pycache__/config.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/core/__pycache__/direction.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/data/__pycache__/__init__.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/data/__pycache__/category_map.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/services/__pycache__/__init__.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/services/__pycache__/backend_client.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/app/services/__pycache__/classifier.cpython-311.pyc` — Python bytecode/cache
- `HEARING-MODEL/desktop.ini` — OS metadata

원본별 `.git` 디렉터리는 복사하지 않았습니다. 실제 `.env`, 인증서·개인키, `node_modules`, `.venv`, 빌드 디렉터리는 원본 추적 파일 목록에 없었고 제출본에도 포함하지 않았습니다. 루트 `.gitignore`에 민감정보·의존성·캐시·산출물 제외 규칙과 설정 예시 허용 규칙을 추가했습니다.

## 검증 결과

- 5개 원본 지정 브랜치의 원격 최신 SHA와 복사 기준 SHA가 일치하며, 원본 체크아웃의 추적 파일 변경이 없음을 확인했습니다.
- 719개 파일의 누락 여부와 원본 해시를 검사하고, 기존 루트 README의 SHA-256 보존을 확인했습니다.
- Gitleaks 8.24.3으로 제출 파일 전체를 검사했습니다. 원본에 있던 API 키 2곳을 제거한 뒤 추가 탐지가 없었습니다. UTF-16 파일 2개는 별도 디코딩하여 재검사했습니다. 제거한 실제 API 키 값이 모든 제출 파일에 없는지도 확인했습니다.
- 변경된 프런트엔드의 잠금 파일 고정 설치와 프로덕션 빌드(`tsc -b && vite build`)가 통과했습니다. 번들 크기 경고가 있었지만 빌드는 성공했습니다.
- 모의 Firebase SDK로 환경변수 → 앱 → 서비스 워커의 키 전달, FCM 등록, 백그라운드 알림 동작을 검사했습니다. 실제 FCM 전송이나 전체 서비스 연동 시험은 수행하지 않았습니다.
- 빌드 검증은 제출 저장소 밖의 임시 복사본에서 수행했습니다. 설치 의존성과 빌드 산출물은 제출 파일에 포함하지 않았습니다.
- 서브모듈, 심볼릭 링크, 미해결 Git LFS 포인터, 압축 아카이브가 없는지 확인했습니다.

자동 검사와 파일 검토는 알려진 패턴을 기준으로 수행했습니다. 백엔드·AI·하드웨어·대시보드의 전체 실행 및 배포 검증은 이번 소스 통합 작업의 검증 범위에 포함하지 않았습니다.
