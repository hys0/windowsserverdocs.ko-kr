---
title: SMB 보안 강화
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 암호화 기능에 대 한 설명입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7221d3ea94ff9f2d7fca8e95cee66597e2dc6270
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402066"
---
# <a name="smb-security-enhancements"></a>SMB 보안 강화

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

이 항목에서는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 보안 향상 기능에 대해 설명 합니다.

## <a name="smb-encryption"></a>SMB 암호화

SMB 암호화는 SMB 데이터에 대 한 종단 간 암호화를 제공 하 고 신뢰할 수 없는 네트워크의 도청 발생 으로부터 데이터를 보호 합니다. 최소한의 노력으로 SMB 암호화를 배포할 수 있지만 특수화 된 하드웨어 또는 소프트웨어에 대 한 추가 비용이 약간 필요할 수 있습니다. IPsec (인터넷 프로토콜 보안) 또는 WAN 가속기에 대 한 요구 사항은 없습니다. SMB 암호화는 공유 기준 또는 전체 파일 서버에 대해 구성할 수 있으며 신뢰할 수 없는 네트워크에서 데이터가 이동 되는 다양 한 시나리오에 사용할 수 있습니다.

>[!NOTE]
>SMB 암호화는 미사용 보안을 포함 하지 않습니다 .이는 일반적으로 BitLocker 드라이브 암호화에 의해 처리 됩니다.

중요 한 데이터를 메시지 가로채기 (man-in-the-middle) 공격 으로부터 보호 해야 하는 모든 시나리오에서 SMB 암호화를 고려해 야 합니다. 가능한 시나리오는 다음과 같습니다.

- 정보 근로자의 중요 한 데이터는 SMB 프로토콜을 사용 하 여 이동 합니다. SMB 암호화는 타사 공급자가 유지 관리 하는 WAN (광역 네트워크) 연결과 같이 트래버스 되는 네트워크에 관계 없이 파일 서버와 클라이언트 간의 종단 간 개인 정보 보호 및 무결성 보증을 제공 합니다.
- SMB 3.0을 사용 하면 파일 서버에서 SQL Server 또는 Hyper-v와 같은 서버 응용 프로그램에 지속적으로 사용 가능한 저장소를 제공할 수 있습니다. SMB 암호화를 사용 하도록 설정 하면 스누핑 공격 으로부터 해당 정보를 보호할 수 있는 기회가 제공 됩니다. 대부분의 San (저장 영역 네트워크)에 필요한 전용 하드웨어 솔루션을 사용 하는 것 보다 SMB 암호화를 사용 하는 것이 더 간단 합니다.

>[!IMPORTANT]
>암호화 되지 않은 경우에 비해 종단 간 암호화 보호를 사용 하 여 성능에 대 한 중요 한 비용이 발생 합니다.

## <a name="enable-smb-encryption"></a>SMB 암호화 사용

전체 파일 서버 또는 특정 파일 공유에 대해서만 SMB 암호화를 사용 하도록 설정할 수 있습니다. SMB 암호화를 사용 하도록 설정 하려면 다음 절차 중 하나를 사용 합니다.

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 SMB 암호화 사용

1. 개별 파일 공유에 대 한 SMB 암호화를 사용 하도록 설정 하려면 서버에 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. 전체 파일 서버에 SMB 암호화를 사용 하도록 설정 하려면 서버에 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. SMB 암호화를 사용 하도록 설정 된 새 SMB 파일 공유를 만들려면 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>서버 관리자를 사용 하 여 SMB 암호화 사용

1. 서버 관리자에서 **파일 및 저장소 서비스**를 엽니다.
2. 공유 **를 선택 하** 여 공유 관리 페이지를 엽니다.
3. SMB 암호화를 사용 하도록 설정 하려는 공유를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.
4. 공유의 **설정** 페이지에서 **데이터 액세스 암호화**를 선택 합니다. 이 공유에 대 한 원격 파일 액세스가 암호화 됩니다.

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 암호화 배포에 대 한 고려 사항

