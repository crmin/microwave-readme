# Microwave Controller

"

## 동작 내용
컨트롤러 프로그램을 통해 설정된 target temperature까지 가열한 후 다음 조건에 맞도록 실행합니다.
* target temperature에 도달하면 해당 온도를 유지하도록 합니다.
    * target temperature보다 온도가 떨어진 경우 microwave를 조사하여 가열합니다.
    * target temperature보다 온도가 높은 경우 온도가 떨어질 때 까지 조사를 중지합니다.
* 위 조건에 따라 조사한 총 시간의 합산이 target time이 될 때 까지 반복합니다.

## 실행 방법
기본적으로 전원을 연결하면 자동으로 실행됩니다.
![image](https://user-images.githubusercontent.com/8157830/157045345-a9d79701-298e-4031-b633-0494a23ebeca.png)
### 화면 설명
#### Temperature
* Target Temperature: 사용자가 설정한 목표 온도입니다. 해당 온도까지 가열한 후 온도를 유지합니다.
* Current Temperature: 센서가 측정한 현재 온도입니다. 센서는 200°C까지 측정할 수 있으므로 위 사진의 값은 오류를 의미합니다. 자세한 내용은 Troubleshooting 항목을 참고해주세요.
* +10°C, +1°C, +0.1°C, -10°C, -1°C, -0.1°C: targhet temperature를 변경할 수 있는 버튼입니다. 센서의 민감도가 0.1°C이기 때문에 최소 1°C 단위로 설정하는 것을 추천합니다.

#### Time
* Target Irradiation Time: 목표 조사 시간입니다. 목표 온도 도달 후 microwave를 조사할 총 시간을 설정합니다.
* Current Irradiation Time: 목표 온도 도달 후 현재까지 누적 조사 시간입니다.
* +1H, +10M, ..., -1S, -0.1S: Target Irradiation Time을 변경할 수 있는 버튼입니다. 0.1초 정도의 오차가 있을 수 있으므로 1초 단위로 설정하는 것을 추천합니다.

#### 하단 시간
* Experiment Time: 총 실험 시간입니다. Experiment Start 버튼을 눌러 시작된 후 현재까지의 시간, 종료되었다면 종료시까지의 시간을 표시합니다.
* Target Temperature Reached: 실험 시작 후 목표 온도에 도달한 시간을 기록합니다. 아직 도달하지 않았다면 `Not reached yet`이 표시됩니다.
* Experiment Time After Reach: 목표 온도에 도달 후 현재까지, 종료되었다면 종료 시점까지의 실험 시간을 표시합니다. 아직 도달하지 않았다면 `Not reached yet`이 표시됩니다.

#### Result Image Server
* 실험 결과를 확인할 수 있는 서버 주소입니다. 센서 컴퓨터가 연결된 네트워크와 같은 네트워크(아마도 학교 인터넷)의 컴퓨터나 휴대폰을 이용하여 접속 가능합니다.

#### State
* 현재 실험 상태를 나타냅니다.
    * `ready`: 현재 동작중이 아니며 실험을 대기하고 있습니다.
    * `Preparatory stage irradiation`: 목표 온도에 도달하기 위해 가열중입니다. 이 시간은 조사 시간에 포함되지 않습니다.
    * `Irradiation`: 목표 온도에 도달 후 온도가 떨어져서 조사중입니다. 이 시간이 조사 시간에 포함됩니다.
    * `Irradiation paused (exceed target temp)`: 목표 온도를 초과해서 조사를 중지했습니다. 온도가 떨어진 후 조사를 재개합니다.

## 실험 결과 확인
* 실험 중 온도 변화와 조사 시간에 대한 그래프가 제공됩니다. 제공되는 결과는 해당 컴퓨터의 ip 주소로 접근하면 됩니다. ip 주소는 프로그램 좌측 하단에서 확인하실 수 있습니다. (실험 중 수동으로 중지한 경우에는 제공하지 않습니다)

![image](https://user-images.githubusercontent.com/8157830/156930436-d5eb4198-64a0-4bd1-9852-53bd3885fe37.png)

![image](https://user-images.githubusercontent.com/8157830/156930457-a6e14833-42a6-4fe2-a186-a20b12cd46a2.png)


## 주의/참고 사항
* 목표 온도에 도달할 때 까지 가열 후 조사를 중지해도 물의 온도는 계속 올라갑니다.
    * 테스트 과정에서 확인한바로는 상온에서 가열 시작시 3°C ~ 5°C 정도까지 더 오르는 경우를 확인했습니다.
    * 이를 방지하기 위해서 목표 온도까지 다른 수단으로 가열 후 실험하는 것이 효과적일 수도 있습니다.
* 모니터 뒤에 달린 케이블은 뽑으면 안됩니다.
* 온도 센서 광섬유를 당기거나 과도하게 굽히면 안됩니다. (손상되면 동작하지 않습니다)
* 실험 중 절대 문을 열지 마세요, 결과가 비정상적으로 측정될 수 있습니다. (실험 중단시 화면의 `Experiment Stop` 버튼을 클릭하고 열기)
* 실험 중 전자레인지 버튼을 조작하지 마세요
* `Experiment Start` 버튼을 누르기 전에 전자레인지 화면에 시간이 표시되었는지 확인해주세요. 전자레인지 화면에 전원이 안들어와있다면 다시 문을 열었다가 닫아주세요. 절전모드로 인해서 전자레인지 화면에 전원이 안들어와있는 상태에서는 실험을 시작할 수 없습니다.

## Troubleshooting
### 컨트롤러에서 읽은 온도 값이 `999.9°C` 또는 `9999.0°C`입니다.
* 온도 센서를 컴퓨터가 인식하지 못하고 있습니다. 다음을 확인해주세요
    * (`999.9°C`인 경우) 온도 센서 광섬유가 컨트롤박스에 연결되었나요?
    * (`9999.0°C`인 경우) 온도 센서 플러그가 콘센트에 연결되었나요?
    * (`9999.0°C`인 경우) 모니터 뒤에 달린 핀 중 빠진 것이 있나요?
### 프로그램이 종료되었습니다.
![image](https://user-images.githubusercontent.com/8157830/157045316-58e09508-e6a1-47b4-af5d-f0d1e0a4aa89.png)

controller 아이콘을 두번 터치하면 실행됩니다.

![image](https://user-images.githubusercontent.com/8157830/157045330-cccb5406-b1f5-4ae6-b5e8-ac4602c30d3d.png)

위 사진과 같은 창이 뜰 경우 `실행(E)`를 터치하면 됩니다.