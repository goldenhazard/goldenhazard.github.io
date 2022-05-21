---
layout: post
title: First long project "GTSAM"
toc: true
categories: slam
---

### [Abstract]
나의 첫 장기 프로젝트이다. GTSAM에 대해서 배경적 이론(Lie Group, Optimization, Factor graph)부터 gtsam 컨셉 design, gtsam 코드분석, 마지막으로 gtsam의 하나의 새로운 factor를 개발한다고 가정했을 때의 절차를 마지막으로 하겠다. 굉장히 긴 프로젝트가 될 것 같으므로, 업데이트 속도가 늦을 수도 있다.
Factor graph 기반으로 slam 연구를 진행하려는 초보 연구자들에게 조금이나마 도움이 되었으면 좋겠다.

### Index
1. What is factor graph?
2. Hierarchy of gtsam
3. [Lie Group]({% post_url 2022-02-10-gtsam-liegroup.md %})
4. [Code]