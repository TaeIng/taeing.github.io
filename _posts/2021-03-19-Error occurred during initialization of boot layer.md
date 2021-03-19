---
layout: post
title: 자바 모듈 오류 Error occurred during initialization of boot layer 
author: 쓰는중
tags: [TIL]
excerpt_separator: <!--more-->
---

<h3>여러 클래스를 사용했을 때 Error occurred during initialization of boot layer 오류가 뜨나요? </h3>

<!--more-->

```
Error occurred during initialization of boot layer
java.lang.module.FindException: Error reading module: C:\Program Files\Workspace\study\JAVA\ch6\out\production\ch6
Caused by: java.lang.module.InvalidModuleDescriptorException: Tv.class found in top-level directory (unnamed package not allowed in module)

Process finished with exit code 1
```

이러한 오류가 생기는 이유는 module-info.java 때문인데, module-info.java 파일을 삭제하면 된다.

오류명을 열심히 구글링 해봤지만, 대부분 영어로 된 페이지에다가 해결방법도 맞지 않았다. 힘들게 고생하던 중 원인을 알게 되었는데, 프로젝트를 만들 때 module-info.java 생성을 하도록 체크해놔서 그렇다고 한다. 이러한 오류는 2019년 자바9에 추가된 자바 모듈 시스템 때문인데, 자바 모듈 시스템에 대한 자세한 내용은 [이 블로그](https://laughcryrepeat.tistory.com/45)를 참고하면 좋을 듯 하다. 자바 모듈 작성법을 알아내어 직접 수정해보려 했지만 자바 입문자로서 통 알아들을 수 없는 말들이 가득하기 때문에, 자바의 정석을 통해 어느정도 공부 후 다시 알아보려 한다.


