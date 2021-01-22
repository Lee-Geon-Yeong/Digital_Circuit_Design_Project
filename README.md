# 스텝모터를 이용한 냉‧난방시스템의 디지털회로설계

### 연구 배경
1. 연구 배경

- 연구 목적 : 집에 있는 에어컨을 보면, 현재 온도와 습도를 알려 주고, 사용자가 원하는 온도에 맞춰 냉방 혹은 난방을 시켜 준다. 이러한 냉난방 시스템을 마이크로컨트롤러 없이 디지털 소자만으로 냉난방시스템을 구현해보고자 하였다. 온습도 센서로 원하는 온도를 맞추는 것에 한계가 있을 것으로 판단되므로, 업/다운 카운터와 tactile 스위치를 이용해 온도를 임의적으로 제어함에 초점을 둔다.
- 연구내용 요약 : 온도를 임의로 설정하여 세그먼트로 나타내고, 현재 온도에 따라 냉난방의 세기를 조절하도록 한다. 실제 냉난방기를 사용할 수 없으므로 초록색, 빨간색의 LED를 사용해 현재 온도에 따라 냉방이 필요한지 난방이 필요한지 가시적으로 알 수 있다. 불빛이 들어오는 개수에 따라 세기를 표현하도록 한다. 온도에 변화를 주기 위해 모터를 이용한 팬이라는 매개체를 사용하도록 한다. 사용자가 팬을 직접 조종할 수 있도록 만들기 위해 가변저항을 써서 모터를 제어한다. 이 프로젝트에서는 555 타이머 IC (컨트롤러로 작동), CD4017 decade 카운터 (드라이버로 작동) 및 기타 구성 요소를 사용하여 간단한 12V stepper 모터 드라이버 회로를 설계한다.

### 설계 내용
1. 개념도<br>
![image](https://user-images.githubusercontent.com/59759468/105456985-72d9f280-5cc9-11eb-946a-b625bd1bc6db.png)

2. 흐름도(flowchart)<br>
![image](https://user-images.githubusercontent.com/59759468/105457053-8dac6700-5cc9-11eb-8626-827f39b6c728.png)

3. 블록도<br>
![image](https://user-images.githubusercontent.com/59759468/105457145-acaaf900-5cc9-11eb-96a0-b4755ddd13e2.png)

4. 회로 시뮬레이션<br>
- 냉난방시스템 회로 시뮬레이션<br>
![image](https://user-images.githubusercontent.com/59759468/105457198-c2b8b980-5cc9-11eb-83fd-cfce1f0cbfcf.png)
- 스텝 모터 시뮬레이션<br>
![image](https://user-images.githubusercontent.com/59759468/105457209-c6e4d700-5cc9-11eb-947e-2d95757f5727.png)

5. 실제 회로 구성
- 냉난방시스템 회로<br>
![image](https://user-images.githubusercontent.com/59759468/105457478-3eb30180-5cca-11eb-9cf0-dcff76638692.png)
- 스텝 모터 회로<br>
![image](https://user-images.githubusercontent.com/59759468/105457484-41155b80-5cca-11eb-958c-269da602186a.png)

6. 동작 설명
  ① NE555타이머를 이용해서 클럭을 발생시켜 업/다운 카운터(74LS192)를 실행시킨다.<br>
  ② tactile switch를 통해 업/다운 카운터에 인가될 펄스를 제어한다. UP switch를 누르면 온도증가, DOWN switch를 누르면 온도가 감소한다. <br>
  ③ 업/다운 카운터에서 나온 BCD숫자를 디코더(BCD to Segment Decoder, 74LS47)에서 10진수로 변환한 후 7-segment(anode 타입)에 연결해서 값을 출력한다.<br>
  ④ 온도를 가시적으로 표현하기 위해 디코더(BCD to Decimal Decoder, 74LS42)를 이용해서 각 출력에 따라 LED를 구동시킨다.<br>
  ⑤ 출력 값이 40~60도일 때 LED(빨강) 두 개가 구동한다.<br>
  ⑥ 출력 값이 30~40도 이상 일 때 LED(빨강) 한 개가 구동한다.<br>
  ⑦ 출력 값이 20~30도일 때 LED(초록) 한 개가 구동한다.<br>
  ⑧ 출력 값이 0~20도 이하 일 때 LED(초록) 두 개가 구동한다.<br>
  ⑨ 100k옴 전위차계를 이용해 수동으로 팬 구동 세기를 스텝모터 드라이버 회로로 조절가능하다.
