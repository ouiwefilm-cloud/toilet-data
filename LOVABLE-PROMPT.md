# 러버블에 붙여넣을 프롬프트 (복사해서 Lovable 채팅에 그대로)

---

전국 공중화장실 찾기 모바일 웹앱을 만들어줘.

**데이터** (fetch로 가져와, CORS 허용됨):
- 인덱스: https://cdn.jsdelivr.net/gh/ouiwefilm-cloud/toilet-data@main/data/index.json — 시도별 건수와 bounds
- 시도별 데이터: https://cdn.jsdelivr.net/gh/ouiwefilm-cloud/toilet-data@main/data/{region}.json
  (region: seoul, busan, daegu, incheon, gwangju, daejeon, ulsan, gyeonggi, gangwon, chungbuk, chungnam, jeonbuk, jeonnam, gyeongbuk, gyeongnam, sejong, jeju, etc)
- 각 행은 배열: [화장실명, 위도, 경도, 플래그, 개방시간문자열, 주소]
- 플래그는 비트합: 1=24시간, 2=장애인화장실, 4=기저귀교환대, 8=어린이용, 16=CCTV, 32=비상벨

**핵심 플로우**:
1. 앱 열리면 즉시 navigator.geolocation으로 내 위치 요청 (거부 시 서울시청 기본값 + 주소 검색 안내)
2. index.json의 bounds와 내 좌표를 비교해 **해당하는 시도 + 인접 시도 파일만** 로드 (전국 한 번에 로드 금지)
3. 내 위치 기준 Haversine 거리 계산해 가까운 순 정렬
4. 화면: 상단 지도(Leaflet + OpenStreetMap 타일, 내 위치 마커 + 화장실 마커), 하단 가까운 순 리스트(이름·거리·개방시간·편의 태그 뱃지)
5. 항목 탭하면 상세 시트: 주소, 개방시간, 편의시설 뱃지(24시간/장애인/기저귀교환대/어린이/CCTV/비상벨), "길찾기" 버튼(카카오맵 웹 길찾기 링크: https://map.kakao.com/link/to/이름,위도,경도)
6. 필터 칩: 전체 / 24시간 / 장애인 / 기저귀교환대
7. "지금 열려 있을 가능성" 표시: 개방시간 문자열에 "24" 또는 "상시" 포함 → 항상 열림 배지. "HH:MM~HH:MM" 패턴이 파싱되면 현재 시각과 비교해 열림/닫힘. 파싱 불가면 개방시간 원문만 표시(추측 금지)

**디자인**: 모바일 우선, 한 손 사용. 큰 터치 타겟. 급한 사람이 3초 안에 가장 가까운 열린 화장실을 찾는 게 목표. 미니멀하고 깨끗하게, 파란색 계열.

**주의**: 데이터는 공공데이터 기반이며 실제와 다를 수 있다는 면책 문구를 하단에 작게.

---

## (선택) 이후 러버블에 추가로 시킬 것
- "거리순 리스트에 도보 예상시간(분)도 표시해줘 (80m/분 기준)"
- "즐겨찾기 기능 추가 (localStorage)"
- "다크모드"
