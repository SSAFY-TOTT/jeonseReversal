# Turn of the Tide

![Logo](https://github.com/SSAFY-TOTT/TOTT/assets/84130518/8fd51875-a4a1-4b85-ab49-7af3ee3bec8e)

Turn of the Tide(TOTT)는 **금융 및 부동산 정보의 결합으로 전세집을 비교하는 통합 애플리케이션**입니다.

## 기획 배경

1. **30대 미만 임차인 급증** : 2018년부터 매해 전년대비 10만건 이상씩 증가하면서 지난해 전국 213만5000명까지 증가했습니다. 특히 수도권에서 2018년부터 임차인이 매년 5만명 이상
   증가했습니다.. 2020년은 10만명이나 늘었다. 또한 임차인의 연령대가 점점 낮아지고 있으며, 2021년 기준 30대 미만 임차인 비율이 2021년 31.2%로 증가하면서 가장 많은 임차인 비율을
   차지했습니다. [관련기사](https://academy.mk.co.kr/news/view.php?year=2021&no=496776)<br><br>
2. **전세대출 총액 167조** :  전세 대출 또한 같은 현상을 겪고 있다. 전세자금 대출 채무자 수는 133만명, 대출 총액은 167조로 집계되었으며, 그 중 2030세대의 비중이 81만명으로 전체 채무자의
   절반 이상을 차지한 것으로 나타났습니다. [관련기사](http://www.m-economynews.com/news/article.html?no=33832)<br><br>
3. **한도 조회만 가능한 기존 은행 어플** : 기존 은행 어플은 사용자의 한도 조회만 가능하고, 부동산 정보는 제공되지 않습니다.<br><br>
4. **전세집 정보 제한** : 기존 부동산 관련 어플은 주로 전세집 정보를 제공하며, 사용자가 가진 한도와 연계된 정보 제공이 부족합니다.<br><br>
5. **시간 부족** : 전세 대출과 부동산 정보를 찾는 것은 시간이 많이 소요되며, 바쁜 사람 혹은 급하게 전세집을 구해야 하는 사람들에게는 부담스러운 작업입니다.

## 주요 기능

사용자에게 **금액, 위치 등** 사용자 기준에 맞춰 전세 매물 정보를 제공하는 기존의 방식에 더하여, 신한은행의 API를 활용하여 **전세 대출 한도**를 제공합니다.

1. 유효한 데이터 필터링 및 업데이트
    - 월전세 데이터 API로부터 전세 여부, 위치 등 12단계로 데이터를 필터링 합니다.
    - 데이터의 업데이트는 주소, 층 등 7개의 조건을 비교하여 갱신 여부를 판단하고, 갱신되지 않은 데이터는 사용하지않는 소프트 딜리트 방식을 적용합니다.<br><br>
2. 매물 검색 시 전세 대출 한도 제공
    - 검색 페이지
    - 전세 매물 조건 설정 시, 사용자가 매물 최대 금액을 설정하면 그에 따른 전세 대출 한도를 제공합니다.
    - 상세 페이지
        - 전세 매물의 상세 페이지에서 사용자의 자산 대비 대출이 필요한 금액을 제공합니다.
        - 필요한 대출 금액은 자세한 수치와 함께 전세 대출 한도 대비 %비율로 표시 되며, 해당하는 대출 금액에 대한 이율이 함께 표시됩니다.

## 기대효과

- 사업 타당성
    - 전세 매물 검색을 통한 부동산 서비스와 전세 대출 한도 조회를 통한 금융 서비스를 자연스럽게 연결하여 전세를 찾기 위한 시간을 단축할 수 있습니다.
    - 이는 사용자의 이용률을 높여 대출 서비스 연결 등의 금융 서비스 확장으로 이어질 수 있습니다.

- 수익성
    - 사용자는 어플리케이션을 통해 전세 대출에 대한 정보를 신속하게 수집할 수 있으며, 이로 인해 전세 대출이 유도될 수 있습니다.

## 아이디어 실현 및 구체화 방안

1. 주택 정보 저장  
   1.1. [서울 공공데이터](https://data.seoul.go.kr/dataList/OA-21276/S/1/datasetView.do) API를 호출합니다.  
   1.2. 호출받은 API 데이터 중 조건에 맞는 데이터를 필터링합니다.  
   1.3. 전세 주택의 자치구 명/ 법정동 명/ 본 번/ 부 번을 기반으로 **좌표 변환 API**를 통해 좌표로 변환합니다.   
   1.4. 필터링 된 데이터를 DB에 저장합니다.  <br><br>
2. 사용자 본인 인증  
   2.1. 사용자는 **1원 이체**를 통해 본인을 인증합니다.  
   2.2. 인증이 된 사용자의 **전체 계좌를 조회**한 후 사용자의 현재 자산을 확인합니다. 이는 후 전세 대출 한도를 확인할 때 사용됩니다.  <br><br>
3. 대출 한도 설정을 통한 전세 주택 검색  
   3.1. 사용자는 여러 조건에 맞는 전세 주택을 검색할 수 있습니다.  
   3.2. 사용자가 선택한 전세 주택의 전세값을 토대로 **대출 한도**를 조회합니다. <br><br>
4. 주택 지도 표시 및 정보 제공  
   4.1. 전세 주택은 법정동 코드 데이터를 통해 구/동으로 구분됩니다.  
   4.2. 전세 주택의 좌표를 기반으로 **Kakao Map Local API**를 통해 지도에 표시합니다.

<br>

## 서비스 아키텍처

<img src="https://github.com/SSAFY-TOTT/TOTT/assets/74192619/d3de8ed6-e126-4784-ad10-ec12b1bff828" width="800" alt="서비스 아키텍처">

<br>

## Open API

### 신한은행 API

---

<img src="https://github.com/SSAFY-TOTT/TOTT/assets/74192619/c96525ff-beb6-45e0-b033-81950bef3884" width="300" alt="신한은행 LOGO">

<br><br>

| 번호 | API         | 설명                                    |
|:--:|:------------|---------------------------------------|
| 1  | 전세 대출 한도 조회 | 계좌를 기반으로 전세 대출 한도를 조회할 수 있습니다.        |
| 2  | 전체 계좌 목록    | 사용자의 계좌들을 모두 조회합니다.                   |
| 3  | 예금주 실명 조회   | 사용자 인증을 위해 사용됩니다.                     |
| 4  | 1원 이체       | 사용자 계좌에 금액 1원과 식별 코드를 전송하여 계좌를 인증합니다. |

<br>

API 들의 활용을 하나의 흐름으로 살펴보면 다음과 같습니다.

1. 사용자가 회원 가입 진행 시, 예금주 실명 조회 API 를 호출하여 본인 인증을 진행한 후
2. 1원 이체 API 호출을 통해 사용자 계좌에 금액 1원과 식별 코드를 전송하여 계좌를 인증합니다.
3. 전체 계좌 목록 API 를 호출하여 사용자의 전체 계좌를 조회한 후, 예적금 계좌들의 금액 총합을 사용자 자산으로 저장합니다.
4. 이제부터 사용자의 매물 확인이 가능합니다.<br>
   검색 조건 선택 시 최대 매물 금액을 설정하거나, 매물 정보를 확인 시 전세 대출 한도 조회 API 를 호출하여 정보를 제공합니다.

<br>

### 서울 열린데이터 광장

---

<img src="https://github.com/SSAFY-TOTT/TOTT/assets/74192619/56b6b438-d406-42a6-86ca-80757d2dacd7" width="300" alt="서울 열린데이터 광장 LOGO">

<br><br>

| 번호 | API             | 설명                                                                                           |
|:--:|:----------------|----------------------------------------------------------------------------------------------|
| 1  | 서울시 부동산 전월세가 정보 | 서울 부동산 정보광장에서 제공하는 전월세가 정보입니다. 자치구, 법정동, 건물명, 임대건물명, 전월세구분, 보증금, 임대료, 계약년도 등의 전월세 정보를 제공합니다. |

<br>

### 카카오 API

---

<img src="https://github.com/SSAFY-TOTT/TOTT/assets/74192619/73f1fc30-a800-4561-b08e-e8fdb4c3d2ef" width="300" alt="카카오 MAPS LOGO">

<br><br>

| 번호 | API       | 설명                                                |
|:--:|:----------|---------------------------------------------------|
| 1  | Local API | 주소를 지도 위에 정확하게 표시하기 위해 해당 주소의 좌표 정보를 제공하는 API입니다. |

<br>

키워드로 특정 장소 정보를 조회하거나, 좌표를 주소 또는 행정구역으로 변환하는 등 장소에 대한 정보를 제공합니다.
매물, 역 등의 주소를 기반으로 좌표를 추출합니다. 이후 지역, 지하철 역, 좌표를 기준으로 조회 시에 매물 좌표를 기준으로 조회할 때 필요합니다.

## 관련 기사

1. [신한은행, 청년 채용 연계한 '신한 해커톤 with SSAFY' 개최](https://daily.hankooki.com/news/articleView.html?idxno=1000809)
