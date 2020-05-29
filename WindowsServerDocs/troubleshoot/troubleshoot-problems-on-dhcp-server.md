---
title: DHCP 서버에서 발생 하는 문제 해결
description: 이 artilce는 DHCP 서버에서 발생 하는 문제를 해결 하 고 데이터를 수집 하는 방법을 소개 합니다.
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: ad70b03fcb6d703a0b99435ee8715319d09af941
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150201"
---
# <a name="troubleshoot-problems-on-the-dhcp-server"></a>DHCP 서버에서 발생 하는 문제 해결

이 문서에서는 DHCP 서버에서 발생 하는 문제를 해결 하는 방법을 설명 합니다.

## <a name="troubleshooting-checklist"></a>문제 해결 검사 목록

다음 설정을 확인합니다.

  - DHCP 서버 서비스가 시작 되어 실행 되 고 있습니다. 이 설정을 확인 하려면 **net start** 명령을 실행 하 고 **DHCP 서버**를 찾습니다.

  - DHCP 서버에 권한이 부여 됩니다. [도메인에 가입 된 시나리오의 WINDOWS DHCP 서버 권한 부여를](https://docs.microsoft.com/openspecs/windows_protocols/ms-dhcpe/56f8870b-a7c1-4db1-8a86-f69079fe5077)참조 하세요.

  - DHCP 클라이언트가 있는 서브넷의 DHCP 서버 범위에서 IP 주소 임대를 사용할 수 있는지 확인 합니다. 이렇게 하려면 DHCP 서버 관리 콘솔에서 해당 범위에 대 한 통계를 참조 하세요.

  - \_주소 임대에서 잘못 된 주소 목록을 찾을 수 있는지 여부를 확인 합니다.

  - 네트워크의 장치에 DHCP 범위에서 제외 되지 않은 고정 IP 주소가 있는지 확인 합니다.

  - DHCP 서버가 바인딩되어 있는 IP 주소가 IP 주소를 임대 해야 하는 범위의 서브넷 내에 있는지 확인 합니다. 릴레이 에이전트를 사용할 수 없는 경우에 발생 합니다. 이렇게 하려면 **DhcpServerv4Binding** 또는 **DhcpServerv6Binding** cmdlet을 실행 합니다.

  - DHCP 서버만 UDP 포트 67 및 68에서 수신 대기 하는지 확인 합니다. 다른 프로세스 또는 다른 서비스 (예: WDS 또는 PXE)는 이러한 포트를 점유 하지 않습니다. 이렇게 하려면 `netstat -anb` 명령을 실행 합니다.

  - IPsec 배포 환경을 처리 하는 경우 DHCP 서버 IPsec 예외가 추가 되었는지 확인 합니다.

  - 릴레이 에이전트 IP 주소를 DHCP 서버에서 ping 할 수 있는지 확인 합니다.

  - 구성 된 DHCP 정책 및 필터를 열거 하 고 확인 합니다.

## <a name="event-logs"></a>이벤트 로그

관찰 된 문제와 관련 된 문제를 보고 하려면 시스템 및 DHCP 서버 서비스 이벤트 로그 (**응용 프로그램 및 서비스 로그** \> **Microsoft** \> **Windows** \> **DHCP 서버**)를 확인 합니다.  
문제 종류에 따라 이벤트는 다음 이벤트 채널 중 하나에 기록 됩니다.  
[DHCP 서버 작동 이벤트](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP 서버 관리 이벤트](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP 서버 시스템 이벤트](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP 서버 필터 알림 이벤트](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP 서버 감사 이벤트](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))

## <a name="data-collection"></a>데이터 수집

### <a name="dhcp-server-log"></a>DHCP 서버 로그

DHCP 서버 서비스 디버그 로그에는 DHCP 서버에서 수행 하는 IP 주소 임대 할당 및 DNS 동적 업데이트에 대 한 자세한 정보가 제공 됩니다. 이러한 로그는 기본적 으로% windir% \\ System32 Dhcp에 있습니다 \\ .  
자세한 내용은 [DHCP 서버 로그 파일 분석](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd183591\(v=ws.10\))을 참조 하세요.

### <a name="network-trace"></a>네트워크 추적

상관 관계 네트워크 추적은 이벤트가 기록 된 시간에 DHCP 서버가 수행 하는 작업을 나타낼 수 있습니다. 이러한 추적을 만들려면 다음 단계를 수행 합니다.

1.  [GitHub](https://github.com/CSS-Windows/WindowsDiag/tree/master/ALL/TSS)로 이동 하 여 [tss \_ tools .zip](https://github.com/CSS-Windows/WindowsDiag/blob/master/ALL/TSS/tss_tools.zip) 파일을 다운로드 합니다.

2.  Tss \_ tools .zip 파일을 복사 하 고이를 로컬 디스크의 위치 (예: C: tools 폴더)로 확장 \\ 합니다.

3.  \\관리자 권한 명령 프롬프트 창에서 C: tools의 다음 명령을 실행 합니다.  
    ```console
    TSS Ron Trace <Stop:Evt:>20321:<Other:>DhcpAdminEvents NoSDP NoPSR NoProcmon NoGPresult
    ```
      
    >[!Note]
    >이 명령에서 및를 \<*Stop:Evt:*\> \<*Other:*\> 추적 세션에서 포커스를 볼 이벤트 ID 및 이벤트 채널로 바꿉니다.  
    >Tss \_ \_ tools .zip 파일에 포함 된 tss .cmd 추가 \_ 정보는 사용 가능한 모든 설정에 대 한 자세한 정보를 제공 합니다.

4.  이벤트가 트리거된 후이 도구는 C: MS DATA 라는 폴더를 만듭니다 \\ \_ . 이 폴더에는 컴퓨터의 네트워크 및 도메인 구성에 대 한 일반 정보를 제공 하는 몇 가지 유용한 출력 파일이 포함 되어 있습니다.  
    이 폴더에서 가장 흥미로운 파일 은% Computername% \_ date \_ time \_ packetcapture \_ internetclient \_ dbg. etl입니다.
    [네트워크 모니터](https://www.microsoft.com/download/4865) 응용 프로그램을 사용 하 여 파일을 로드 하 고 "DHCP 또는 DNS" 프로토콜에 표시 필터를 설정 하 여 백그라운드에서 진행 되는 작업을 확인할 수 있습니다.
