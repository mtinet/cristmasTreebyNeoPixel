# cristmasTreebyNeoPixel

## 아두이노 나노와 네오픽셀을 이용해 크리스마스 트리 만들기

---
### 제작 설명서
* 아두이노에서 네오픽셀을 사용하기 위해 아두이노의 라이브러리 폴더에 [Adafruit의 NeoPixel라이브러리](https://github.com/adafruit/Adafruit_NeoPixel)를 설치한다.(설치폴더는 아두이노IDE가 설치 되어 있는 폴더의 libraries폴더이며, 보통 윈도우의 경우 C:/Program Files/Arduino/library에 압축을 풀어 설치하면 된다.)
* 설치가 끝나면 아두이노IDE를 재시작한다.(압축을 풀 때는 이중 폴더가 되지 않도록 해야 라이브러리가 제대로 인식된다.)
* 제대로 인식이 되었다면 아두이노IDE의 파일-예제 탭에 Adafruit NeoPixel이 보일 것이고, 몇 가지 예제가 보이는데 우리는 strandtest라는 예제를 사용할 것이다. 해당 예제를 연다. 
* 보드와 포트를 사용자의 상황에 맞게 선택하고, 프로그램을 업로드한다.

* 디폴트 신호핀은 6번이다.
* 16번째 줄의 'Adafruit_NeoPixel strip = Adafruit_NeoPixel(60, PIN, NEO_GRB + NEO_KHZ800);'에서 중간부분의 60이 네오픽셀의 갯수이다. 필요한 만큼의 갯수로 선택한다.

* 네오픽셀의 갯수가 많아지면 더 많은 전력이 필요하다. 특히 트리를 만들 정도의 갯수라면 작은 사이즈의 트리라도 50~100개의 네오픽셀이 사용되는데 단순히 계산해도 100개가 개당 20mA를 사용하면 2A의 전류를 소모한다.
* 따라서, 외부 전력이 필요하며, 아두이노를 제어하는 전력과 네오픽셀에 공급되는 전력을 분리하는 것이 좋다. 
* 아두이노에는 기존의 전원을 그대로 사용하면 되고, 아래 회로에서는 배터리로 사용했지만, 요즘 나오는 스마트폰의 고속충전기 정도의 전력(5V, 2.1A)을 내는 어댑터를 따로 연결해주는 것이 좋다.(본인은 USB케이블을 하나 잘라서 아두이노가 꽂혀있는 브레드보드에 꽂아 외부 전원을 사용할 수 있도록 개조했다.)
* 하지만, 전력을 이렇게 따로 쓰기만 한다고 제대로 동작하지 않는다. 전압 레벨을 맞춰줘야 하는 것이 그것인다. 이는 '마이너스 접지'를 통해 가능하다. 이것은 아두이노의 GND핀과 네오픽셀에 공급하는 전력의 GND(-)를 연결해주는 것으로 갈음된다. 아래의 회로도를 보면 아두이노의 GND핀과 배터리의 음극이 연결되어 있는 것을 확인할 수 있다. 
* 전력 부족으로 자꾸 꺼지는 현상이 생겨 아두이노와 네오픽셀의 전원을 분리했다. 
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/20171223_211309.jpg?raw=true)  
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/20171223_211325.jpg?raw=true)  
* 빨간색 절연 테잎이 붙어져 있는 부분이 USB케이블의 단자를 잘라내고 +, - 만 살려 네오픽셀의 전원으로 사용하는 부분이다. 그 중 - 에 해당하는 선을 아두이노의 GND핀에 꽂아준 것을 확인할 수 있을 것이다. 그 부분이 마이너스 접지를 한 부분이다.  
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/20171223_211338.jpg?raw=true)  
* 네오픽셀을 다루는 자세한 정보는 [여기](http://blog.naver.com/PostView.nhn?blogId=dev4unet&logNo=220824812556&parentCategoryNo=&categoryNo=263&viewDate=&isShowPopularPosts=true&from=search)를 참고하면 좋다.  


---
### 설치 이미지
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/20171223_192550-ANIMATION.gif?raw=true)


---
### 회로도
![](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202017-12-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.35.40.png?raw=true)  


