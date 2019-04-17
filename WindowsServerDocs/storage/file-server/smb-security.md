---
title: SMB 보안 향상 기능
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016 SMB 암호화 기능을 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 831ca8266c3ec18ffb83227dcb2d39b3f953ad1a
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233529"
---
# <a name="smb-security-enhancements"></a>SMB 보안 향상 기능

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

이 항목에서는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 보안 향상 기능에 설명 합니다.

## <a name="smb-encryption"></a>SMB 암호화

SMB 암호화 SMB 데이터의 끝-암호화를 제공 하 고 신뢰할 수 없는 네트워크에서 발생 한 도청 수에서 데이터를 보호 합니다. 최소한의 노력으로 SMB 암호화를 배포할 수 있지만 특수 하드웨어 또는 소프트웨어에 대 한 추가 비용을 작은 번 실행 해야 합니다. 있으면 인터넷 프로토콜 보안 (IPsec) 또는 WAN 가속기에 대 한 요구 사항이 없습니다. SMB 암호화 당 공유 별로 또는 전체 파일 서버에 대해 구성할 수 있습니다 하 고 다양 한 데이터가 신뢰할 수 없는 네트워크를 통과 하는 시나리오에 대해 사용할 수 있습니다.

>[!NOTE]
>SMB 암호화 BitLocker 드라이브 암호화가 일반적으로 처리 하는 나머지 부분에서 보안을 해결할 수는 없습니다.

SMB 암호화 중요 한 데이터를 메시지 가로채기 중간 공격 으로부터 보호 해야 하는 모든 시나리오에 대 한 것으로 간주 해야 합니다. 사용할 수 있는 시나리오는 다음과 같습니다.

- 정보 근로자의 중요 한 데이터는 SMB 프로토콜을 사용 하 여 이동 됩니다. SMB 암호화 파일 서버와 같은 타사 공급자에 의해 유지 관리 되는 광역 네트워크 (WAN) 연결 통과 네트워크에 관계 없이 클라이언트 간의 끝-개인정보 보호 및 무결성 보증을 제공 합니다.
- SMB 3.0 파일 예: SQL Server 또는 Hyper-v 서버 응용 프로그램에 대 한 지속적으로 사용 가능한 저장소를 제공 하는 서버 수 있습니다. SMB 암호화를 사용 하면 다른 공격 으로부터 해당 정보를 보호 하기 위해 기회를 제공 합니다. SMB 암호화는 대부분의 저장소 영역 네트워크 (San)에 필요한 전용된 하드웨어 솔루션에 비해 사용 하 여 더 간단 합니다.

>[!IMPORTANT]
>주목할 만한 성능 비용 암호화 되지 않은 비교 했을 때 모든-종단간 암호화 보호와 함께 작동 하는 유의 해야 합니다.

## <a name="enable-smb-encryption"></a>SMB 암호화를 사용 하도록 설정

전체 파일 서버에 대 한 또는 특정 파일 공유에 대해서만 SMB 암호화를 사용 하도록 설정할 수 있습니다. SMB 암호화를 사용 하도록 설정 하려면 다음 절차 중 하나를 사용 합니다.

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell 사용 하 여 SMB 암호화를 사용 하도록 설정

1. 개별 파일 공유에 대 한 SMB 암호화를 사용 하려면 서버에서 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. 전체 파일 서버에 대 한 SMB 암호화를 사용 하려면 서버에서 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. 새 SMB 파일 공유를 사용 하도록 설정 하는 SMB 암호화를 만들려면 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>서버 관리자를 통한 SMB 암호화를 사용 하도록 설정

1. 서버 관리자에서 **파일 및 저장소 서비스를**엽니다.
2. 공유 관리 페이지를 열려면 **공유** 선택 합니다.
3. SMB 암호화를 사용 하도록 설정 하려는 공유를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.
4. 공유의 **설정** 페이지에서 **데이터 액세스를 통한 암호화를**선택 합니다. 이 공유에 대 한 원격 파일 액세스 암호화 됩니다.

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 암호화를 배포 하기 위한 고려 사항

