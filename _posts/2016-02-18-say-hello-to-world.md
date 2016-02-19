---
layout: post
title: 'Say hello to world!'
date: 2016-02-18T12:38:00.000Z
---

# Hello World!

```
#include <stdio.h>

int main(int argc, char* argv[]){
  if(argc != 2){
    printf("app error: argv is error!\r\n");
    printf("usage: %s <say something>\r\n", argv[0]);
  }
  else{
    printf("%s\r\n", argv[1]);
  }
}
```

## Just with the codes
