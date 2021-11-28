# Derma Manager

## 주요기능

- 피부미용 기기와 블루투스 연결을 지원 
- 블루투스 제어 기능
- 스마트폰 카메라로 얼굴을 촬영하여 피부의 상태를 측정

## 수행역할
- 단독 앱 기획 및 총 제작 배포
- 하드웨어 설계 및 개발

## 사용한 기술
- `Swift 4`, `Xcode 11`
- `AVFoundation`, `CoreBluetooth`
- `Alamofire`

## 적용한 주요 Layout
- `TableView`
- `TabbarController`
- `ScrollView`

## 한계점 / 개선점
- 네비게이션 컨트롤러를 적용하여 깔끔한 UI를 제작할 필요가 있음
- 2번째 탭의 구성을 ScrollView 대신 TableView 나 CollectionView를 적용하여 깔끔하게 재구성할 필요가 

## 주요 구현 장면

### 1. 블루투스 연결 (CoreBluetooth)
![bluetooth](https://user-images.githubusercontent.com/42457589/132481152-c9398231-6f63-49e2-b6a8-67f7084061ee.gif)  
 하드웨어 기기와 블루트스 연결을 한다.
### 1
``` swift
 // 1. 디바이스 스캔시작 
 centralManager.scanForPeripherals(withServices: nil) 

``` 
### 2
``` swift
 // 1. 디바이스 발견시 연결 
func centralManager(_ central: CBCentralManager, didDiscover peripheral: CBPeripheral, advertisementData: [String : Any], rssi RSSI: NSNumber) {
        if peripheral.name == "myDevice"{
            central.connect(peripheral,options:nil) // 일련번호를 확인후 연결한다
        }
    }

``` 
``` swift
 // 2. notifying 서비스 연결
 func peripheral(_ peripheral: CBPeripheral, didDiscoverCharacteristicsFor service: CBService, error: Error?) {
     guard let charactistics = service.characteristics else{return}
     if charactistic.uuid == notiUUID{
                peripheral.setNotifyValue(true, for: charactistic) // notifiying 서비스를 구독하여 기기에서 변경된 값을 감시
            }
      }
 }
 
 //3. 원하는 패킷 전송
 peripheral.writeValue(value) // 패킷 전송

``` 
### 3
``` swift
// 3. 응답패킷 수신 
 func peripheral(_ peripheral: CBPeripheral, didUpdateValueFor characteristic: CBCharacteristic, error: Error?) {
        switch characteristic.uuid{
        
        case notiUUID:
            guard let s = characteristic.value else {return}
            guard let sData = s.data(using: .utf8) else {return}
            if let string = String(data: sData,encoding: String.Encoding.utf8){
                print("receive : \(string)")
            }
        default:
            print("Unhandled Charactistic UUID: \(characteristic.uuid)")
        }
    }
```
### 2. 얼굴 각도 인식 및 자동촬영 카메라
![cam](https://user-images.githubusercontent.com/42457589/132481160-308a01dc-cd5c-42d9-90f3-0d6b0a7e29e2.gif)  
 이미지 분석서버에 전송할 얼굴사진을 촬영한다.


### 3. 이미지 좌우 스크롤 뷰 / 스크롤뷰 확대 축소
![recored](https://user-images.githubusercontent.com/42457589/132481165-550d1a45-7dba-4620-bc23-6209699cd766.gif)  
 분석결과 이미지의 디테일화면을 스크롤 하여 볼수 있다.

### 4. 분석 결과 DB저장
![list](https://user-images.githubusercontent.com/42457589/132481163-c2307729-1035-47c1-8581-d1c1a8d19e88.gif)  
 분석 결과를 DB 에 저장하여 테이블뷰로 표현한다.