기본적으로 SMB 암호화 파일 공유 또는 서버를 사용 하는 경우 지정 된 파일 공유에 액세스 하려면 SMB 3.0 클라이언트만 허용 됩니다. 이 공유 폴더에 액세스 하는 모든 클라이언트에 대 한 데이터를 보호의 관리자의 의도 강제 적용 합니다. 그러나 일부 경우에서 관리자는 (예: 혼합된 클라이언트 운영 체제 버전을 사용 중인 경우 프로그램으로 전환 기간) 동안 SMB 3.0을 지원 하지 않는 클라이언트에 대 한 암호화 되지 않은 액세스를 허용 하도록 할 수 있습니다. SMB 3.0을 지원 하지 않는 클라이언트에 대 한 암호화 되지 않은 액세스를 허용 하려면 Windows PowerShell에서 다음 스크립트를 입력 합니다.

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

다음 섹션에 설명 된 보안 방언 협상 기능 SMB 3.0에서 SMB 2.0 (하는 암호화 되지 않은 액세스 사용)에 대 한 연결을 다운 그레이드에서 메시지 가로채기 중간 공격을 방지 합니다. 그러나 암호화 되지 않은 액세스 초래 SMB 1.0으로 다운 그레이드를 못하도록 막지 않습니다. SMB 3.0 클라이언트 암호화 된 공유에 액세스 하려면 항상 SMB 암호화를 사용 하을 보장 하기 위해 SMB 1.0 서버를 비활성화 해야 합니다. (지침을 [사용 하지 않도록 설정 하는 SMB 1.0](#disabling-smb-1.0)섹션 참조). **-RejectUnencryptedAccess** 설정 **$true**기본 설정인에 그대로 유지 됩니다, 하는 경우에 암호화 지원 SMB 3.0 클라이언트만 (SMB 1.0 클라이언트 거부도 됨) 파일 공유에 액세스할 수 있습니다.

>[!NOTE]
>* SMB 암호화의 암호화 표준 AES (고급)를 사용 하 여-CCM 알고리즘 암호화 하 고 데이터를 해독 합니다. 또한 AES CCM (서명) SMB 서명 설정에 관계 없이 암호화 된 파일 공유에 대 한 데이터 무결성 유효성 검사를 제공 합니다. SMB 암호화 하지 않고 서명을 사용 하도록 설정 하려는 경우에이 작업을 수행 계속 수 있습니다. 자세한 내용은 [의 기본 (영문) SMB 서명](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조 하십시오.
>* 광역 네트워크 (WAN) 가속 어플라이언스 조직에서 사용 하는 경우 파일 공유 또는 서버에 액세스 하려고 할 때 문제가 발생할 수 있습니다.
>* 기본 구성을 사용 하 여 (되는 경우에 암호화 된 파일 공유를 사용할 수 없는 암호화 되지 않은 액세스) 클라이언트는 암호화 된 파일 공유, 이벤트 ID 1003에 액세스 하려고 하는 SMB 3.0을 지원 하지 않는 Microsoft-Windows-SmbServer/작동 가능 이벤트 로그에 기록 되는 경우, 및 클라이언트 **액세스 거부** 오류 메시지가 수신 됩니다.
>* SMB 암호화 및 NTFS 파일 시스템의 파일 시스템 암호화 (EFS) 관련이 없는, 및 SMB 암호화 필요 하지 않거나 EFS를 사용 하 여에 따라 달라 집니다.
>* SMB 암호화 및 BitLocker 드라이브 암호화는 관련, 및 SMB 암호화 필요 하지 않거나 BitLocker 드라이브 암호화를 사용 하 여에 따라 달라 집니다.

## <a name="secure-dialect-negotiation"></a>보안 방언 협상

SMB 3.0은 SMB 2.0 또는 SMB 3.0 프로토콜 또는 클라이언트와 서버 협상 하는 기능을 다운 그레이드 하려고 하는 메시지 가로채기 중간 공격을 검색할 수 있습니다. 이러한 공격 클라이언트 또는 서버에 의해 감지 되 면 연결이 끊어질 때 및 이벤트 ID 1005 Microsoft-Windows-SmbServer/작동 가능 이벤트 로그에 기록 됩니다. 방언 보안 협상을 검색 하거나 SMB 2.0 또는 3.0에서 다운 그레이드 SMB 1.0을 방지 수 없습니다. 따라서 및 SMB 암호화의 전체 기능을 활용 하는 SMB 1.0 서버를 사용 하지 않도록 설정 하는 것이 좋습니다. 자세한 내용은 [SMB 1.0 비활성화](#disabling-smb-1.0)를 참조 하십시오.

다음 섹션에 설명 된 보안 방언 협상 기능 (하는 암호화 되지 않은 액세스 사용) SMB 2;에 대 한 연결 SMB 3에서 다운 그레이드에서 메시지 가로채기 중간 공격을 방지 그러나 암호화 되지 않은 액세스 초래 하는 SMB 1로 다운 그레이드 못하도록 막지 않습니다. Smb 이전 비 Windows 구현으로 잠재적 문제에 대 한 자세한 내용은 [Microsoft 기술 자료](http://support.microsoft.com/kb/2686098)를 참조 하십시오.

## <a name="new-signing-algorithm"></a>새 서명 알고리즘

SMB 3.0 최신 암호화 알고리즘을 사용 하 여 서명: 암호화 표준 AES (고급)-암호화-기반 메시지 인증 코드 (CMAC). SMB 2.0 이전 HMAC SHA256 암호화 알고리즘을 사용 합니다. AES CMAC 및 AES CCM 지원 AES 명령에 있는 대부분의 최신 Cpu에 데이터 암호화를 크게 가속화할 수 있습니다. 자세한 내용은 [의 기본 (영문) SMB 서명](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조 하십시오.

## <a name="disabling-smb-10"></a>SMB 1.0을 사용 하지 않도록 설정

레거시 컴퓨터 브라우저 서비스 및 SMB 1.0의 원격 관리 프로토콜 기능은 별도, 이제 하 고 제거할 수 있습니다. 이러한 기능을 기본적으로 계속 사용할 수는 있지만 Windows Server 2003 또는 Windows XP를 실행 하는 컴퓨터와 같은 이전 SMB 클라이언트 하지 않은 경우에 보안을 강화 및 패치를 적용을 크게 줄일 SMB 1.0 기능을 제거할 수 있습니다.

>[!NOTE]
>SMB 2.0 Windows Server 2008 및 Windows Vista에서 도입 되었습니다. Windows Server 2003 또는 Windows XP를 실행 하는 컴퓨터와 같은 이전 클라이언트, SMB 2.0;를 지원 하지 않음 따라서 더 하지 수는 SMB 1.0 서버를 사용 하지 않도록 설정 하는 경우 공유 인쇄 또는 파일 공유에 액세스할 수 있습니다. 또한 일부 비 Microsoft SMB 클라이언트가 SMB 2.0 파일 공유에 액세스 하거나 공유 (예: "스캔 공유" 기능을 가진 프린터) 인쇄 못할 수 있습니다.

SMB 1.0을 사용 하지 않도록 설정를 시작 하기 전에 SMB 클라이언트는 현재 SMB 1.0을 실행 하는 서버에 연결 하는 경우 알아낼 필요 합니다. 이 작업을 수행 하려면 Windows PowerShell에서 다음 cmdlet을 입력 합니다.

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>감사 내역을 구축 하는 주 (여러 번 매일)에 걸쳐 반복 하 여이 스크립트를 실행 해야 합니다. 예약 된 작업으로도 실행할 수 있습니다.

SMB 1.0을 사용 하지 않으려면 Windows PowerShell에서 다음 스크립트를 입력 합니다.

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>SMB 1.0을 실행 하는 서버에 사용 하지 않도록 설정 하기 때문에 대 한 SMB 클라이언트 연결 거부 된 경우 Microsoft-Windows-SmbServer/작동 가능 이벤트 로그에 이벤트 ID 1001을 기록 됩니다.

## <a name="more-information"></a>자세한 정보

SMB 및 Windows Server 2012의 관련된 기술에 대 한 추가 리소스는 다음과 같습니다.

- [서버 메시지 블록](file-server-smb-overview.md)
- [WindowsServer의 저장소](../storage.md)
- [응용 프로그램 데이터에 대 한 확장 파일 서버](../../failover-clustering/sofs-overview.md)