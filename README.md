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
  ⑤ 출력 값이 40에서 60도일 때 LED(빨강) 두 개가 구동한다.<br>
  ⑥ 출력 값이 30에서 40도 이상 일 때 LED(빨강) 한 개가 구동한다.<br>
  ⑦ 출력 값이 20에서 30도일 때 LED(초록) 한 개가 구동한다.<br>
  ⑧ 출력 값이 0에서 20도 이하 일 때 LED(초록) 두 개가 구동한다.<br>
  ⑨ 100k옴 전위차계를 이용해 수동으로 팬 구동 세기를 스텝모터 드라이버 회로로 조절가능하다.
  
7. 실험결과 및 고찰<br>
 이번 실험에는 지금까지 디지털논리회로 설계 실험을 통해 배웠던 것들을 응용하여 하나의 프로젝트로 만드는 것이었다. 555타이머 IC를 이용한 클럭 펄스를 통해 업/다운 카운터(74LS192)와 디코더(74LS47)를 통해 세그먼트(anode 타입)로 나타내고, tactile 스위치를 이용하여 온도를 임의로 원하는 온도로 제어한다. NOT게이트(74LS04N)와 OR게이트(74LS32N)의 조합으로 초록색, 빨간색의 LED를 사용해 현재 온도에 따라 냉방이 필요한지 난방이 필요한지 가시적으로 알 수 있다. <사진 4>의 회로 시물레이션을 보면 온도가 42도일 때 40~60도의 범위에서는 빨간색 LED가 2개 켜지는 것으로 정상적으로 작동하는 것을 확인을 할 수 있다. 현재 온도에 따라 냉난방의 세기를 조절하도록 한다. 냉난방의 세기를 조절하는 매개체로 스텝 모터를 이용한 팬을 사용하도록 한다. 사용자가 팬을 직접 조종할 수 있도록 만들기 위해 가변저항을 써서 모터를 제어한다. <br>
 실험 도중에 주의해야 할 점으로는 첫 째, 세그먼트의 타입을 anode 타입인지, cathode 타입인지 확인해야 한다. anode 타입은 Vcc에 연결해주어야 하고, cathode는 GND에 연결해주어야 한다. 그 이유는 타입에 따라 다이오드의 방향이 다르므로 전류의 방향을 올바르게 해주어야 작동을 하기 때문이다. 둘 째, 스텝 모터 부분 카운터(CD4017)에서 CMOS 종류의 IC이므로 모두 사용하지 않는 게이트는 꼭 GND 혹은 Vcc에 연결해주어야 한다. 그대로 방치하게 되면 불필요한 큰 전류와 정전 파괴를 일으키는 경우가 있기 때문에 주의가 필요하다. 또한 CMOS IC는 정전기에 약하므로 보관 할 때 더 주의를 기울였다. 셋 째, 온도를 제어하기 위한 스위치의 종류를 설계목적에 따라 잘 결정해야 한다. Push 스위치에는 누를 때마다 잠기고 풀림의 토글을 반복하는 Self Lock type(Latching type)이 있고 누를 때마다 상태를 유지하지 않고 원래 상태로 돌아오는 Momentary의 Non Lock type(Push type)의 두 가지 형태가 있다. 이번 설계에서는 좀 더 정밀하게 누를 때마다 온도를 증가시키거나 감소시키게 하기 위해 Non Lock type(Push type)의 tactile switch를 사용하였다. 한번 누르면 계속 증가하다가 멈추고 싶을 때 멈추게 하려면 Self Lock type(Latching type)을 사용하면 된다. 넷 째, 데이터시트를 꼭 확인하여 최대 인가 전압이 얼마인지, 풀업 저항을 달아줘야 하는 소자인지, 허용 전압 범위는 얼마인지 확인하면서 실험을 해야 한다. <br>
 타이머에서 발생하는 클럭의 주파수는 f=1.44/(Ra+2Rb)C[Hz]의 식을 통해 계산해보았다. NE555의 5번 핀인 커패시터는 없어도 무방하기 때문에 굳이 커패시터를 달지 않았다. 7번 핀과 연결된 저항 즉, Ra=91[ohm], Rb=91[ohm]이고 6번 핀과 연결된 커패시터의 값 C=100[uF]으로 설정하여 빠른 주파수를 만들었다. 그 계산값은 f=1.44/(91[ohm]+2*91[ohm])*100*10^(-6)=52.75[Hz], T=1/f=1/52.75=0.019[sec]가 나온다. <br>
 실험 오차의 원인에는 실험장비의 노후화, 회로도 내부와 실험기기의 내부저항, 리드선의 저항, 브레드보드 내부의 결함 등이 있을 수 있겠다. 실험을 원활하게 하기 위해 입력값이나 출력값이 허용 전압 범위 내에 있는지 확인하면서 하였고, 리드선의 저항을 최소화하기 위해 최대한 짧게 이용하였다. 이번 설계에서 스텝 모터를 구동시키는 것에 많은 시행착오가 있었는데, 클럭 펄스를 이용해야 하기 때문에 직류전원모터가 아닌 스텝 모터를 사용하였다. 이번 설계에서
 사용한 스텝 모터는 데이터시트를 확인해 보면 15씩 돌아가는 모터이다. 스텝 모터는 1펄스당 일정각도로 정확히 움직인다. 모터의 원리는 목차 2.2-(2)번에 설명해 놓았다. 실험에서 고전했던 부분은 555타이머에서 나오는 클럭 펄스가 자꾸 트랜지스터(1N4007)를 지나면 펄스가 매우 감소되어 원인을 찾는 데 많은 시간을 썼다. 모터를 돌리기에 매우 부족한 전압의 양이라 판단하여 교수님의 말대로 전류도 허용전류 범위 내에서 상당량 인가해보고 증폭기를 이용해 펄스를 증폭시켜봤지만 이유를 알 수 없었다. 결국 문제는 트랜지스터가 위치했던 브레드내부의 문제가 있었던 것으로 판별되어 결국 스텝 모터를 무사히 구동시킬 수 있게 되었다. 
