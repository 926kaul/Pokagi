## 🥚 포카기: 포켓몬 타입 상성 기반 알까기 게임

https://926kaul.github.io/Pokagi/

포카기(Pokagi)는 포켓몬스터 1세대(151종)와 독특한 **물리 엔진 및 타입 상성 시스템**을 결합한 특별한 알까기(물리 충돌) 게임입니다. 포켓몬의 스탯이 충돌 물리량에 직접 영향을 미치며, 전략적인 배치와 타입 상성 계산이 승리의 열쇠입니다.

---

### 🎮 게임 시스템 및 특징

#### 1. 타입 상성과 충돌 속도

포켓몬이 서로 충돌한 후의 **속도**는 **타입 상성**에 의해 결정됩니다. 충돌하는 두 포켓몬의 타입 1과 타입 2가 모두 계산에 반영됩니다 (1세대 타입 상성표 기준).

* **계산 예시:** 바위/땅 타입 포켓몬이 바위/비행 타입 포켓몬을 공격할 경우:
    > $1.0 (\text{바위} \to \text{바위}) \times 0.5 (\text{바위} \to \text{땅}) \times 2.0 (\text{땅} \to \text{바위}) \times 0 (\text{땅} \to \text{비행}) = 0$
    > (최종 결과가 0이므로 해당 충돌은 무효화됩니다.)

#### 2. 포켓몬의 물리 속성 결정

각 포켓몬의 물리적 특성(크기, 질량, 속도)은 **종족값**을 기준으로 50, 70, 100, 120을 경계로 **1~5등급**으로 분류되어 결정됩니다.

| 물리 속성 | 결정 기준 |
| :---: | :---: |
| **크기** | HP 등급 |
| **운동 질량** | $\text{max}(\text{공격}, \text{특수})$ 등급 |
| **정지 질량** | $\text{max}(\text{방어}, \text{특수})$ 등급 |
| **최대 속도** | 스피드 등급 |

<details>
<summary>▶ 여기를 클릭하여 포켓몬 능력치 데이터 보기</summary>

