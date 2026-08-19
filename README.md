# Eversio Medical — 회사 홈페이지

`www.eversiomedical.com` 에 올릴 정적 사이트입니다. 빌드 도구 없이 파일 그대로 서빙됩니다.

```
index.html     전체 페이지 (HTML·CSS·JS·SVG 전부 이 파일 하나에 들어 있음)
favicon.svg    브라우저 탭 아이콘
CNAME          GitHub Pages 커스텀 도메인 설정 (www.eversiomedical.com)
.nojekyll      GitHub Pages의 Jekyll 처리 비활성화
```

## 로컬에서 확인하기

```bash
python -m http.server 8899
```

브라우저에서 `http://localhost:8899` 접속.

---

## GitHub Pages 배포

### 1. 저장소 만들기

GitHub에서 새 저장소를 만듭니다 (예: `eversio-web`). Public이어야 무료 Pages를 쓸 수 있습니다.

### 2. 파일 올리기

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<계정>/<저장소>.git
git push -u origin main
```

### 3. Pages 켜기

저장소 → **Settings → Pages** →
- Source: `Deploy from a branch`
- Branch: `main` / `/ (root)` → Save

### 4. 커스텀 도메인 연결

같은 화면의 **Custom domain** 에 `www.eversiomedical.com` 입력 후 Save.
(저장소에 `CNAME` 파일이 이미 있어서 자동으로 채워지기도 합니다.)

### 5. DNS 설정 — 도메인 등록업체 관리 페이지에서

| 타입 | 이름 | 값 |
|---|---|---|
| CNAME | `www` | `<계정>.github.io` |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

`www` 만 쓸 거면 CNAME 한 줄로 충분하고, A 레코드 4개는 `eversiomedical.com`(www 없이)으로 들어온 사람을 `www` 로 넘겨주기 위한 것입니다.

DNS 반영에 보통 10분~수 시간 걸립니다. 반영된 뒤 Settings → Pages 에서 **Enforce HTTPS** 를 체크하세요 (인증서 발급에 몇 분 더 걸립니다).

---

## 내용 수정하기

### 국문/영문 텍스트

거의 모든 문구가 `data-ko` / `data-en` 속성 쌍으로 되어 있습니다. 태그 안의 글자는 국문 기본값이고, JS가 선택된 언어에 맞춰 바꿔 끼웁니다.

```html
<h3 data-ko="무마찰 전개" data-en="Friction-free deployment">무마찰 전개</h3>
```

수정할 때는 **세 군데를 같이** 고쳐야 합니다: `data-ko`, `data-en`, 그리고 태그 사이의 기본 텍스트.

### 페이지 제목·검색 결과 설명

`index.html` 맨 아래 `<script>` 안의 `META` 객체를 고치면 됩니다.

### 채워 넣어야 할 항목

`class="tbd"` 로 표시된 자리는 점선 상자로 눈에 띄게 렌더링됩니다. 현재 남아 있는 것:

- **회사 › 법인 설립** — 법인 설립일 (또는 이 줄 자체를 삭제)

그 외 확인이 필요한 값:

- **팀원 영문 이름** — EN 모드에서 쓰이는 로마자 표기 (`Jeonghyeon Lim` / `Sukho Song` / `Jongsoo Lee`). 논문에 쓰는 표기와 다르면 고쳐야 합니다
- **아바타 이니셜** — EN 모드에서 `JL`, `SS`, `JL` 로 표시됩니다 (임정현·이종수가 겹침)

---

## 의도적으로 넣지 않은 것

IR 덱에는 있지만 공개 홈페이지에는 올리지 않은 항목입니다. 필요하면 말씀해 주세요.

- 매출 추정치, 확보 자금, 개당 판매가, 급여 등재 전략
- 인허가 2단계 단축 시나리오 (식약처 사전 상담 전이라 확정 표현을 피함)
- 경쟁사 실명 비교표 (업계 표준 vs 구조 중심 구도로 대체)
- 기술이전·협업 논의 중인 회사명

## 이미지에 대해

덱의 제품 렌더링과 스톡 사진은 쓰지 않았습니다. 렌더링은 다른 브랜드명(JEONGHYEON)이 박혀 있는 컨셉 이미지고, 스톡 사진은 상업 사이트 사용 라이선스를 확인할 수 없기 때문입니다. 대신 작동 원리 도해를 SVG로 새로 그렸습니다 — 확대해도 깨지지 않고, 국문/영문 라벨이 함께 전환됩니다.

실제 시제품 사진이 나오면 그걸 넣는 것이 가장 좋습니다.

## 법적 고지

푸터에 개발 단계·미승인 의료기기 고지가 들어 있습니다. 의료기기 광고 규정과 관련해 민감한 부분이니, 문구를 바꿀 때는 신중하게 확인하세요.
