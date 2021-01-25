---
layout: post
title: 깃허브 블로그 잔디가 안심어질 때
hide_title: true
feature-img: assets/img/feature-img/github-fork.jpg
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---

<h3>혹시 Jekyll 블로그 테마를 받아오시지 않으셨나요?</h3>

<!--more-->

> **깃허브 Contributions(잔디심기) 안되는 이유**
>
> 1. github에 등록된 email과 local에 등록된 email이 다른 경우
> 2. merge한 branch가 master(main) branch가 아닐 때
> 3. fork 된 프로젝트 일 경우

며칠째 깃허브 잔디가 심어지지 않고 있었다. 조금 기다리면 되겠지 라는 생각이었지만, 비어가는 잔디밭을 보니 불안하고 가슴 한 켠이 답답했다. 탈모가 이런 기분일까.

급하게 구글링을 해본 결과, 대부분 **github에 등록된 email과 local에 등록된 email이 다른 경우,** 그리고 **merge한 branch가 master(main) branch가 아닐 때** 생기는 오류라고 하였다.

그러나 branch도 확인해보고, 깃허브 홈페이지의 이메일과 `$ git config --list` 를 통해 확인해 보았지만 전혀 이상이 없었다.

한참을 더 끙끙거리며 검색해보니 fork된 프로젝트의 경우 잔디가 안심어진다는 해결방안을 찾게 되었다.

사전지식없이 깃허브 블로그를 처음 만들어보는 입장이라면, 마음에 드는 Jekyll테마를 fork한 뒤 Repository name을 바꿔서 제작하신 분들이 많을 거라 생각한다.

나의 경우, 기존의Github desktop을 이용해 새로운 _name.github.io_ 폴더를 만든 후, 기존 블로그 파일을 옮겨 넣는 식으로 문제를 해결하였다.
