# 🚽 toilet-data — 전국 공중화장실 좌표 데이터 (시도별 JSON)

전국 공중화장실 **43,350곳**의 이름·좌표·개방시간·주소. 웹앱에서 `fetch`로 바로 사용 가능 (raw.githubusercontent.com은 CORS `*` 허용).

## 사용법

```
https://cdn.jsdelivr.net/gh/ouiwefilm-cloud/toilet-data@main/data/index.json   ← 시도별 건수/경계(bounds)
https://cdn.jsdelivr.net/gh/ouiwefilm-cloud/toilet-data@main/data/seoul.json   ← 시도별 데이터
```

시도 키: seoul busan daegu incheon gwangju daejeon ulsan gyeonggi gangwon chungbuk chungnam jeonbuk jeonnam gyeongbuk gyeongnam sejong jeju etc

## 스키마 (행 = 배열)

| idx | 내용 | 예 |
|---|---|---|
| 0 | 화장실명 | "창덕공원" |
| 1 | 위도(WGS84) | 37.57799 |
| 2 | 경도(WGS84) | 126.99219 |
| 3 | 편의 플래그(비트합) | 1=24시간, 2=장애인, 4=기저귀교환대, 8=어린이용, 16=CCTV, 32=비상벨 |
| 4 | 개방시간(원문, 형식 제각각) | "09:00~18:00", "상시" |
| 5 | 도로명/지번 주소 | "서울특별시 종로구 …" |

## 출처·주의

- 원천: 행정안전부 **전국공중화장실표준데이터** (공공누리, data.go.kr/data/15012892)
- 좌표: 2025-02 이후 원천에서 좌표 제공이 중단되어, 좌표 포함 구버전 스냅샷 계열의 공개 미러(daeillband2014-hub/toilet-map-korea)를 경유해 수집 (공식 약 5.2만 건 중 43,350건)
- ⚠️ **MVP/개발용.** 정식 출시 전에는 data.go.kr OpenAPI(tn_pubr_public_toilet_api) 최신 데이터 + VWorld/카카오 지오코딩으로 자체 재구축 권장
- 개방시간은 원문 그대로라 앱에서 파싱 필요 ("상시"/"24시간" 포함 시 상시 개방 처리 권장)