| 번호 | 이름 | 크기 | 운동질량 | 정지질량 | 최대 속도 |
| :-- | :-- | :-- | :-- | :-- | :-- |
| 1 | **이상해씨** | 1 | 1.5 | 1.5 | 15 |
| 2 | **이상해풀** | 1.5 | 2 | 2 | 18 |
| 3 | **이상해꽃** | 2 | 2.5 | 2.5 | 22 |
| 4 | **파이리** | 1 | 1.5 | 1.5 | 18 |
| 5 | **리자드** | 1.5 | 1.5 | 1.5 | 22 |
| 6 | **리자몽** | 2 | 2 | 2 | 25 |
| 7 | **꼬부기** | 1 | 1.5 | 1.5 | 15 |
| 8 | **어니부기** | 1.5 | 1.5 | 2 | 18 |
| 9 | **거북왕** | 2 | 2 | 2.5 | 22 |
| 10 | **캐터피** | 1 | 1 | 1 | 15 |
| 11 | **단데기** | 1.5 | 1 | 1.5 | 15 |
| 12 | **버터플** | 1.5 | 2 | 2 | 22 |
| 13 | **뿔충이** | 1 | 1 | 1 | 18 |
| 14 | **딱충이** | 1 | 1 | 1.5 | 15 |
| 15 | **독침붕** | 1.5 | 2 | 1 | 22 |
| 16 | **구구** | 1 | 1 | 1 | 18 |
| 17 | **피죤** | 1.5 | 1.5 | 1.5 | 22 |
| 18 | **피죤투** | 2 | 2 | 2 | 22 |
| 19 | **꼬렛** | 1 | 1.5 | 1 | 22 |
| 20 | **레트라** | 1.5 | 2 | 1.5 | 22 |
| 21 | **깨비참** | 1 | 1.5 | 1 | 22 |
| 22 | **깨비드릴조** | 1.5 | 2 | 1.5 | 25 |
| 23 | **아보** | 1 | 1.5 | 1 | 18 |
| 24 | **아보크** | 1.5 | 2 | 1.5 | 22 |
| 25 | **피카츄** | 1 | 1.5 | 1.5 | 22 |
| 26 | **라이츄** | 1.5 | 2 | 2 | 25 |
| 27 | **모래두지** | 1.5 | 2 | 2 | 15 |
| 28 | **고지** | 2 | 2.5 | 2.5 | 18 |
| 29 | **니드런♀** | 1.5 | 1 | 1.5 | 15 |
| 30 | **니드리나** | 2 | 1.5 | 1.5 | 18 |
| 31 | **니드퀸** | 2 | 2 | 2 | 22 |
| 32 | **니드런♂** | 1 | 1.5 | 1 | 18 |
| 33 | **니드리노** | 1.5 | 2 | 1.5 | 18 |
| 34 | **니드킹** | 2 | 2 | 2 | 22 |
| 35 | **삐삐** | 2 | 1.5 | 1.5 | 15 |
| 36 | **픽시** | 2 | 2 | 2 | 18 |
| 37 | **식스테일** | 1 | 1.5 | 1.5 | 18 |
| 38 | **나인테일** | 2 | 2.5 | 2.5 | 25 |
| 39 | **푸린** | 2.5 | 1 | 1 | 15 |
| 40 | **푸크린** | 3 | 2 | 1.5 | 15 |
| 41 | **주뱃** | 1 | 1 | 1 | 18 |
| 42 | **골뱃** | 2 | 2 | 2 | 22 |
| 43 | **뚜벅초** | 1 | 2 | 2 | 15 |
| 44 | **냄새꼬** | 1.5 | 2 | 2 | 15 |
| 45 | **라플레시아** | 2 | 2.5 | 2.5 | 18 |
| 46 | **파라스** | 1 | 2 | 1.5 | 15 |
| 47 | **파라섹트** | 1.5 | 2 | 2 | 15 |
| 48 | **콘팡** | 1.5 | 1.5 | 1.5 | 15 |
| 49 | **도나리** | 2 | 2 | 2 | 22 |
| 50 | **디그다** | 1 | 1.5 | 1 | 22 |
| 51 | **닥트리오** | 1 | 2 | 2 | 30 |
| 52 | **나옹** | 1 | 1 | 1 | 22 |
| 53 | **페르시온** | 1.5 | 2 | 1.5 | 25 |
| 54 | **고라덕** | 1.5 | 1.5 | 1.5 | 18 |
| 55 | **골덕** | 2 | 2 | 2 | 22 |
| 56 | **망키** | 1 | 2 | 1 | 22 |
| 57 | **성원숭** | 1.5 | 2.5 | 1.5 | 22 |
| 58 | **가디** | 1.5 | 2 | 1.5 | 18 |
| 59 | **윈디** | 2 | 2.5 | 2 | 22 |
| 60 | **발챙이** | 1 | 1.5 | 1 | 22 |
| 61 | **슈륙챙이** | 1.5 | 1.5 | 1.5 | 22 |
| 62 | **강챙이** | 2 | 2 | 2 | 22 |
| 63 | **캐시** | 1 | 2.5 | 2.5 | 22 |
| 64 | **윤겔라** | 1 | 3 | 3 | 25 |
| 65 | **후딘** | 1.5 | 3 | 3 | 30 |
| 66 | **알통몬** | 2 | 2 | 1.5 | 15 |
| 67 | **근육몬** | 2 | 2.5 | 2 | 15 |
| 68 | **괴력몬** | 2 | 3 | 2 | 18 |
| 69 | **모다피** | 1.5 | 2 | 2 | 15 |
| 70 | **우츠동** | 1.5 | 2 | 2 | 18 |
| 71 | **우츠보트** | 2 | 2.5 | 2.5 | 22 |
| 72 | **왕눈해** | 1 | 2.5 | 2.5 | 22 |
| 73 | **독파리** | 2 | 3 | 3 | 25 |
| 74 | **꼬마돌** | 1 | 2 | 2.5 | 15 |
| 75 | **데구리** | 1.5 | 2 | 2.5 | 15 |
| 76 | **딱구리** | 2 | 2.5 | 3 | 15 |
| 77 | **포니타** | 1.5 | 2 | 1.5 | 22 |
| 78 | **날쌩마** | 1.5 | 2.5 | 2 | 25 |
| 79 | **야돈** | 2 | 1.5 | 1.5 | 15 |
| 80 | **야도란** | 2 | 2 | 2.5 | 15 |
| 81 | **코일** | 1 | 2 | 2 | 15 |
| 82 | **레어코일** | 1.5 | 3 | 3 | 22 22 | 
| 83 | **파오리** | 1.5 | 1.5 | 1.5 | 18 |
| 84 | **두두** | 1 | 2 | 1 | 22 |
| 85 | **두트리오** | 1.5 | 2.5 | 2 | 25 |
| 86 | **쥬쥬** | 1.5 | 2 | 2 | 15 |
| 87 | **쥬레곤** | 2 | 2 | 2 | 22 |
| 88 | **질퍽이** | 2 | 2 | 1.5 | 15 |
| 89 | **질뻐기** | 2.5 | 2.5 | 2 | 18 |
| 90 | **셀러** | 1 | 1.5 | 2.5 | 15 |
| 91 | **파르셀** | 1.5 | 2 | 3 | 22 |
| 92 | **고스** | 1 | 2.5 | 2.5 | 22 |
| 93 | **고우스트** | 1 | 2.5 | 2.5 | 22 |
| 94 | **팬텀** | 1.5 | 3 | 3 | 25 |
| 95 | **롱스톤** | 1 | 1 | 3 | 22 |
| 96 | **슬리프** | 1.5 | 2 | 2 | 15 |
| 97 | **슬리퍼** | 2 | 2.5 | 2.5 | 18 |
| 98 | **크랩** | 1 | 2.5 | 2 | 18 |
| 99 | **킹크랩** | 1.5 | 3 | 2.5 | 22 |
| 100 | **찌리리공** | 1 | 1.5 | 1.5 | 25 |
| 101 | **붐볼** | 1.5 | 2 | 2 | 30 |
| 102 | **아라리** | 1.5 | 1.5 | 2 | 15 |
| 103 | **나시** | 2 | 3 | 3 | 18 |
| 104 | **탕구리** | 1.5 | 1.5 | 2 | 15 |
| 105 | **텅구리** | 1.5 | 2 | 2.5 | 15 |
| 106 | **시라소몬** | 1.5 | 3 | 1.5 | 22 |
| 107 | **홍수몬** | 1.5 | 2.5 | 2 | 22 |
| 108 | **내루미** | 2 | 1.5 | 2 | 15 |
| 109 | **또가스** | 1 | 1.5 | 2 | 15 |
| 110 | **또도가스** | 1.5 | 2 | 3 | 18 |
| 111 | **뿔카노** | 2 | 2 | 2 | 15 |
| 112 | **코뿌리** | 2.5 | 3 | 3 | 15 |
| 113 | **럭키** | 3 | 2.5 | 2.5 | 18 |
| 114 | **덩쿠리** | 1.5 | 2.5 | 2.5 | 18 |
| 115 | **캥카** | 2.5 | 2 | 2 | 22 |
| 116 | **쏘드라** | 1 | 2 | 2 | 18 |
| 117 | **시드라** | 1.5 | 2 | 2 | 22 |
| 118 | **콘치** | 1 | 1.5 | 1.5 | 18 |
| 119 | **왕콘치** | 2 | 2 | 2 | 18 |
| 120 | **별가사리** | 1 | 2 | 2 | 22 |
| 121 | **아쿠스타** | 1.5 | 2.5 | 2.5 | 25 |
| 122 | **마임맨** | 1 | 2.5 | 2.5 | 22 |
| 123 | **스라크** | 2 | 2.5 | 2 | 25 |
| 124 | **루주라** | 1.5 | 2 | 2 | 22 |
| 125 | **에레브** | 1.5 | 2 | 2 | 25 |
| 126 | **마그마** | 1.5 | 2 | 2 | 22 |
| 127 | **쁘사이저** | 1.5 | 3 | 2.5 | 22 |
| 128 | **켄타로스** | 2 | 2.5 | 2 | 25 |
| 129 | **잉어킹** | 1 | 1 | 1.5 | 22 |
| 130 | **갸라도스** | 2 | 3 | 2.5 | 22 |
| 131 | **라프라스** | 3 | 2 | 2 | 18 |
| 132 | **메타몽** | 1 | 1 | 1 | 15 |
| 133 | **이브이** | 1.5 | 1.5 | 1.5 | 18 |
| 134 | **샤미드** | 3 | 2.5 | 2.5 | 18 |
| 135 | **쥬피썬더** | 1.5 | 2.5 | 2.5 | 30 |
| 136 | **부스터** | 1.5 | 3 | 2.5 | 18 |
| 137 | **폴리곤** | 1.5 | 2 | 2 | 15 |
| 138 | **암나이트** | 1 | 2 | 2.5 | 15 |
| 139 | **암스타** | 2 | 2.5 | 3 | 18 |
| 140 | **투구** | 1 | 2 | 2 | 18 |
| 141 | **투구푸스** | 1.5 | 2.5 | 2.5 | 22 |
| 142 | **프테라** | 2 | 2.5 | 1.5 | 30 |
| 143 | **잠만보** | 3 | 2.5 | 1.5 | 15 |
| 144 | **프리져** | 2 | 3 | 3 | 22 |
| 145 | **썬더** | 2 | 3 | 3 | 25 |
| 146 | **파이어** | 2 | 3 | 3 | 22 |
| 147 | **미뇽** | 1 | 1.5 | 1.5 | 18 |
| 148 | **신뇽** | 1.5 | 2 | 2 | 22 |
| 149 | **망나뇽** | 2 | 3 | 2.5 | 22 |
| 150 | **뮤츠** | 2.5 | 3 | 3 | 30 |
| 151 | **뮤** | 2.5 | 2.5 | 2.5 | 25 |

