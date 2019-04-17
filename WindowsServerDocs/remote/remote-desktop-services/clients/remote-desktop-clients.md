---
title: 원격 데스크톱 클라이언트
description: 모든 디바이스에서 사용할 수 있는 다양한 원격 데스크톱 클라이언트 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7d8158c-aee1-4c60-8a46-40ce5595b8e8
author: HeidiLohr
manager: dougkim
ms.author: helohr
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 28e41595c3f18f5960a05fd9aecf8d54fc6c35bc
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297343"
---
# 원격 데스크톱 클라이언트

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Microsoft 원격 데스크톱 클라이언트를 사용하여 어떤 장치를 사용하는 거의 모든 위치에서 원격 PC 및 회사 리소스에 연결할 수 있습니다. 작업 PC에 연결하여 책상에 앉아 있는 것처럼 모든 앱, 파일 및 네트워크 리소스에 액세스할 수 있습니다. RD 클라이언트를 사용하여 회사에 앱을 열어 두고 집에서 동일한 앱을 볼 수도 있습니다.

시작하기 전에 반드시 [지원되는 구성](remote-desktop-supported-config.md) 문서를 확인하십시오. 이 문서에는 원격 데스크톱 클라이언트를 사용하여 연결할 수 있는 PC에 대해서 설명되어 있습니다. [클라이언트 FAQ](remote-desktop-client-faq.md)도 확인하십시오.

사용할 수 있는 클라이언트 앱은 다음과 같습니다.

| 장치   | 앱 가져오기                                                                                                     | 설치 지침                                                                |
|----------|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Windows  | [Microsoft Store의 Windows 10 클라이언트](https://go.microsoft.com/fwlink/?LinkID=616709)                      | [Windows에서 원격 데스크톱 클라이언트 시작](windows.md)                |
| Android  | [Google Play의 Android 클라이언트](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)        | [Android에서 원격 데스크톱 클라이언트 시작](remote-desktop-android.md) |
| iOS      | [iTunes 스토어의 iOS 클라이언트](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)     | [iOS에서 원격 데스크톱 클라이언트 시작](remote-desktop-ios.md)         |
| macOS    | [iTunes 스토어의 macOS 클라이언트](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12) | [Mac에서 원격 데스크톱 클라이언트 시작](remote-desktop-mac.md)         |


## 원격 PC 구성

원격 액세스하기 전에 원격 PC를 구성하려면 [PC에 대한 액세스를 허용](remote-desktop-allow-access.md)합니다.

## 원격 데스크톱 클라이언트 URI 스키마
리소스 URI(Uniform Identifier) 체계를 사용하여 플랫폼 간에 원격 데스크톱 클라이언트의 기능을 통합할 수 있습니다. iOS, Mac 및 Android 클라이언트에서 사용할 수 있도록 [지원 되는 URI 특성](remote-desktop-uri.md)을 확인하십시오.
