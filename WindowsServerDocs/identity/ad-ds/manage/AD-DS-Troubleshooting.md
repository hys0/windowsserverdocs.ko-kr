---
ms.assetid: fd3bc84a-48eb-4f00-9dc2-846bf2c2668b
title: AD DS 문제 해결
description: AD DS에 대 한 문제 해결 섹션 개요
ms.author: joflore
author: MicrosoftGuyJFlo
manager: dcscontentpm
ms.date: 11/22/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b9e1cf812234bc3b0bd81db7045ed83208f3a0ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824366"
---
# <a name="ad-ds-troubleshooting"></a>AD DS 문제 해결

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

이 섹션에서는 Active Directory 복제 중 발생할 수 있는 문제를 진단 하 고 해결 하기 위한 문제 해결 권장 사항 및 절차를 제공 합니다. 디렉터리 서비스 이벤트 로그 항목에 응답 하는 방법과 Repadmin.exe와 같은 도구가 보고 하는 메시지를 해석 하는 방법에 중점을 둘 수 있습니다.

Windows Server 2012 R2 이상 버전을 실행 하는 모든 도메인 컨트롤러에서 repadmin.exe 및 Dcdiag.exe를 사용할 수 있습니다. 이러한 도구를 사용 하 여 문제를 해결 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [Active Directory 문제 해결을 위한 컴퓨터 구성](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)
- [Active Directory 복제 문제 해결](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)

또 다른 유용한 기술은 ETW (ETW(Windows용 이벤트 추적))입니다. ETW를 사용 하 여 도메인 컨트롤러 간의 LDAP 통신 문제를 해결할 수 있습니다. 자세한 내용은 [ETW를 사용 하 여 LDAP 연결 문제 해결](../manage/troubleshoot/troubleshoot-ldap-using-etw.md)을 참조 하세요.

Windows 10을 실행 하는 구성원 서버에 원격 서버 관리 도구 (RSAT)를 설치할 수도 있습니다. RSAT를 설치 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)를 참조 하세요.
