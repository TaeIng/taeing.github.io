---
layout: post
title: 프로그래머스 코딩테스트 연습 level1 모의고사
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---


채점 결과: 성공!  
많은 연습과 경험을 통해 Math.max, filter 같은 함수들을 바로바로 사용할 수 있도록 해야겠다.

 <!--more-->

<h4>프로그래머스 코딩테스트 연습 level1 모의고사</h4>

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한 조건
시험은 최대 10,000 문제로 구성되어있습니다.
문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

입출력 예시
answers [1,2,3,4,5] , [1,3,2,4,2]	
return	[1] , [1,2,3]


<h4>내가 쓴 답</h4>
```javascript
function solution(answers) {
    var answer = [];

  let student1 = 0;
  let student2 = 0;
  let student3 = 0;
  
  const answers2 = [2,1,2,3,2,4,2,5];
  const answers3 = [3,3,1,1,2,2,4,4,5,5];

  for (i=0; i<answers.length; i++){
      if(answers[i] == i%5+1)
          student1 ++;
      if(answers[i]==answers2[i%8])
          student2 ++;
      if((answers[i])==answers3[i%10])
          student3 ++;
        }

  if(student1 > student2 && student1 >  student3){
    answer = [1]
  }
  if(student2 > student1 && student2 > student3){
    answer = [2]
  }
  if(student3 > student1 && student3 > student2){
    answer = [3]
  }
  if(student1 > student3 && student1 == student2){
    answer = [1,2]
  }
  if(student1 > student2 && student1 == student3){
    answer = [1,3]
  }
  if(student2 > student1 && student2 == student3){
    answer = [2,3]
  }
  if(student1 == student2 && student2 == student3 && student1 == student3){
    answer = [1,2,3]
  }

}
```
채점 결과: 성공

배열을 어떻게 해야할 지 생각나지 않아 하드코딩으로 풀었다. 아쉬움이 많이 남는다.


<h4>다른 사람의 풀이</h4>

```javascript
function solution(answers) {
    var answer = [];
    var a1 = [1, 2, 3, 4, 5];
    var a2 = [2, 1, 2, 3, 2, 4, 2, 5]
    var a3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

    var a1c = answers.filter((a,i)=> a === a1[i%a1.length]).length;
    var a2c = answers.filter((a,i)=> a === a2[i%a2.length]).length;
    var a3c = answers.filter((a,i)=> a === a3[i%a3.length]).length;
    var max = Math.max(a1c,a2c,a3c);

    if (a1c === max) {answer.push(1)};
    if (a2c === max) {answer.push(2)};
    if (a3c === max) {answer.push(3)};

    return answer;
}
```

max를 이용해 배열에 push하는 방식으로 쉽게 정렬하였다.
filter도 사용하였는데, filter를 쉽게 사용하기에는 많은 경험과 연습이 필요할 것 같다.

<h4>내 풀이 수정</h4>

```javascript
function solution(answers) {
  var answer = [];

  let student1 = 0;
  let student2 = 0;
  let student3 = 0;
  
  const answers1 = [1,2,3,4,5]
  const answers2 = [2,1,2,3,2,4,2,5];
  const answers3 = [3,3,1,1,2,2,4,4,5,5];

  for (i=0; i<answers.length; i++){
      if(answers[i] == answers1[i%answers1.length])
          student1 ++;
      if(answers[i]== answers2[i%answers2.length])
          student2 ++;
      if((answers[i])== answers3[i%answers3.length])
          student3 ++;
        }
  const max = Math.max(student1,student2,student3);
        
  if (student1 == max) {answer.push(1)}
  if (student2 == max) {answer.push(2)}
  if (student3 == max) {answer.push(3)}

  return answer
}
```

i%answers1.length로 코드를 좀 더 직관적으로 수정하였고, Math.max를 이용해 정렬을 간단하게 만들었다.