---
### 스케치
스케치 링크는 [여기](https://github.com/mtinet/cristmasTreebyNeoPixel/blob/master/cristmasTreebyNeoPixel.ino)를 클릭하세요.

~~~
#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
  #include <avr/power.h>
#endif

// 이 부분이 신호선으로 사용할 핀을 지정해주는 부분이다. PWM신호를 사용할 수 있는 3, 5, 6, 9, 10, 11번 핀 중 원하는 핀을 사용하면 된다.(아두이노 우노 기준)
#define PIN 6

// 네오픽셀은 몇 가지 종류로 나뉘는데 그 중 큰 구분은 RGB모델과 RGBW모델로 나뉜다는 것이다. 전자는 24비트의 데이터가 하나의 픽셀을 제어하고, 후자는 32비트의 데이터가 하나의 픽셀을 제어한다.(아두이노의 analogWrite는 8비트(0~255)로 제어되므로...) 빨강,  파랑의 세가지 색깔을 제어하기 위해서는 총 24비트가 필요하기 때문이다. 
// Parameter 1 = number of pixels in strip
// Parameter 2 = Arduino pin number (most are valid)
// Parameter 3 = pixel type flags, add together as needed:
//   NEO_KHZ800  800 KHz bitstream (most NeoPixel products w/WS2812 LEDs)
//   NEO_KHZ400  400 KHz (classic 'v1' (not v2) FLORA pixels, WS2811 drivers)
//   NEO_GRB     Pixels are wired for GRB bitstream (most NeoPixel products)
//   NEO_RGB     Pixels are wired for RGB bitstream (v1 FLORA pixels, not v2)
//   NEO_RGBW    Pixels are wired for RGBW bitstream (NeoPixel RGBW products)
// 아래의 세 인수 중 첫 번째가 네오픽셀의 갯수, 두 번째가 아두이노의 핀 넘버(여기서는 6), 세 번째가 네오픽셀의 종류이다. 위의 설명을 보고 자신이 가지고 있는 모델로 써 주면 된다.  
Adafruit_NeoPixel strip = Adafruit_NeoPixel(60, PIN, NEO_GRB + NEO_KHZ800);

// IMPORTANT: To reduce NeoPixel burnout risk, add 1000 uF capacitor across
// pixel power leads, add 300 - 500 Ohm resistor on first pixel's data input
// and minimize distance between Arduino and first pixel.  Avoid connecting
// on a live circuit...if you must, connect GND first.

void setup() {
  // This is for Trinket 5V 16MHz, you can remove these three lines if you are not using a Trinket
  #if defined (__AVR_ATtiny85__)
    if (F_CPU == 16000000) clock_prescale_set(clock_div_1);
  #endif
  // End of trinket special code


  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}

void loop() {
  // Some example procedures showing how to display to the pixels:
  colorWipe(strip.Color(255, 0, 0), 50); // Red
  colorWipe(strip.Color(0, 255, 0), 50); // Green
  colorWipe(strip.Color(0, 0, 255), 50); // Blue
//colorWipe(strip.Color(0, 0, 0, 255), 50); // White RGBW
  // Send a theater pixel chase in...
  theaterChase(strip.Color(127, 127, 127), 50); // White
  theaterChase(strip.Color(127, 0, 0), 50); // Red
  theaterChase(strip.Color(0, 0, 127), 50); // Blue

  rainbow(20);
  rainbowCycle(20);
  theaterChaseRainbow(50);
}

// Fill the dots one after the other with a color
void colorWipe(uint32_t c, uint8_t wait) {
  for(uint16_t i=0; i<strip.numPixels(); i++) {
    strip.setPixelColor(i, c);
    strip.show();
    delay(wait);
  }
}

void rainbow(uint8_t wait) {
  uint16_t i, j;

  for(j=0; j<256; j++) {
    for(i=0; i<strip.numPixels(); i++) {
      strip.setPixelColor(i, Wheel((i+j) & 255));
    }
    strip.show();
    delay(wait);
  }
}

// Slightly different, this makes the rainbow equally distributed throughout
void rainbowCycle(uint8_t wait) {
  uint16_t i, j;

  for(j=0; j<256*5; j++) { // 5 cycles of all colors on wheel
    for(i=0; i< strip.numPixels(); i++) {
      strip.setPixelColor(i, Wheel(((i * 256 / strip.numPixels()) + j) & 255));
    }
    strip.show();
    delay(wait);
  }
}

//Theatre-style crawling lights.
void theaterChase(uint32_t c, uint8_t wait) {
  for (int j=0; j<10; j++) {  //do 10 cycles of chasing
    for (int q=0; q < 3; q++) {
      for (uint16_t i=0; i < strip.numPixels(); i=i+3) {
        strip.setPixelColor(i+q, c);    //turn every third pixel on
      }
      strip.show();

      delay(wait);

      for (uint16_t i=0; i < strip.numPixels(); i=i+3) {
        strip.setPixelColor(i+q, 0);        //turn every third pixel off
      }
    }
  }
}

//Theatre-style crawling lights with rainbow effect
void theaterChaseRainbow(uint8_t wait) {
  for (int j=0; j < 256; j++) {     // cycle all 256 colors in the wheel
    for (int q=0; q < 3; q++) {
      for (uint16_t i=0; i < strip.numPixels(); i=i+3) {
        strip.setPixelColor(i+q, Wheel( (i+j) % 255));    //turn every third pixel on
      }
      strip.show();

      delay(wait);

      for (uint16_t i=0; i < strip.numPixels(); i=i+3) {
        strip.setPixelColor(i+q, 0);        //turn every third pixel off
      }
    }
  }
}

// Input a value 0 to 255 to get a color value.
// The colours are a transition r - g - b - back to r.
uint32_t Wheel(byte WheelPos) {
  WheelPos = 255 - WheelPos;
  if(WheelPos < 85) {
    return strip.Color(255 - WheelPos * 3, 0, WheelPos * 3);
  }
  if(WheelPos < 170) {
    WheelPos -= 85;
    return strip.Color(0, WheelPos * 3, 255 - WheelPos * 3);
  }
  WheelPos -= 170;
  return strip.Color(WheelPos * 3, 255 - WheelPos * 3, 0);
}
~~~
