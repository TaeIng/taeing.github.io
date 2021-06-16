---
layout: post
title: 프로그래머스 코딩테스트 연습 level1 신규 아이디 추천
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---


채점 결과: 성공!  
하지만 정규표현식을 이용한다면 더 간결한 코드를 작성할 수 있을 것

 <!--more-->

<h4>프로그래머스 코딩테스트 연습 level1 신규 아이디 추천</h4>

기업 코딩테스트는 저작권으로 인해 링크로 대체합니다.
[신규아이디 추천](https://programmers.co.kr/learn/courses/30/lessons/72410)


<h4>내가 쓴 답</h4>
```javascript


function solution(new_id) {
  let answer = '';
  
  const ableWord = '0123456789qwertyuiopasdfghjklzxcvbnm-_.'
  let ableId = [];
  
  // 1단계
  answer = new_id.toLowerCase();
  
  // 2단계
  for (let word of answer){
      if(ableWord.includes(word)){
          ableId.push(word);
      }
  };
  // 3단계
  for(let i=0; i<ableId.length; i++){
      if (ableId[i-1]=='.' && ableId[i]=='.'){
          ableId.splice(i,1);
          i = 0;
      }
  };
  
  // 4단계
  if (ableId[0]=='.')
      ableId.shift();
  if (ableId[ableId.length-1]=='.')
      ableId.pop();

  // 5단계
  if (ableId=='')
      ableId.push('a')
  
  // 6단계
  if (ableId.length>15)
      ableId.splice(15,ableId.length);
  if (ableId[ableId.length-1]=='.')
      ableId.pop();
  
  // 7단계
  if (ableId.length<3)
      ableId.push(ableId[ableId.length-1]);
  if (ableId.length<3)
      ableId.push(ableId[ableId.length-1]);
  
  // 마지막 문자열을 문자로 변환
    answer = ableId.join('');
    
  return answer;
}
```

2단계와 문자열 문자변환은 구글링을 통해 for문을 이용한 includes함수사용, join함수를 배워 해결하였다.


<h4>다른 사람의 풀이</h4>

```javascript
function solution(new_id) {
    const answer = new_id
        .toLowerCase() // 1
        .replace(/[^\w-_.]/g, '') // 2
        .replace(/\.+/g, '.') // 3
        .replace(/^\.|\.$/g, '') // 4
        .replace(/^$/, 'a') // 5
        .slice(0, 15).replace(/\.$/, ''); // 6
    const len = answer.length;
    return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
}
```

정규식 표현을 이용해 간결하게 표현하였다. 정규식 표현을 들어보기만 했지, 실제로 사용한 코드는 처음보았다. 코딩테스트 뿐만 아니라 클린코드를 위해 꼭 배워놓아야겠다.

```javascript
const regExp = /[\{\}\[\]\/?.,;:|\)*~`!^\-+<>@\#$%&\\\=\(\'\"]/gi; //  / /gi 의 의미: // 정규식표현 g: 모든 패턴에 대한 전역검색 i:대소문자 구분안함
if(regExp.test(Data)){  // test() ㅡ 찾는 문자열이 들어있는지 확인
  new_Data = Data.replace(regExp, "")}; // 찾은 특수 문자를 제거
let fruit = 'apple, banana, orange';
let replaced_fruit = fruit.replace('banana', 'tomato');
arr.join(separator) // 배열 arr을 문자열로 바꿈. separator는 문자열 사이마다 들어가는 구분자, defalt값이 , 이므로 없애려면 arr.join('')
```