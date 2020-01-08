---
title: "cors란?"
date: 2020-01-07T01:53:51+09:00
categories: ["web"]
tags: ["term"]
---
## cross-domain
웹 개발 이슈 중 하나이며 **현재 도메인에서 다른 도메인의 리소스를 요청하는 것을 말한다.** 자바스크립트 같은 경우 보안상의 이유로 cross-origin을 제한한다. 이 제한을 Same Origin Policy(동일 출처 정책)이라고도 하며 보호된 영역에서만 프로그램이 동작하도록 한다고해서 샌드박스라고도 불린다.

## cross-origin resource sharing
상당수의 웹 서버는 하나의 도메인만으로 모든 처리를 하기에는 효율성이나 성능등 여러 문제가 발생할 수 있어 각 기능별로 여러 서버를 두는 경우가 있다. 이러한 cross domain의 해결 방안으로 **CORS**를 서버단에서 허용해준다.

## Access-Control-Allow-Origin
cors를 허용해주는 가장 간단한 방법은 서버의 응답 헤더에 **Access-control-Allow-Origin** 프로퍼티를 추가해주는 것이다.

    Access-Control-Allow-Origin: *
    or
    Access-Control-Allow-Origin: http://goooogle.com, ....

## Express 프레임워크에서 허용

    app.use(require('cors'))

    or

    app.all('/*',(req,res,next)=>{
        res.header("Access-Control-Allow-Origin", "*");
        res.header("Access-Control-Allow-Headers", "X-Requested-With");
        next();    
    })