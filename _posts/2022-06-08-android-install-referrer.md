---
title: 'Android install referrer 설정하기'
date: 2022-06-08 20:51:00
categories: android
tags: install referrer android adb shell boradcast utm_source utm_campaign
comments: true
---




## install referrer 테스트
adb shell am broadcast -a com.android.vending.INSTALL_REFERRER -n com.onezlabs.tickl/.InstallReferrerReceiver --es referrer "utm_source=testSource&utm_medium=testMedium&utm_term=testTerm&utm_content=testContent&utm_campaign=testCampaign"