# Derma Manager

## 주요기능

- 피부미용 기기와 블루투스 연결을 지원 
- 스마트폰 카메라로 얼굴을 촬영하여 피부의 상태를 측정

## 수행역할
- 앱 설계 및 총 제작

## 사용한 기술
- `Swift 4`, `Xcode 11`
- `AVFoundation`, `CoreBluetooth`
- `Alamofire`

## 주요 구현 장면

### 1. 블루투스 연결 (CoreBluetooth)
![bluetooth](https://user-images.githubusercontent.com/42457589/132481152-c9398231-6f63-49e2-b6a8-67f7084061ee.gif)  
 하드웨어 기기와 블루트스 연결을 한다.

### 2. 얼굴 각도 인식 및 자동촬영 카메라
![cam](https://user-images.githubusercontent.com/42457589/132481160-308a01dc-cd5c-42d9-90f3-0d6b0a7e29e2.gif)  
 이미지 분석서버에 전송할 얼굴사진을 촬영한다.

### 3. 이미지 좌우 스크롤 뷰 / 스크롤뷰 확대 축소
![recored](https://user-images.githubusercontent.com/42457589/132481165-550d1a45-7dba-4620-bc23-6209699cd766.gif)  
 분석결과 이미지의 디테일화면을 스크롤 하여 볼수 있다.

### 4. 분석 결과 DB저장
![list](https://user-images.githubusercontent.com/42457589/132481163-c2307729-1035-47c1-8581-d1c1a8d19e88.gif)  
 분석 결과를 DB 에 저장하여 테이블뷰로 표현한다.


