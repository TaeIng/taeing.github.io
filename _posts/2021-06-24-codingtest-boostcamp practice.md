---
layout: post
title: 프로그래머스 코딩테스트 연습 level1 소수찾기
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---

코드를 검색하고 이해하고 작성하는데 6시간정도 걸린 것 같다.
풀긴 풀었지만 상처뿐인 성공

 <!--more-->

<h4>문제 설명</h4>


주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

제한사항
nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

입출력 예
nums: [1,2,3,4], [1,2,7,6,4]	result: 1, 4


<h4>내가 쓴 답</h4>

```javascript
function solution(nums) {
    let answer = 0;
    let sums = [];
    // 서로 다른 3개 고르기 조합
    const getCombination = function (arr, selectNum) {
        const result = [];
        if (selectNum===1) return arr.map(v=>[v]); 
        
        arr.forEach((fixed, index, array)=>{
            const rest = array.slice(index+1);
            const combinations = getCombination(rest, selectNum-1);
            const attached = combinations.map(combi=>[fixed, ...combi]);
            result.push(...attached);
        });
        return result;
    }
    // 조합의 합
    const C3 = getCombination(nums,3); 
    for (let i=0; i<C3.length; i++) {
        sums.push(C3[i][0]+C3[i][1]+C3[i][2]);
    }
    
    // 소수인지 확인
    for(let sum of sums){
        let isPrime = true;
        for(let j=3; j<sum; j++){
            if(sum % j ===0){
             isPrime = false;
            }
        }
        if(isPrime)
        answer ++;
    }
    
    return answer;
}
```
서로 다른 3가지를 고르는 것이 쉬울것이라 생각했다. for문을 덕지덕지 붙여 식을 만들었는데, 당최 어디서 발생하는지 모를 오류가 자꾸 발생했다. 이렇게 된거 지저분한 for문 대신 아예 조합을 공부해보기로 했다. 그리고 그 과정에서 머리를 몇번이나 쥐어뜯었는지 모르겠다...😭


<h4>조합</h4>

[춤추는 개발자 자바스크립트 순열과 조합 알고리즘](https://jun-choi-4928.medium.com/javascript%EB%A1%9C-%EC%88%9C%EC%97%B4%EA%B3%BC-%EC%A1%B0%ED%95%A9-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-21df4b536349)
```javascript
const getCombinations = function (arr, selectNumber) {
  const results = [];
  if (selectNumber === 1) return arr.map((value) => [value]); // 1개씩 택할 때, 바로 모든 배열의 원소 return

  arr.forEach((fixed, index, origin) => {
    const rest = origin.slice(index + 1); // 해당하는 fixed를 제외한 나머지 뒤
    const combinations = getCombinations(rest, selectNumber - 1); // 나머지에 대해서 조합을 구한다.
    const attached = combinations.map((combination) => [fixed, ...combination]); //  돌아온 조합에 떼 놓은(fixed) 값 붙이기
    results.push(...attached); // 배열 spread syntax 로 모두다 push
  });

  return results; // 결과 담긴 results return
}

const example = [1,2,3,4];
const result = getCombinations(example, 3);
console.log(result);
```
위 코드를 보는데, 모르는 것이 크게 3가지 있었다. forEach, map, 재귀함수

Array.forEach((Value,Index,Array) => { 함수 작성});
인수 순서대로 현재 값, 인덱스, 배열이며 필요하지 않은 것은 공란으로 두면 된다.
for문과 비슷하게 인수를 가지고 함수를 순회한다.

const Array1 = Array.map((Value,Index,Array) => { 함수 작성}); 
인수 순서대로 현재 값, 인덱스, 배열이며 필요하지 않은 것은 공란으로 두면 된다.
Map()과는 다른 함수이며, 함수의 결과를 통해 새로운 배열을 반환한다.

가장 머리아픈 부분은 const combinations = getCombinations(rest, selectNumber - 1); 부분이었다. 재귀함수를 통해 계속 반복되는 함수를 만드는 것인데, 아직도 완벽히 이해했다고는 할 수 없을 것 같다. 여러 재귀함수를 접하면서 공부하고 익숙해져야겠다.


<h4>시간단축 소수 구하기</h4>

[개미는뚠뚠딴 소수판별식](https://ant-programmer.tistory.com/2)

내가 작성했던 것처럼 단순하게 소수를 구할수도 있지만, 시간복잡도를 낮출 수 있는 방법들이 꽤 있었다. 아래는 루트를 이용한 소수판별법이다.
```javascript
function isPrime(num) {
  let result = false;
  if(num === 2)
  return true;

  for(let i = 2; i<=Math.floor(Math.sqrt(num)); i++){
    if(num % i === 0){
      result = false;
      break;
    }else result = true;
  }
  return result;
}
```
Math.aqrt() : 제곱근 반환  Math.floor(): 반올림

