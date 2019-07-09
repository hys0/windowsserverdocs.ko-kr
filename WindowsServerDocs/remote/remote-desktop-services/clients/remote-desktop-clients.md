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
ms.openlocfilehash: 341262243b5bbe8ed046382d7490a6e5c39b8965
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66188128"
---
# <a name="remote-desktop-clients"></a>원격 데스크톱 클라이언트

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Microsoft 원격 데스크톱 클라이언트를 사용하여 어떤 디바이스를 사용하는 거의 모든 위치에서 원격 PC 및 회사 리소스에 연결할 수 있습니다. 작업 PC에 연결하여 책상에 앉아 있는 것처럼 모든 앱, 파일 및 네트워크 리소스에 액세스할 수 있습니다. RD 클라이언트를 사용하여 회사에 앱을 열어 두고 집에서 동일한 앱을 볼 수도 있습니다.

시작 하기 전에 반드시 체크 아웃의 [지원 되는 구성](remote-desktop-supported-config.md) 문서에서는 원격 데스크톱 클라이언트를 사용 하 여 연결할 수 있는 Pc에 논의 합니다. [클라이언트 FAQ](remote-desktop-client-faq.md)도 확인하십시오.

사용할 수 있는 클라이언트 앱은 다음과 같습니다.

| 장치   | 앱 가져오기                                                                                                     | 설치 지침                                                                |
|----------|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Windows  | [Microsoft Store의 Windows 10 클라이언트](https://go.microsoft.com/fwlink/?LinkID=616709)                      | [Windows에서 원격 데스크톱 클라이언트 시작](windows.md)                |
| Android  | [Google Play의 Android 클라이언트](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)        | [Android에서 원격 데스크톱 클라이언트 시작](remote-desktop-android.md) |
| iOS      | [iTunes 스토어의 iOS 클라이언트](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)     | [iOS에서 원격 데스크톱 클라이언트 시작](remote-desktop-ios.md)         |
| macOS    | [iTunes 스토어의 macOS 클라이언트](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12) | [Mac에서 원격 데스크톱 클라이언트 시작](remote-desktop-mac.md)         |

## <a name="configuring-the-remote-pc"></a>원격 PC 구성

원격 액세스하기 전에 원격 PC를 구성하려면 [PC에 대한 액세스를 허용](remote-desktop-allow-access.md)합니다.

## <a name="remote-desktop-client-uri-scheme"></a>원격 데스크톱 클라이언트 URI 체계

리소스 URI (Uniform Identifier) 체계를 사용 하 여 플랫폼 간에 원격 데스크톱 클라이언트의 기능을 통합할 수 있습니다. 체크 아웃 된 [지원 되는 URI 특성](remote-desktop-uri.md) iOS, Mac 및 Android 클라이언트에 사용할 수 있는 합니다.
