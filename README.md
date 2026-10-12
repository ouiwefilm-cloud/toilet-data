# 🚽 toilet-data — 전국 공중화장실 좌표 데이터 (시도별 JSON)

전국 공중화장실 **42,513곳**의 이름·좌표·개방시간·주소·편의시설. 웹앱에서 `fetch`로 바로 사용 가능
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
- 좌표: 2025-02 이후 원천 CSV 에 좌표가 없다. 그래서 이전 판(좌표 포함 구버전 스냅샷의 공개 미러
  daeillband2014-hub/toilet-map-korea)의 좌표를 **같은 주소**에 재사용했다. 모든 좌표는 공공데이터 출처다.
- **빠진 곳:** 이전 판에 없던 새 화장실·주소가 바뀐 곳 약 9,500곳은 좌표가 없어 아직 빠져 있다.
  저장이 허용되는 공공데이터(도로명주소 위치정보요약DB)로 채울 예정이다.
- **카카오·브이월드 지오코딩 결과는 넣지 않는다.** 두 서비스 모두 결과의 저장·재배포를 금지한다(실시간 호출만 허용).
- 재구축 스크립트: ouiwefilm-cloud/simple-md-reader 의 `scripts/toilet-data/rebuild.py`
- 공공데이터 원본 특성상 실제와 다를 수 있다.

## 지역별 건수

| 시도 | 건수 |
|---|---|
| busan | 2,288 |
| chungbuk | 1,803 |
| chungnam | 1,867 |
| daegu | 1,653 |
| daejeon | 1,363 |
| etc | 0 |
| gangwon | 3,629 |
| gwangju | 1,092 |
| gyeongbuk | 4,365 |
| gyeonggi | 6,804 |
| gyeongnam | 4,042 |
| incheon | 2,074 |
| jeju | 692 |
| jeonbuk | 2,270 |
| jeonnam | 3,272 |
| sejong | 472 |
| seoul | 4,085 |
| ulsan | 742 |
