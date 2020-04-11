---
title: 클라이언트에서 연결할 수 없고 "클래스가 등록되지 않았습니다" 오류가 발생함
description: 원격 데스크톱 연결과 관련된 "클래스가 등록되지 않았습니다" 오류를 해결합니다.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 52e696bd4229b947ea63a379211192b8664a9f93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857186"
---
# <a name="clients-cant-connect-and-get-the-class-not-registered-error"></a>클라이언트에서 연결할 수 없고 "클래스가 등록되지 않았습니다" 오류가 발생함

Windows 10 버전 1709 이상을 실행하는 클라이언트를 사용하여 원격 컴퓨터에 연결하려고 하면, 원격 데스크톱 세션 호스트 서버에서 "클래스가 등록되지 않았습니다(0x80040154)" 오류 코드가 포함된 메시지를 보고하는 동안 클라이언트가 연결되지 않을 수 있습니다.

이 문제는 연결하려는 사용자에게 필수 사용자 프로필이 있는 경우에 발생합니다. 이 이슈를 해결하려면 [2018년 7월 24일 - KB4338817(OS 빌드 16299.579)](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) Windows 10 업데이트를 설치합니다.
