# jetson-nano로 Smart-farm 만들기

***

### 준비물

1. jetson-nano
2. arduino Uno
3. DHT11 온습도 센서

### 아두이노 세팅하기

DHT11 선을 아두이노의 5V,GND,D2에 연결한다.

회로도

![IMG_0673](https://github.com/user-attachments/assets/381c31d4-f013-47c1-83f3-cf872e0592a5)

![IMG_0674](https://github.com/user-attachments/assets/627b00a0-67da-4a9a-8d35-610e5213ab76)

회로를 이렇게 연결했다면, 제슨에 arduino.cc 1.8.19 버전을 깔아야 한다.

![IMG_0675](https://github.com/user-attachments/assets/1d24e802-f054-4275-8d6b-6055178f16e8)

우리는 제슨을 쓰니 chat 대신 jetson을 치면 된다.
    
    #include <SimpleDHT.h>
    int pinDHT11=2;
    SimpleDHT11 dht11(pinDHT11);
    void setup() {
    Serial.begin(115200);
    }
    
    void loop() {
    byte temperature = 0;
    byte humidity = 0;
    
    if (dht11.read(&temperature, &humidity, NULL) ==
    SimpleDHTErrSuccess) {
    int temp (int)temperature;
    int humid (int)humidity;
    
    #유효한 범위민지 확인 
    if (temp >= 0 && temp <= 50 && humid >= 0 && humid <= 100) {
    Serial.print(temp);
    Serial.print(",");
    Serial.println(humid);
    }
    }
    
    delay(2000);
    }

아두이노 깔고 들어가면 예시코드가 있다. 예시 코드를 이걸로 수정하면 된다.
board,port를 맞춰야한다.

![IMG_0676](https://github.com/user-attachments/assets/404df456-69ad-4760-a51f-e0b6ece017cc)

하라는대로 하면 이렇게 시니얼 모니터에 뜨게 된다.

***

이제 이 값들을 내 메일로 옮겨보자.

