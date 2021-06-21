---
layout: post
title: 네이버 부스트캠프 웹모바일 자가진단 코딩테스트
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---

가뿐하게는 아니지만 그래도 성공!
네이버 해설에서는 forEach, Map 등을 사용해 간결함과 범용성을 잡았다.

 <!--more-->

<h4>네이버 부스트캠프 웹모바일 자가진단 코딩테스트</h4>

[중복 숫자 찾기 함수구현](https://blog.naver.com/PostView.naver?blogId=boostcamp_official&logNo=221978031932&parentCategoryNo=&categoryNo=20&viewDate=&isShowPopularPosts=false&from=postList)


<h4>내가 쓴 답</h4>
```javascript

function solution(arr){

  let answer = [];
  let count = 0;
  let numbers = [...new Set(arr)].sort((a,b)=>a-b); // 정렬, 중복된 값 제거

  if(numbers.length == arr.length){ // 중복된 값이 없으면 -1 출력
    answer=[-1];
    return answer;
    }
    
  for(let num of numbers){
    for(let i=0;i<arr.length;i++){ // 중복된 값이 있는 경우 카운트 ++
      if(num == arr[i]){
        count ++;
      }
    }
    if(count>1){
      answer.push(count);
    }
    count=0;
  }
  return answer;
}
```

 Set을 이용해 중복된 값을 제거하고, 배열에서 중복된 값의 수를 찾아 answer배열에 푸쉬하는 방식으로 풀었다. 문제만 봤을 땐 쉽다고 생각했는데, 자잘한 실수가 있어 빙빙 돌아 풀었다..😂

<h4>부스트캠프 해설 1</h4>

[부스트캠프 해설](https://blog.naver.com/boostcamp_official/222388429782)

네이버 블로그에 소개된 자바스크립트 해설은 두가지 방식으로 풀었다. 

```javascript

function countOf(arr, value) { // 중복횟수를 계산하는 함수
  var count = 0;
  arr.forEach(element => {
    if(element == value) count++;
  });
  return count;
}

function solution(arr) {
  var answer = [];
  var set = new Set([]);
  arr.forEach( element => {
    if (set.has(element)) return; // 중복을 계산한 숫자 제외
    set.add(element); 
    count = countOf(arr, element); // 배열을 돌면서 같은 수를 set에 추가
    if (count > 1) answer.push(count); // 중복된 수 answer으로 푸쉬
  });
  if (answer.length == 0) answer.push(-1); // 중복된 값이 없으면 -1 푸쉬
  return answer;
}
```
forEach를 사용했다는 점과 함수를 추가적으로 사용했다는 점을 제외하면 거의 내 코드와 흡사하다. 개인적으로는 내 코드가 더 간결한 느낌이다 ㅎㅎ..  

*forEach()함수는 array.forEach(element => console.log(element)); 일때 array배열의 요소를 각각 실행해주는 방식이다.


<h4>부스트캠프 해설 2</h4>
```javascript
function solution(arr) {
  var answer = [];
  var map = new Map();
  arr.forEach( element => {
    if (map.has(element)){ // map이 arr의 요소를 갖고있다면 
        map.set(element, map.get(element) + 1); // map에 요소, 카운팅을 추가
    }
    else {
        map.set(element, 1); // map에 arr 요소가 없다면 map에 요소, 1 추가
    }
  });

  map.forEach( (value) => {
    if (value > 1) { // map의 값이 1보다 크다면 answer에 추가
      answer.push(value);
    }
  });
  if (answer.length == 0 ) answer.push(-1); // 중복된 값이 없으면 -1 추가
  return answer;
}
```
두번째 풀이방법은 Map을 이용해 중복횟수를 map에 담아 배열에 추가하는 형식이다. 어떤 수가 몇번 중복되었는지 쉽게 볼 수 있다는 장점이 있다. 간결성으로나 범용성으로나 내가 작성했던 코드보다 훨씬 좋은 코드라고 생각된다..
