---
layout: post
title: 프로그래머스 코딩테스트 연습 level1 크레인 인형뽑기 게임
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---


채점 결과: 질문목록에서 테스트1,2 실패 원인을 찾고 성공!  
for문 종료시 i에 +1을 더하기 때문에, 0으로 설정하여도 1로 시작한다는 것이 문제였다.

 <!--more-->

<h4>프로그래머스 코딩테스트 연습 level1 크레인 인형뽑기 게임</h4>

문제가 길어 링크로 대체합니다.
[크레인 인형뽑기 게임](https://programmers.co.kr/learn/courses/30/lessons/64061)

입출력 예시
board = [[0,0,0,0,0],[0,0,1,0,3],[0,2,5,0,1],[4,2,4,4,2],[3,5,1,3,1]]
moves = [1,5,3,5,1,2,1,4]
return	= 4


<h4>내가 쓴 답</h4>
```javascript
function solution(board, moves) {
  var answer = 0;
  let basket = []

  for (i=0; i<moves.length; i++){
      for (j=0; j<board[0].length; j++){
        if(board[j][moves[i]-1]!==0){
        basket.push(board[j][moves[i]-1]);
        board[j][moves[i]-1] = 0;
        j = board[0].length;
        }
      }
    }
    console.log(basket);

for (i=0; i<basket.length; i++){
  if(basket[i]===basket[i+1]){
    basket.splice(i,2);
    answer += 2;
    i = 0;
  }
}
console.log(basket);
  return answer;
}
console.log(solution(board,moves));
```

테스트 1,2 실패 정답률 81.8

왜 안되는지 이해가 안가서 다른사람들의 질문목록을 뒤져봤다.  
1,2번 케이스가 해결이 안된 사람들이 많았는데, 그 원인은 기존 인형이 터뜨려지지 않는다는 것이다. 분명 나는 그런 케이스에 대한 코딩을 해놨는데 왜 문제가 생기는 것일까? 테스트케이스를 넣어보기 전까지는 원인을 찾지 못했다.

테스트 1,2번 실패시 테스트 1,2번 케이스는 이미 1개의 인형 a가들어잇고, 그위로 인형 b가 두개쌓여 사라진후 다음 입력으로 a가 들어왓을경우 a도 삭제시켜주는 예 같습니다. 다음케이스를 활용해보세요 
let board = [[0, 0, 1, 0, 0], [0, 0, 1, 0, 0], [0, 2, 1, 0, 0], [0, 2, 1, 0, 0], [0, 2, 1, 0, 0]];
const moves = [1, 2, 3, 3, 2, 3, 1];


<h4>내 풀이 수정</h4>

```javascript
function solution(board, moves) {
  var answer = 0;
  let basket = []

  for (i=0; i<moves.length; i++){
      for (j=0; j<board[0].length; j++){
        if(board[j][moves[i]-1]!==0){
        basket.push(board[j][moves[i]-1]);
        board[j][moves[i]-1] = 0;
        j = board[0].length;
        }
      }
    }
    console.log(basket);

for (i=0; i<basket.length; i++){
  if(basket[i]===basket[i+1]){
    basket.splice(i,2);
    answer += 2;
    i = -1; // 이 부분 수정 (i=0 -> i=-1)
  }
}
console.log(basket);
  return answer;
}
```

원인은 for문 종료시 i에 +1을 더하기 때문에 0으로 설정하여도 1로 시작한다는 것이 문제였다... 실수라고 하기도 뭐한게, 당연히 i=0으로 해두면 for문을 다시 시작할때 0으로 시작할 것이라 믿고 있었다. 천천히 배워가면 되지 뭐...😂