</details>

#### 3. 성장 및 도감 수집

* **도감 등록 및 사용:** 쓰러뜨린 **적 포켓몬**은 도감에 등록되어 이후 플레이 시 아군으로 사용할 수 있게 됩니다.
* **진화:** 전투에서 살아남은 **아군 포켓몬**은 승리 시 진화할 수 있습니다. (단, 이브이 계열은 진화 불가)

#### 4. 히든 스테이지 (Hidden Stage)

전투에서 아군 포켓몬 3마리 **모두 생존**한 상태로 승리하면 **히든 스테이지**가 잠금 해제됩니다.

* **히든 스테이지 위치:** 5-2, 8-2, 9-2, 그리고 Real-Final 스테이지가 존재합니다.

#### 5. 턴 순서 개념 및 게임 속도 조정

* **턴 순서:** 각 **세대**에 모든 포켓몬은 한 번씩 움직일 기회인 "턴"을 갖게 됩니다. 한 세대에서 **턴 순서는 스피드와 무관**하며, 세대가 시작할 때 **중심에서 먼 포켓몬**부터 턴을 부여받게 됩니다.
* **게임 속도 조정:** Gen 6 이후부터의 빠른 게임 진행을 위해 마찰력이 감소됩니다. 마찰 계수가 0.95 $\to$ **0.98**가 됩니다.

