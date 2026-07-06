# CPC 광고 운영보고서 자동 생성 웹앱

중국어 CPC 엑셀/CSV 데이터를 업로드하면 점주 전달용 2페이지 PDF 및 PNG 운영보고서를 생성하는 Streamlit 웹앱입니다. 여러 월이 포함된 단일 파일에서 가장 최근 월을 이번달, 직전 월을 전월 데이터로 자동 인식합니다.

## 설치 방법

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## 실행 방법

```bash
streamlit run app.py
```

브라우저에서 보통 `http://localhost:8501` 주소로 접속합니다.

## 엑셀 업로드 방법

1. `CPC 데이터 파일 업로드`에 여러 월 데이터가 포함된 파일 1개를 업로드합니다.
2. 매장명을 입력합니다.
3. 광고 중단일과 비고가 있으면 선택 입력합니다.
4. `보고서 생성` 버튼을 클릭합니다.

가장 최근 월은 이번달 보고서 데이터로 사용하고, 직전 월은 전월 대비 비교 분석에만 사용합니다. 직전 월 데이터가 없으면 전월 대비 섹션은 자동으로 숨겨집니다.

자동 매칭 예시:

- `曝光（次）` → `노출수`
- `点击（次）` → `클릭수`
- `花费（元）` → `소진비용(위안)`
- `平均点击价格（元）` → `클릭당 평균비용(위안)`
- `查看团购` → `상품권 조회수`
- `日期` → `날짜`

금액은 PDF와 이미지에서 모두 `위안`으로 표시됩니다.

## 보고서 구성

1페이지:

- 매장명
- 운영기간
- 핵심 성과지표
- 전월 대비 성과 비교
- 일별 노출수 추이
- 일별 클릭수 추이

2페이지:

- 일별 상세 데이터
- 이번 달 광고 운영 요약

전월 파일이 없으면 전월 대비 성과 비교 섹션은 자동으로 숨겨집니다.

## PDF 및 이미지 생성 방법

생성 완료 후 아래 버튼이 표시됩니다.

- `PDF 다운로드`
- `이미지(PNG) 다운로드`

파일명 형식:

```text
매장명_YYYY년MM월_CPC운영보고서.pdf
매장명_YYYY년MM월_CPC운영보고서.png
```

## 배포 방법

서버 또는 Streamlit Cloud에 아래 파일과 폴더를 함께 업로드합니다.

- `app.py`
- `requirements.txt`
- `README.md`
- `assets`

## Streamlit Cloud 배포 방법

1. GitHub 저장소를 만듭니다.
2. `app.py`, `requirements.txt`, `README.md`, `assets` 폴더를 업로드합니다.
3. [Streamlit Cloud](https://streamlit.io/cloud)에 로그인합니다.
4. `New app`을 클릭합니다.
5. GitHub 저장소와 브랜치를 선택합니다.
6. `Main file path`를 `app.py`로 설정합니다.
7. `Deploy`를 클릭합니다.

배포가 끝나면 `https://앱이름.streamlit.app` 형태의 웹사이트 URL이 생성됩니다.