기본적으로 파일 공유 또는 서버에 SMB 암호화를 사용 하도록 설정 하면 SMB 3.0 클라이언트만 지정 된 파일 공유에 액세스할 수 있습니다. 이렇게 하면 관리자가 공유에 액세스 하는 모든 클라이언트의 데이터를 안전 하 게 보호 합니다. 그러나 경우에 따라 관리자는 SMB 3.0을 지원 하지 않는 클라이언트 (예: 혼합 클라이언트 운영 체제 버전을 사용 하는 경우 전환 기간 동안)에 대해 암호화 되지 않은 액세스를 허용할 수 있습니다. SMB 3.0을 지원 하지 않는 클라이언트에 대해 암호화 되지 않은 액세스를 허용 하려면 Windows PowerShell에서 다음 스크립트를 입력 합니다.

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

다음 섹션에서 설명 하는 보안 언어 협상 기능을 사용 하면 메시지 가로채기 (man-in-the-middle) 공격에서 smb 3.0에서 SMB 2.0 (암호화 되지 않은 액세스 사용)로의 연결을 다운 그레이드할 수 없습니다. 그러나 SMB 1.0에 대 한 다운 그레이드는 차단 되지 않으므로 암호화 되지 않은 액세스도 발생 합니다. Smb 3.0 클라이언트가 항상 SMB 암호화를 사용 하 여 암호화 된 공유에 액세스 하도록 보장 하려면 SMB 1.0 서버를 사용 하지 않도록 설정 해야 합니다. 자세한 내용은 [SMB 1.0 사용 안 함](#disabling-smb-10)섹션을 참조 하세요. **– RejectUnencryptedAccess** 설정이 기본 설정인 **$true**설정 된 상태로 유지 되는 경우 암호화 가능 smb 3.0 클라이언트만 파일 공유에 액세스할 수 있습니다. smb 1.0 클라이언트도 거부 됩니다.

>[!NOTE]
>* SMB 암호화는 AES (AES(Advanced Encryption Standard))-CCM 알고리즘을 사용 하 여 데이터를 암호화 하 고 해독 합니다. 또한 AES-CCM은 SMB 서명 설정에 관계 없이 암호화 된 파일 공유에 대 한 데이터 무결성 유효성 검사 (서명)를 제공 합니다. 암호화 하지 않고 SMB 서명을 사용 하도록 설정 하려는 경우이 작업을 계속할 수 있습니다. 자세한 내용은 [SMB 서명의 기본 사항](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조 하세요.
>* 조직에서 WAN (광역 네트워크) 가속 어플라이언스를 사용 하는 경우 파일 공유 또는 서버에 액세스 하려고 하면 문제가 발생할 수 있습니다.
>* 기본 구성 (암호화 된 파일 공유에 대 한 암호화 되지 않은 액세스 허용 안 함)을 사용 하는 경우 SMB 3.0을 지원 하지 않는 클라이언트가 암호화 된 파일 공유에 액세스 하려고 하면 이벤트 ID 1003가 SmbServer/Operational 이벤트 로그에 기록 됩니다. 클라이언트는 **액세스 거부** 오류 메시지를 받게 됩니다.
>* NTFS 파일 시스템의 SMB 암호화와 파일 시스템 암호화 (EFS)는 관련이 없으며 SMB 암호화에는 EFS 사용이 필요 하지 않습니다.
>* SMB 암호화와 BitLocker 드라이브 암호화는 관련이 없으며 SMB 암호화에는 BitLocker 드라이브 암호화 사용이 필요 하지 않습니다.

## <a name="secure-dialect-negotiation"></a>보안 언어 협상

SMB 3.0은 SMB 2.0 또는 SMB 3.0 프로토콜 또는 클라이언트와 서버가 협상 하는 기능을 다운 그레이드 하려고 하는 메시지 가로채기 (man-in-the-middle) 공격을 검색할 수 있습니다. 이러한 공격이 클라이언트 또는 서버에서 검색 되 면 연결이 끊어지고 이벤트 ID 1005이 SmbServer/Operational 이벤트 로그에 기록 됩니다. 보안 언어 협상은 SMB 2.0 또는 3.0에서 SMB 1.0로 다운 그레이드을 검색 하거나 방지할 수 없습니다. 따라서 SMB 암호화의 전체 기능을 활용 하려면 SMB 1.0 서버를 사용 하지 않도록 설정 하는 것이 좋습니다. 자세한 내용은 [SMB 1.0을 사용 하지 않도록 설정](#disabling-smb-10)을 참조 하세요.

다음 섹션에서 설명 하는 보안 언어 협상 기능을 사용 하면 메시지 가로채기 (man-in-the-middle) 공격이 SMB 3에서 SMB 2로의 연결을 다운 그레이드 (암호화 되지 않은 액세스 사용) 할 수 없습니다. 그러나 SMB 1로 다운 그레이드를 방지 하는 것이 아니라 암호화 되지 않은 액세스도 발생 합니다. SMB의 이전 비 Windows 구현과 관련 된 잠재적인 문제에 대 한 자세한 내용은 [Microsoft 기술 자료](http://support.microsoft.com/kb/2686098)를 참조 하십시오.

## <a name="new-signing-algorithm"></a>새 서명 알고리즘

SMB 3.0은 서명에 최신 암호화 알고리즘을 사용 합니다. AES (AES(Advanced Encryption Standard))-CMAC (암호화 기반 메시지 인증 코드). SMB 2.0는 이전 HMAC-SHA256 암호화 알고리즘을 사용 했습니다. Aes-CMAC 및 AES-CCM은 AES 지침이 지원 되는 대부분의 최신 Cpu에서 데이터 암호화를 크게 가속화할 수 있습니다. 자세한 내용은 [SMB 서명의 기본 사항](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조 하세요.

## <a name="disabling-smb-10"></a>SMB 1.0 사용 안 함

SMB 1.0의 레거시 컴퓨터 브라우저 서비스 및 원격 관리 프로토콜 기능은 이제 분리 되어 있으므로 제거할 수 있습니다. 이러한 기능은 여전히 기본적으로 사용 하도록 설정 되어 있지만 Windows Server 2003 또는 Windows XP를 실행 하는 컴퓨터와 같은 이전 SMB 클라이언트를 사용 하지 않는 경우에는 SMB 1.0 기능을 제거 하 여 보안을 강화 하 고 잠재적으로 패치를 줄일 수 있습니다.

>[!NOTE]
>SMB 2.0은 Windows Server 2008 및 Windows Vista에서 도입 되었습니다. Windows Server 2003 또는 Windows XP를 실행 하는 컴퓨터와 같은 이전 클라이언트는 SMB 2.0을 지원 하지 않습니다. 따라서 SMB 1.0 서버를 사용 하지 않도록 설정 하는 경우 파일 공유 또는 인쇄 공유에 액세스할 수 없습니다. 또한 일부 타사 SMB 클라이언트는 SMB 2.0 파일 공유 또는 인쇄 공유에 액세스 하지 못할 수도 있습니다 (예: "검색-공유" 기능이 있는 프린터).

Smb 1.0을 사용 하지 않도록 설정 하기 전에 smb 클라이언트가 현재 smb 1.0을 실행 하는 서버에 연결 되어 있는지 확인 해야 합니다. 이렇게 하려면 Windows PowerShell에서 다음 cmdlet을 입력 합니다.

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>감사 내역을 작성 하려면 일주일 동안 (매일 여러 번)이 스크립트를 반복 해 서 실행 해야 합니다. 이 작업을 예약 된 작업으로 실행할 수도 있습니다.

SMB 1.0을 사용 하지 않도록 설정 하려면 Windows PowerShell에서 다음 스크립트를 입력 합니다.

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>SMB 1.0를 실행 하는 서버가 사용 하지 않도록 설정 되었기 때문에 SMB 클라이언트 연결이 거부 된 경우 SmbServer/Operational 이벤트 로그에 이벤트 ID 1001가 기록 됩니다.

## <a name="more-information"></a>자세한 정보

다음은 Windows Server 2012의 SMB 및 관련 기술에 대 한 몇 가지 추가 리소스입니다.

- [서버 메시지 블록](file-server-smb-overview.md)
- [Windows Server의 스토리지](../storage.md)
- [응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버](../../failover-clustering/sofs-overview.md)