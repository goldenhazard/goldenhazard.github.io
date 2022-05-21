---
layout: post
title: "[GTSAM] Lie Group"
toc: true
categories: slam
---

### Abstract
GTSAM 위주의 Lie group 이야기를 나름대로의 해석을 얹어 정리해보고자 한다.

### References
(1) [Micro Lie theory - Joan Sola](https://arxiv.org/abs/1812.01537)
(2) [Lie Group - Frank Dallaert](https://github.com/borglab/gtsam/blob/develop/doc/LieGroups.pdf)
(3) [Lie Group - Waterloo Lecslide](http://t-robotics.blogspot.com/2015/07/lie-group-formulation-for-robot.html#.YgTQxN9BxPY)

### Introduction
필자는 사실 Frank Park 교수님의 introduction to robotics 수업을 들었지만, Lie group이라는 것이 정확히 무엇인지 무지몽매했다. (benighted, gre) 하지만, slam의 visual-inertial-odometry 연구에 한 획을 그은 `imu preintegration` 논문을 이해하려면, 반드시 lie group에 대한 이해가 필요하다. 이 논문 이후로, `slam`에서 pose나 orientation을 다룰 때의 표준이 lie group을 차용하는 것으로 바뀌었다고 봐도 무방하다.

### Lie Group : Intersection of manifold and group
Lie group은 differential manifold면서 동시에 group의 성질을 가지고 있는 집합을 의미한다. 실제로 gtsam의 `base` 폴더를 확인해보면 lie group은 `manifold`와 `group`의 두가지 category tag를 상속받고 있다. GTSAM은 각 category별로 필요한 traits를 따로 정의해두어, 이를 상속받는 class에서 해당 메소드를 반드시 구현하도록 설정해 놓았다. 이를 먼저 살펴보고 들어가자. <br><br>

***
`Group`은 반드시 다음 4가지 함수를 구현해야 한다.
- `Identity()`
- `Compose(g, h)`
- `Between(g, h)`
- `Inverse(g)`

***
예를 들어 `Rot3` 객체를 살펴보자.

비슷하게, Frank Dallaert는 `new imu factor`에서 `NavSat`이라는 새로운 상태변수를 정의하여, 이를 구현하였다. 이를 자유자재로 다룰 필요가 있는 듯 하다. 해당 코드를 뜯어보는 것이 GTSAM 기본 자료형의 이해에 큰 도움이 될 것이다.

### Lie Group : Useful Formula
1. Adjoint
2. BCH Formula
3. First-order linearization in `Exp`
4. First-order linearization in `Log`
5. Retraction

### Question
1. 그래서 누군가 필자에게 "그래서 pose를 나타낼 때 왜 lie group을 사용하는가?"라고 물어본다면 아직 정확하게 답하지 못할 것 같다. 필자 스스로 내린 결론은, 그 것이 수학적으로 차용되는 많은 테크닉을 얻을 수 있기 때문이다 라는 것이다. 아직 한참 부족한 답변이므로, 이 포스팅을 마무리할 쯤에는 나름대로의 깨달음이 있었으면 한다.