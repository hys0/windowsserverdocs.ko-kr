---
title: SMB 보안 강화
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 암호화 기능에 대해 설명합니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7b96574dcfc2a4417aa36780d7bd87c2556f61f
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "75950267"
---
# <a name="smb-security-enhancements"></a>SMB 보안 강화

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

이 토픽에서는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 향상된 SMB 보안에 대해 설명합니다.

## <a name="smb-encryption"></a>SMB 암호화

SMB 암호화는 SMB 데이터에 대한 엔드투엔드 암호화 기능을 제공하며, 신뢰할 수 없는 네트워크에서 발생하는 도청으로부터 데이터를 보호합니다. 최소한의 작업으로 SMB 암호화를 배포할 수 있지만, 약간의 특수 하드웨어 또는 소프트웨어 비용이 발생할 수 있습니다. IPsec(인터넷 프로토콜 보안) WAN 가속기에 대한 요구 사항은 없습니다. SMB 암호화는 공유 단위별로 구성하거나 전체 파일 서버용으로 구성할 수 있으며, 신뢰할 수 없는 네트워크에서 데이터가 전송되는 다양한 시나리오에서 사용할 수 있습니다.

>[!NOTE]
>미사용 보안은 SMB 암호화의 범위에 포함되지 않으며, 일반적으로 BitLocker 드라이브 암호화를 통해 처리됩니다.

중요한 데이터를 메시지 가로채기 공격으로부터 보호해야 하는 시나리오에는 SMB 암호화를 고려해야 합니다. 가능한 시나리오는 다음과 같습니다.

- SMB 프로토콜을 사용하여 정보 근로자의 중요한 데이터를 이동합니다. SMB 암호화는 Microsoft가 아닌 타사 공급자가 유지 관리하는 WAN(광역 네트워크) 연결처럼 트래버스되는 네트워크에 관계없이, 파일 서버와 클라이언트 간의 엔드투엔드 개인 정보 보호 및 무결성을 보증합니다.
- SMB 3.0을 사용하면 파일 서버에서 SQL Server나 Hyper-V 같은 서버 애플리케이션에 지속적으로 사용 가능한 스토리지를 제공할 수 있습니다. SMB 암호화를 사용하도록 설정하면 스누핑 공격으로부터 해당 정보를 보호할 수 있는 기회가 제공됩니다. SMB 암호화는 대부분의 SAN(저장 영역 네트워크)에 필요한 전용 하드웨어 솔루션보다 사용 방법이 간단합니다.

>[!IMPORTANT]
>엔드투엔드 암호화 보호는 비-암호화에 비해 훨씬 많은 성능 비용이 발생한다는 점을 기억해야 합니다.

## <a name="enable-smb-encryption"></a>SMB 암호화 사용

파일 서버 전체에 또는 특정 파일 공유에만 SMB 암호화를 사용하도록 설정할 수 있습니다. 다음 절차 중 하나를 사용하여 SMB 암호화를 사용하도록 설정합니다.

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell에서 SMB 암호화를 사용하도록 설정

1. 개별 파일 공유에 SMB 암호화를 사용하도록 설정하려면 서버에서 다음 스크립트를 입력합니다.
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. 파일 서버 전체에 SMB 암호화를 사용하도록 설정하려면 서버에서 다음 스크립트를 입력합니다.
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. SMB 암호화를 사용하도록 설정된 새 SMB 파일 공유를 만들려면 다음 스크립트를 입력합니다.
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>서버 관리자에서 SMB 암호화를 사용하도록 설정

1. 서버 관리자에서 **파일 및 스토리지 서비스**를 엽니다.
2. **공유**를 선택하여 공유 관리 페이지를 엽니다.
3. SMB 암호화를 사용하도록 설정하려는 공유를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.
4. 공유의 **설정** 페이지에서 데이터 액세스 **암호화**를 선택합니다. 이 공유에 대한 원격 파일 액세스가 암호화됩니다.

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 암호화 배포 시 고려할 사항