#### 6. 스테이지 유형

* **정규 스테이지 (Stage X):** 체육관 관장으로, 포켓몬 배치와 구성이 **고정**되어 있습니다.
* **야생 스테이지 (Stage X-1):** 야생 포켓몬이 **일정 범위 내에서 랜덤하게** 출현하며, 중복 방지 보정이 적용되어 다회차 플레이를 돕습니다.
* **히든 스테이지 (Stage X-2):** 이전 정규 스테이지에서 아군 포켓몬 3마리가 모두 생존하면, 특별한 포켓몬을 잡을 수 있는 히든 스테이지로 진입할 수도 있습니다.

#### 7. 151종 수집

진화, 히든 스테이지, 야생 포켓몬 사냥을 통해 **다회차 플레이**를 하면서 151종의 모든 포켓몬을 수집할 수 있습니다.

<details>
<summary>▶ 야생 스테이지 출현 포켓몬 확인하기</summary>

### 야생 스테이지별 몬스터 구성

* **Stage 2_1**: 캐터피, 뿔충이, 구구, 꼬렛, 깨비참, 아보
* **Stage 3_1**: 모래두지, 니드런♀, 니드런♂, 삐삐, 식스테일, 푸린, 주뱃, 뚜벅초, 파라스, 콘팡
* **Stage 4_1**: 디그다, 나옹, 망키, 가디, 발챙이, 캐시, 알통몬, 모다피, 왕눈해
* **Stage 6_1**: 포니타, 야돈, 파오리, 두두, 쥬쥬, 질퍽이, 셀러, 고스, 슬리프, 크랩
* **Stage 7_1**: 아라리, 탕구리, 시라소몬, 홍수몬, 내루미, 뿔카노, 럭키, 캥카, 쏘드라
* **Stage 8_1**: 콘치, 별가사리, 스라크, 루주라, 에레브, 쁘사이저, 켄타로스, 잉어킹, 라프라스
* **Stage 8_2**: 폴리곤, 암나이트, 투구, 프테라, 잠만보

