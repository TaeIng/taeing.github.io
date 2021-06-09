---
layout: post
title: 프로그래머스 코딩테스트 연습 level1 체육복
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---


채점 결과: 91.7 / 100   <span style="color:red"> 테스트 12 실패</span>  
내가 볼 땐 틀린 부분이 없어보이는데 자꾸 테스트 12를 통과하지 못한다...

 <!--more-->

<h4>프로그래머스 코딩테스트 연습 level1 체육복</h4>

[링크](https://programmers.co.kr/learn/courses/30/lessons/42862)
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

제한사항
전체 학생의 수는 2명 이상 30명 이하입니다.
체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

입출력 예시: n = 5	lost = [2, 4] reserve =	[1, 3, 5]	return =5

<h4>내가 쓴 답</h4>
```javascript
function solution(n, lost, reserve) {
  var answer = n - lost.length;
  
  for(lostS of lost){
      if (reserve.includes(lostS)) {
          answer ++;
          reserve.splice(reserve.indexOf(lostS),1);
          }
      else if (reserve.includes(lostS-1)) {
          answer ++;
          reserve.splice(reserve.indexOf(lostS-1),1);
          }
      else if (reserve.includes(lostS+1)) {
          answer ++;
          reserve.splice(reserve.indexOf(lostS+1),1);
          }
       }
  return answer;
}
```
채점 결과: 91.7 / 100, 테스트 12 실패

내가 볼 땐 틀린 부분이 없어보이는데 자꾸 테스트 12를 통과하지 못한다...



<h4>다른 사람의 풀이</h4>

```javascript
function solution(n, lost, reserve) {
  let answer = n;

  for (let i = 0; i < reserve.length; i++) { // 여벌 체육복
    if (lost.includes(reserve[i])) { // 체육복을 도난맞은 학생이 여벌 체육복이 있다면
      lost.splice(lost.indexOf(reserve[i]), 1); // 도난 체육복에서 여벌 체육복 제외
      reserve.splice(i, 1); // 여벌 체육복 제외
      i--; // reserve.length가 줄어드므로 i--;
    }
  }

  for (let i = 0; i < reserve.length; i++) { 
    if (lost.includes(reserve[i] - 1)) {
      lost.splice(lost.indexOf(reserve[i] - 1), 1);
      reserve.splice(i, 1);
      i--;
    } else if (lost.includes(reserve[i] + 1)) {
      lost.splice(lost.indexOf(reserve[i] + 1), 1);
      reserve.splice(i, 1);
      i--;
    }
  }
  answer = n - lost.length;
  return answer;
}
```
내 풀이와 차이점은 여벌 체육복을 통해 도난 체육복을 뺀 점,[i]를 이용한 점이다.

논리적으로 어떤 부분에서 틀린 것인지 알아보기 위해 for(reserveS of reserve)으로도 풀어봤지만 풀리지 않는다...

기존에 풀었던 풀이가 어디서 잘못된건지는 여전히 모르겠다 ㅠㅠ