기본적으로 파일 공유 또는 서버에 SMB 암호화를 사용하도록 설정할 때 SMB 3.0 클라이언트만이 지정된 파일 공유에 액세스할 수 있습니다. 이를 통해 공유에 액세스하는 모든 클라이언트의 데이터를 안전하게 보호하려는 관리자의 의도를 적용할 수 있습니다. 그러나 경우에 따라 관리자는 SMB 3.0을 지원하지 않는 클라이언트의 암호화되지 않은 액세스를 허용하려 할 때가 있습니다(예: 혼합 클라이언트 운영 체제 버전을 사용하는 전환 기간 동안). SMB 3.0을 지원하지 않는 클라이언트의 암호화되지 않은 액세스를 허용하려면 Windows PowerShell에서 다음 스크립트를 입력합니다.

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

다음 섹션에서 설명하는 보안 언어 협상 기능은 메시지 가로채기 공격이 SMB 3.0의 연결을 (암호화되지 않은 액세스를 사용하는) SMB 2.0으로 다운그레이드할 수 없도록 차단합니다. 그러나 마찬가지로 암호화되지 않은 액세스가 발생하는 SMB 1.0으로의 다운그레이드를 차단하지는 않습니다. SMB 3.0 클라이언트가 항상 SMB 암호화를 사용하여 암호화된 공유에 액세스하도록 보장하려면 SMB 1.0 서버를 사용하지 않도록 설정해야 합니다. (자세한 지침은 [SMB 1.0을 사용하지 않도록 설정](#disabling-smb-10) 섹션을 참조하세요.) **– RejectUnencryptedAccess** 설정을 기본값인 **$true**로 유지하면 암호화를 지원하는 SMB 3.0 클라이언트만이 파일 공유에 액세스할 수 있습니다(SMB 1.0 클라이언트도 거부됨).

>[!NOTE]
>* SMB 암호화는 AES(Advanced Encryption Standard)-CCM 알고리즘을 사용하여 데이터를 암호화하고 암호 해독합니다. 또한 AES-CCM은 SMB 서명 설정에 관계없이 암호화된 파일 공유의 데이터 무결성 유효성 검사(서명)를 제공합니다. 암호화 없이 SMB 서명을 사용하도록 설정하려는 경우 해당 설정 작업을 계속 진행할 수 있습니다. 자세한 내용은 [SMB 서명 기본 사항](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조하세요.
>* 조직에서 WAN(광역 네트워크) 가속 어플라이언스를 사용하는 경우 파일 공유 또는 서버에 액세스하려고 하면 문제가 발생할 수 있습니다.
>* 기본 구성(암호화된 파일 공유에 대한 암호화되지 않은 액세스를 허용하지 않음)을 사용하는 경우 SMB 3.0을 지원하지 않는 클라이언트가 암호화된 파일 공유에 액세스하려고 시도하면 Microsoft-Windows-SmbServer/Operational 이벤트 로그에 이벤트 ID 1003이 기록되고, 클라이언트는 **액세스 거부됨** 오류 메시지를 받게 됩니다.
>* NTFS 파일 시스템의 SMB 암호화와 EFS(파일 시스템 암호화)는 서로 관련이 없으며, SMB 암호화는 EFS를 요구하지도, 사용하지도 않습니다.
>* SMB 암호화와 BitLocker 드라이브 암호화는 서로 관련이 없으며, SMB 암호화는 BitLocker 드라이브 암호화를 요구하지도, 사용하지도 않습니다.

## <a name="secure-dialect-negotiation"></a>보안 언어 협상

SMB 3.0은 SMB 2.0/SMB 3.0 프로토콜 또는 클라이언트와 서버가 협상하는 기능을 다운그레이드하려고 시도하는 메시지 가로채기 공격을 탐지할 수 있습니다. 클라이언트 또는 서버에서 이러한 공격을 탐지하면 연결이 끊어지고 Microsoft-Windows-SmbServer/Operational 이벤트 로그에 이벤트 ID 1005가 기록됩니다. 보안 언어 협상은 SMB 2.0 또는 3.0에서 SMB 1.0으로의 다운그레이드를 탐지하거나 방지할 수 없습니다. 따라서 SMB 암호화의 전체 기능을 활용하려면 SMB 1.0 서버를 사용하지 않도록 설정할 것을 강력하게 권장합니다. 자세한 내용은 [SMB 1.0을 사용하지 않도록 설정](#disabling-smb-10)을 참조하세요.

다음 섹션에서 설명하는 보안 언어 협상 기능은 메시지 가로채기 공격이 SMB 3의 연결을 (암호화되지 않은 액세스를 사용하는) SMB 2로 다운그레이드할 수 없도록 차단합니다. 그러나 마찬가지로 암호화되지 않은 액세스가 발생하는 SMB 1로의 다운그레이드를 차단하지는 않습니다. 이전의 비-Windows SMB 구현과 관련된 잠재적인 문제에 대한 자세한 내용은 [Microsoft 기술 자료](https://support.microsoft.com/kb/2686098)를 참조하세요.

## <a name="new-signing-algorithm"></a>새로운 서명 알고리즘

SMB 3.0은 최신 암호화 알고리즘인 AES(Advanced Encryption Standard)-CMAC(암호 기반 메시지 인증 코드)를 서명에 사용합니다. SMB 2.0는 이전 HMAC-SHA256 암호화 알고리즘을 사용했습니다. AES-CMAC 및 AES-CCM은 AES 지침이 지원되는 대부분의 최신 CPU에서 데이터 암호화 속도를 크게 높일 수 있습니다. 자세한 내용은 [SMB 서명 기본 사항](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조하세요.

## <a name="disabling-smb-10"></a>SMB 1.0을 사용하지 않도록 설정

SMB 1.0의 기존 컴퓨터 브라우저 서비스 및 원격 관리 프로토콜 기능은 이제 별도로 제공되며 제거할 수 있습니다. 이러한 기능은 여전히 기본적으로 사용되지만, Windows Server 2003 또는 Windows XP를 실행하는 컴퓨터 같은 이전 SMB 클라이언트가 없는 경우에는 SMB 1.0 기능을 제거하여 보안을 강화하고 잠재적으로 패치 적용을 줄일 수 있습니다.

>[!NOTE]
>SMB 2.0은 Windows Server 2008 및 Windows Vista에서 도입되었습니다. Windows Server 2003 또는 Windows XP를 실행하는 컴퓨터와 같은 이전 클라이언트는 SMB 2.0을 지원하지 않습니다. 따라서 SMB 1.0 서버를 사용하지 않도록 설정하면 이전 클라이언트에서 파일 공유 또는 인쇄 공유에 액세스할 수 없습니다. 뿐만 아니라 일부 비-Microsoft SMB 클라이언트도 SMB 2.0 파일 공유 또는 인쇄 공유에 액세스하지 못할 수 있습니다(예: "검색-공유" 기능이 있는 프린터).

SMB 1.0을 사용하지 않도록 설정하기 전에, SMB 클라이언트가 현재 SMB 1.0을 실행 중인 서버에 연결되어 있는지 확인해야 합니다. 확인하려면 Windows PowerShell에서 다음 cmdlet을 입력합니다.

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>일주일 동안(매일 여러 차례) 이 스크립트를 반복해서 실행하여 감사 내역을 작성해야 합니다. 이 스크립트 실행을 예약된 작업으로 실행할 수도 있습니다.

SMB 1.0을 사용하지 않도록 설정하려면 Windows PowerShell에서 다음 스크립트를 입력합니다.

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>SMB 1.0을 실행하는 서버가 사용하지 않도록 설정되었기 때문에 SMB 클라이언트 연결이 거부된 경우에는 Microsoft-Windows-SmbServer/Operational 이벤트 로그에 이벤트 ID 1001이 기록됩니다.

## <a name="more-information"></a>자세한 정보

다음은 Windows Server 2012의 SMB 및 관련 기술에 대한 추가 리소스입니다.

- [서버 메시지 블록](file-server-smb-overview.md)
- [Windows Server의 스토리지](../storage.md)
- [애플리케이션 데이터를 위한 스케일 아웃 파일 서버](../../failover-clustering/sofs-overview.md)