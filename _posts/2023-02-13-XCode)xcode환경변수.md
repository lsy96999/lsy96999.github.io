---
layout: post
title:  "XCode)xcode 환경변수 설정 하기"
date:   2023-02-13 14:28:18 +0900
categories: xcode swift
---
xcode에서 ios 환경변수 설정하기

1)  Configuration Settings File을 생성한다.
![xcconfig생성](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/newfile_xcconfig.png)

2) 각환경별로 생성을한다(prd, dev). shared는  공통 변수 이다.
![dev](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcconfig_debugfile.png)

![prd](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcconfig_productfile.png)  

![shared](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcconfig_sharedfile.png)

#include 는 xcconfig를 import하는 구문이다.

첫번째 #include는 pod 프로젝트일경우, pod의 기본 debugxcconfig 세팅을 가져오기위해 추가했다.  
두번째 #inlcude는 shared.xcconfig로 prd, dev 환경에서 공통으로 사용할 변수를 선언한다.


3) debug, release 환경에서 사용할 xcconfig 설정하기 
![before](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcode_config_before_set.png)

![after](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcode_config_after_set.png)
Pod 프로젝트여서, 기본으로 Pods의 xcconfig가 잡혀있다.
Debug, Product xcconfig에 pods의 세팅을 include 했으니,  
Debug, Product 로 변경해준다.

4) info.plist 설정하기
![setInfoPlist](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcode_set_info.plist.png)
inpo.plist를 에서 xcconfig의 변수를 사용하기위해서 $()안에 xcconfig의 key를 적는다.

5) 소스상에서 info.plist를 출력한다.
![source](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/source.png)
{% highlight swift %}
Bundle.main.object(forInfoDictionary: "someVar") as! String
{% endhighlight %}

  
6) 스킴을 변경한다.
![editScheme](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcode_edit_schme.png)

![selectScheme](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/xcode_select_schme.png)


7) 결과를 확인한다.  
![dev_result](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/dev_profile.png)

![prd_result](/assets/images/xcode%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98/prd_profile.png)