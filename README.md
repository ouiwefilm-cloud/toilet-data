# 🚽 toilet-data — 전국 공중화장실 좌표 데이터 (시도별 JSON)

전국 공중화장실 **46,080곳**의 이름·좌표·개방시간·주소·편의시설. 웹앱에서 `fetch`로 바로 사용 가능
(raw.githubusercontent.com·jsDelivr 모두 CORS 허용).

## 사용법

```
https://cdn.jsdelivr.net/gh/ouiwefilm-cloud/toilet-data@main/data/index.json   ← 시도별 건수/경계(bounds)
https://cdn.jsdelivr.net/gh/ouiwefilm-cloud/toilet-data@main/data/seoul.json   ← 시도별 데이터
```

시도 키: seoul busan daegu incheon gwangju daejeon ulsan gyeonggi gangwon chungbuk chungnam jeonbuk jeonnam gyeongbuk gyeongnam sejong jeju etc
(`etc` 는 시도를 알 수 없는 행용이며 지금은 빈 배열이다.)

## 스키마 (행 = 배열)

| idx | 내용 | 예 |
|---|---|---|
| 0 | 화장실명 | "창덕공원" |
| 1 | 위도(WGS84) | 37.57799 |
| 2 | 경도(WGS84) | 126.99219 |
| 3 | 플래그(비트합) | 1=24시간, 2=장애인, 4=기저귀교환대, 8=어린이용, 16=CCTV, 32=비상벨, **64=미개방(외부인 이용 불가)** |
| 4 | 개방시간 | 상세 시간이 있으면 그 값("09:00~18:00"), 없으면 "상시"/"불규칙"/"미개방"/"정보 없음" |
| 5 | 도로명(없으면 지번) 주소 | "서울특별시 종로구 …" |
| 6 | **[남아용, 여아용] 어린이 변기 수** (새로 추가) | [1, 0] |

6번 원소와 플래그 64는 2026-10-12 재구축에서 추가됐다. 앞의 6개 원소는 그대로라 기존 앱도 읽을 수 있다.
24시간(1)은 "상시"이거나 "24시간"·"00:00~24:00"일 때만 켜진다. "09:00~24:00"(자정 마감)은 24시간이 아니다.

## 출처·주의

- 원천: 행정안전부 **전국공중화장실표준데이터** (공공누리, data.go.kr/data/15012892), **데이터 기준일 2024-12-31**
  (CSV 53,585곳). 2026년 광주·전남 통합으로 바뀐 "전남광주통합특별시" 주소는 광주/전남 파일로 나눈다.
- 좌표: 2025-02 이후 원천 CSV 에 좌표가 없어 두 공공데이터에서 가져온다.
  1. **행정안전부 도로명주소 "위치정보요약DB"** (juso.go.kr, 2026-09 판)의 건물 출입구 좌표를 도로명 주소로 짝지음 → 40,682곳.
     가장 정확한 원천이다. 예전 좌표 중 수 km 이상 틀려 있던 약 1,000곳(섬 화장실이 육지에 찍힌 것 등)도 이걸로 바로잡혔다.
  2. 도로명으로 못 찾은 곳은 이전 판(좌표 포함 구버전 스냅샷의 공개 미러 daeillband2014-hub/toilet-map-korea)의
     좌표를 같은 주소에 재사용 → 6,954곳.
- **빠진 곳:** 약 5,900곳. 대부분 공식 데이터의 도로명 칸에 지번 주소만 적혀 있어 도로명 DB 로 찾을 수 없는 곳이다.
  도로명주소 "건물DB"(지번↔도로명 대응)를 더하면 더 채울 수 있다.
- **카카오·브이월드 지오코딩 결과는 넣지 않는다.** 두 서비스 모두 결과의 저장·재배포를 금지한다(실시간 호출만 허용).
- 재구축 스크립트: ouiwefilm-cloud/simple-md-reader 의 `scripts/toilet-data/rebuild.py`
- 공공데이터 원본 특성상 실제와 다를 수 있다.

## 지역별 건수

| 시도 | 건수 |
|---|---|
| busan | 2,489 |
| chungbuk | 1,829 |
| chungnam | 1,976 |
| daegu | 1,667 |
| daejeon | 1,450 |
| etc | 0 |
| gangwon | 3,686 |
| gwangju | 1,173 |
| gyeongbuk | 4,413 |
| gyeonggi | 8,885 |
| gyeongnam | 4,202 |
| incheon | 2,258 |
| jeju | 698 |
| jeonbuk | 2,363 |
| jeonnam | 3,553 |
| sejong | 473 |
| seoul | 4,214 |
| ulsan | 751 |
