---
title: 'adb command'
date: 2021-12-25 01:00:00
categories: Marketing
tags: adb command android
comments: true
---



./adb -s R3CR90PZD8Y install /Users/aron/projects/NCTMarketing/eco-pedometer/build/app/outputs/flutter-apk/app-release.apk
./adb -s ce03160390ae063203 install /Users/aron/projects/NCTMarketing/eco-pedometer/build/app/outputs/flutter-apk/app-release.apk





./adb -s R3CR90PZD8Y shell ps -ef | grep com.nct.eco
./adb -s R3CR90PZD8Y shell logcat --pid=8050


./adb -s ce03160390ae063203 shell ps -ef | grep com.nct.eco
./adb -s ce03160390ae063203 shell logcat --pid=10709



shell am broadcast -a com.android.vending.INSTALL_REFERRER -n com.nct.v/com.nct.v.InstallReferrer --es "referrer"--es "referrer" "utm_source=test_source&utm_medium=test_medium&utm_term=utm_test&utm_content=test_content&utm_campaign=test_name"


./adb shell am broadcast -a com.android.vending.INSTALL_REFERRER -n com.nct.v/com.nct.v.InstallReferrer --es "referrer"--es "referrer" "utm_source=test_source&utm_medium=test_medium&utm_term=utm_test&utm_content=test_content&utm_campaign=test_name"


adb shell am broadcast -a com.android.vending.INSTALL_REFERRER --es referrer hello



./adb shell am broadcast -a com.android.vending.INSTALL_REFERRER -n com.nct.v/.util.broadcast_receivers.FacadeBroadcastReceiver --es "referrer" "utm_source=test_source\&utm_medium=test_medium\&utm_term=test_term\&utm_content=test_content\&utm_campaign=test_name"



