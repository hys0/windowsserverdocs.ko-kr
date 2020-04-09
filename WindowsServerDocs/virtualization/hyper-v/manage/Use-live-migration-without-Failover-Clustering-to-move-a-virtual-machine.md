---
title: 가상 컴퓨터를 이동 하려면 장애 조치 클러스터링이 없는 실시간 마이그레이션 사용
description: 독립 실행형 환경에서 실시간 마이그레이션을 수행 하기 위한 필수 구성 요소 및 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 75c32e42-97f7-48df-aac9-1d82d34825e1
author: kbdazure
ms.author: kathydav
ms.date: 01/17/2017
ms.openlocfilehash: 41d5edb02d4384955e711024d4e4d68cee5d3937
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858926"
---
# <a name="use-live-migration-without-failover-clustering-to-move-a-virtual-machine"></a>가상 컴퓨터를 이동 하려면 장애 조치 클러스터링이 없는 실시간 마이그레이션 사용

>적용 대상: Windows Server 2016

이 문서에서는 장애 조치 클러스터링을 사용 하지 않고 실시간 마이그레이션을 수행 하 여 가상 컴퓨터를 이동 하는 방법을 보여 줍니다. 실시간 마이그레이션 눈에 띄는 가동 중지 시간 없이 Hyper-v 호스트 간에 실행 중인 가상 컴퓨터를 이동합니다.   
  
이 작업을 수행할 수, 다음이 필요 합니다.   

- 로컬 Hyper-v Administrators 그룹 또는 소스와 대상 컴퓨터에서 Administrators 그룹의 구성원 인 사용자 계정입니다. 
  
- 원본 및 대상 서버에 설치 된 Windows Server 2016 또는 Windows Server 2012 r 2의 Hyper-v 역할이 며 실시간 마이그레이션에 대해 설정 됩니다. 가상 컴퓨터가 버전 5 이상인 경우 Windows Server 2016 및 Windows Server 2012 r 2를 실행 하는 호스트 간에 실시간 마이그레이션을 수행할 수 있습니다.

    버전 업그레이드 지침은 [windows 10 또는 Windows Server 2016에서 hyper-v의 가상 머신 버전 업그레이드](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)를 참조 하세요. 설치 지침은 [실시간 마이그레이션을 위한 호스트 설정](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)을 참조 하세요.

- 도구는 원본 또는 대상 서버에 설치 되어 있지 않으면 Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에 설치 된 Hyper-v 관리 도구에서에서 실행 합니다.  
   
## <a name="use-hyper-v-manager-to-move-a-running-virtual-machine"></a>Hyper-v 관리자를 사용 하 여 실행 중인 가상 컴퓨터를 이동 하려면  
  
1.  Hyper-V 관리자를 엽니다. (서버 관리자에서 클릭 **도구** >>**Hyper-v 관리자**.)  
  
2.  탐색 창에서 서버 중 하나를 선택 합니다. (이 나열 되어 있지 않으면 단추로 **Hyper-v 관리자**, 클릭 **서버에 연결**, 서버 이름을 입력 하 고 클릭 **확인**합니다. 서버를 더 추가 반복 합니다.)  
  
3.  **가상 컴퓨터** 창, 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 클릭 **이동**합니다. 이동 마법사를 엽니다. 
  
4.  마법사 페이지를 사용 하 여 이동, 대상 서버 및 옵션의 유형을 선택 합니다.
  
5.  **요약** 페이지에서 선택 사항을 검토한 다음 **마침**을 클릭합니다.  

## <a name="use-windows-powershell-to-move-a-running-virtual-machine"></a>Windows PowerShell을 사용 하 여 실행 중인 가상 컴퓨터를 이동 하려면
  
다음 예제에서는 명명 된 가상 컴퓨터를 이동 하려면 MOVE-VM cmdlet를 사용 하 여 *LMTest* 라는 대상 서버로 *TestServer02* 가상 하드 디스크 및 기타 파일, 이러한 검사점 및 스마트 페이징 파일을 이동 하 고는 *D:\LMTest* 대상 서버에서 디렉터리입니다.  
  
```  
PS C:\> Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest  
```  
  
## <a name="troubleshooting"></a>문제 해결

### <a name="failed-to-establish-a-connection"></a>연결을 설정 하지 못했습니다. 

제한 된 위임의 설정 하지 않은 경우에 로그인 해야 원본 서버에 가상 컴퓨터를 이동할 수 있습니다. 이렇게 하지 않으면 인증 시도가 실패 하면 오류가 발생 하 고이 메시지가 표시 됩니다.  
  
"마이그레이션 원본에서 가상 컴퓨터 마이그레이션 작업이 실패 했습니다.  
호스트와의 연결을 설정 하지 못했습니다 *컴퓨터 이름*: 자격 증명이 없는 0x8009030E 보안 패키지에서 사용할 수 있습니다. "
  
 이 문제를 해결 하려면 원본 서버에 로그인 하 고 이동 다시 합니다. 실시간 마이그레이션을 수행 하기 전에 원본 서버에 로그인 하는 것을 방지 하려면 제한 된 위임을 설정 합니다. 제한 된 위임을 설정 하려면 도메인 관리자 자격 증명이 필요 합니다. 자세한 내용은 [실시간 마이그레이션에 대 한 호스트를 설정](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)합니다. 
 
 ### <a name="failed-because-the-host-hardware-isnt-compatible"></a>호스트 하드웨어에는 호환 되지 않습니다. 실패 했습니다.
 
 가상 컴퓨터 프로세서 호환성 설정에 없는 하나 이상의 스냅샷이 이동 하는 호스트 프로세서 버전이 다른 경우 실패 합니다. 오류가 발생 하 고이 메시지가 표시 됩니다.
 
**가상 컴퓨터를 대상 컴퓨터로 이동할 수 없습니다. 대상 컴퓨터의 하드웨어가이 가상 컴퓨터의 하드웨어 요구 사항과 호환 되지 않습니다.**
 
 이 문제를 해결 하려면 가상 컴퓨터를 종료 한 프로세서 호환성 설정을 사용 합니다.
 
1. Hyper-v 관리자에서에 **가상 컴퓨터** 창에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 설정을 클릭 합니다.
2. 탐색 창에서 확장 **프로세서** 클릭 **호환성**합니다.
3. 확인 **다른 프로세서 버전을 사용 하는 컴퓨터로 마이그레이션**합니다.
4. **확인**을 클릭합니다.
 
   Windows PowerShell을 사용 하려면 사용 된 [Set-vmprocessor](https://technet.microsoft.com/library/hh848533.aspx) cmdlet:
 
   ```
   PS C:\> Set-VMProcessor TestVM -CompatibilityForMigrationEnabled $true
   ```