</details>

#### 8. 공중날기

어떤 전설의 포켓몬을 포획하면, 공중을 날아다니며 랜덤 스테이지나 포켓몬 리그에 곧바로 방문할 수 있습니다. 도감을 채울 때 유용한 기능입니다.

---

### 🐛 버그 제보 및 문의

버그나 문제점은 아래 채널로 제보해 주시면 감사하겠습니다.

* GitHub Issue
* 이메일: 926kaul@gmail.com
* 소스코드: https://github.com/926kaul/Pokagi_Gamemaker

***

# 🇬🇧 English Version: Pokagi Readme

## 🥚 Pokagi: Type Effectiveness Physics Simulator

Pokagi is a unique physics-based collision (marbles/egg-smashing) game that combines the Pokémon Generation 1 (151 species) roster with a distinctive **physics engine and Type Effectiveness system**. A Pokémon's stats directly influence its collision properties, making strategic placement and type analysis key to victory.

---

### 🎮 Game System and Features

#### 1. Velocity After Collisions Linked to Type Effectiveness

The **Velocity** of Pokémon after a collision is determined by **Type Effectiveness**. Crucially, both Type 1 and Type 2 of the two colliding Pokémon are fully reflected in this calculation (based on the Gen 1 Type Chart).

* **Calculation Example:** If a Rock/Ground type attacks a Rock/Flying type:
    > $1.0 (\text{Rock} \to \text{Rock}) \times 0.5 (\text{Rock} \to \text{Ground}) \times 2.0 (\text{Ground} \to \text{Rock}) \times 0 (\text{Ground} \to \text{Flying}) = 0$
    > (Since the final result is 0, the collision is nullified.)

#### 2. Determining Pokémon's Physical Attributes

A Pokémon's physical attributes (Size, Mass, Speed) are classified into **1 to 5 tiers** based on their **Base Stats**, cut off at values of 50, 70, 100, and 120.

| Physical Attribute | Determination Base |
| :---: | :---: |
| **Size** | HP Tier |
| **Moving Mass** | $\text{max}(\text{Attack}, \text{Special})$ Tier |
| **Static Mass** | $\text{max}(\text{Defense}, \text{Special})$ Tier |
| **Max Speed** | Speed Tier |

#### 3. Growth and Pokedex Collection

* **Pokedex and Usage:** Defeated **enemy Pokémon** are registered in the Pokedex and become available for use as allies in subsequent runs.
* **Evolution:** Surviving **allied Pokémon** may evolve upon winning a battle. (Eevee and its evolutions cannot evolve.)

#### 4. Hidden Stages

A **Hidden Stage** may be unlocked if you win a regular stage with **all three allied Pokémon surviving**.

* **Hidden Stage Locations:** Hidden stages 5-2, 8-2, 9-2, and the Real-Final stage exist.

#### 5. Turn Order Concept and Game Speed Adjustment

* **Turn Order:** In each **Generation**, every Pokémon gets one turn to move. The **turn order is independent of the Speed stat** and is assigned at the start of a Generation, prioritizing the Pokémon **farthest from the center**.
* **Game Speed Adjustment:** For faster gameplay (similar to Gen 6 onwards), friction has been reduced. The friction coefficient has changed from 0.95 $\to$ **0.98**.

#### 6. Stage Types

* **Regular Stages:** Feature Gym Leaders with **fixed** Pokémon composition and placement.
* **Random Stages (-1, -2):** Feature wild Pokémon that appear **randomly** within a certain range (with a bias to prevent duplicates), encouraging multiple playthroughs.

#### 7. Collecting All 151 Species

Through evolution, hidden stages, and catching wild Pokémon, you can collect all 151 species across **multiple playthroughs**.

---

### 🐛 Bug Reporting and Inquiry

Please report any bugs or issues via the channels below:

* GitHub Issue
* Email: 926kaul@gmail.com
* Source Code: https://github.com/926kaul/Pokagi_Gamemaker
