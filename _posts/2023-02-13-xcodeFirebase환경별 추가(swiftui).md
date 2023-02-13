---
layout: post
title:  "xcode Firebase 환경별 추가(swiftui)"
date:   2023-02-13 14:28:18 +0900
categories: xcode
---

swiftui firebase 환경별로 추가하기

1. firebase 콘솔로부터, GoogleService-info.plist를 받아서 prd,dev분리한다.
![dev_prd_set](/assets/images/xcodeFirebase%ED%99%98%EA%B2%BD%EB%B3%84/firebase-dev_prd_set.png)

2. BundleResources에 GoogleService-info.plist를 추가해준다.(prd, dev)
![set_bundle](/assets/images/xcodeFirebase%ED%99%98%EA%B2%BD%EB%B3%84/firebase_info_set_bundle_resource.png)

3. AppDelegate에서 #if DEBUG 전처리 조건문으로 분기하여 환경에 맞게 
GoogleService-info.plist를 넣어준다.
![app_delegate](/assets/images/xcodeFirebase%ED%99%98%EA%B2%BD%EB%B3%84/firebase_add_app_delegate.png)