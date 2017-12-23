# cristmasTreebyNeoPixel

## 아두이노 나노와 네오픽셀을 이용해 크리스마스 트리 만들기

---
### 제작 설명서
- 아두이노에서 네오픽셀을 사용하기 위해 아두이노의 라이브러리 폴더에 [Adafruit의 NeoPixel라이브러리](https://github.com/adafruit/Adafruit_NeoPixel)를 설치한다.(설치폴더는 아두이노IDE가 설치 되어 있는 폴더의 libraries폴더이며, 보통 윈도우의 경우 C:/Program Files/Arduino/library에 압축을 풀어 설치하면 된다.)
- 설치가 끝나면 아두이노IDE를 재시작한다.(압축을 풀 때는 이중 폴더가 되지 않도록 해야 라이브러리가 제대로 인식된다.)
- 제대로 인식이 되었다면 아두이노IDE의 파일-예제 탭에 Adafruit NeoPixel이 보일 것이고, 몇 가지 예제가 보이는데 우리는 strandtest라는 예제를 사용할 것이다. 해당 예제를 연다. 
- 보드와 포트를 사용자의 상황에 맞게 선택하고, 프로그램을 업로드한다.

* 디폴트 신호핀은 6번이다.
* 16번째 줄의 'Adafruit_NeoPixel strip = Adafruit_NeoPixel(60, PIN, NEO_GRB + NEO_KHZ800);'에서 중간부분의 60이 네오픽셀의 갯수이다. 필요한 만큼의 갯수로 선택한다.

- 네오픽셀의 갯수가 많아지면 더 많은 전력이 필요하다. 특히 트리를 만들 정도의 갯수라면 작은 사이즈의 트리라도 50~100개의 네오픽셀이 사용되는데 단순히 계산해도 100개가 개당 20mA를 사용하면 2A의 전류를 소모한다.
- 따라서, 외부 전력이 필요하며, 아두이노를 제어하는 전력과 네오픽셀에 공급되는 전력을 분리하는 것이 좋다. 
- 아두이노에는 기존의 전원을 그대로 사용하면 되고, 아래 회로에서는 배터리로 사용했지만, 요즘 나오는 스마트폰의 고속충전기 정도의 전력(5V, 2.1A)을 내는 어댑터를 따로 연결해주는 것이 좋다.(본인은 USB케이블을 하나 잘라서 아두이노가 꽂혀있는 브레드보드에 꽂아서 외부 전원을 사용할 수 있도록 개조했다.
- 하지만, 전력을 이렇게 따로 쓰기만 한다고 제대로 동작하지 않는다. 전압 레벨을 맞춰줘야 하는 것이 그것인다. 이는 '마이너스 접지'를 통해 가능하다. 이것은 아두이노의 GND핀과 네오픽셀에 공급하는 전력의 GND(-)를 연결해주는 것으로 갈음된다. 아래의 회로도를 보면 아두이노의 GND핀과 배터리의 음극이 연결되어 있는 것을 확인할 수 있다. 
- 네오픽셀을 다루는 자세한 정보는 [여기](http://blog.naver.com/PostView.nhn?blogId=dev4unet&logNo=220824812556&parentCategoryNo=&categoryNo=263&viewDate=&isShowPopularPosts=true&from=search)를 참고하면 좋다.  


---
### 설치 이미지
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/20171223_192550-ANIMATION.gif?raw=true)


---
### 회로도
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202017-12-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.35.40.png?raw=true)  
