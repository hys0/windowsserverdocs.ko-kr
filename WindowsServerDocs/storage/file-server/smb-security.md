---
title: SMB 보안 강화
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016에서 SMB 암호화 기능에 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b1586c8c63e46452075b4106c944670395734142
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034406"
---
# <a name="smb-security-enhancements"></a>SMB 보안 강화

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

이 항목에서는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016에서 향상 된 SMB 보안 기능을 설명 합니다.

## <a name="smb-encryption"></a>SMB 암호화

SMB 암호화 SMB 데이터의 종단 간 암호화를 제공 하 고 신뢰할 수 없는 네트워크에서 도청 항목에서 데이터를 보호 합니다. 최소한의 노력으로 SMB 암호화를 배포할 수 있지만 특수 하드웨어 또는 소프트웨어에 대 한 작은 추가 비용을 필요할 수 있습니다. 있기 인터넷 프로토콜 보안 (IPsec) 또는 WAN 가속기에 대 한 요구 사항이 없습니다. 공유 당 기준 또는 전체 파일 서버에 대해 SMB 암호화를 구성할 수 있습니다 하 고 다양 한 시나리오 데이터에서 신뢰할 수 없는 네트워크를 통과 하는 위치에 사용할 수 있습니다.

>[!NOTE]
>SMB 암호화는 BitLocker 드라이브 암호화가 일반적으로 처리 하는 미사용 시 보안을 다루지 않습니다.

SMB 암호화는 중요 한 데이터를 중간자 개입 공격 으로부터 보호 해야 하는 모든 시나리오에 대 한 고려 되어야 합니다. 가능한 시나리오는 다음과 같습니다.

- 정보 근로자의 중요 한 데이터는 SMB 프로토콜을 사용 하 여 이동 됩니다. SMB 암호화는 파일 서버와 Microsoft 이외의 공급자가 관리 하는 광역 네트워크 (WAN) 연결 등으로 트래버스 네트워크에 관계 없이 클라이언트 간의 종단 간 개인 정보 보호 및 무결성 보증을 제공 합니다.
- SMB 3.0 파일 서버를를 SQL Server 또는 Hyper-v와 같은 서버 응용 프로그램을 위한 지속적으로 사용 가능한 저장소를 제공할 수 있습니다. SMB 암호화를 사용 하도록 설정 하면 스누핑 공격 으로부터 정보를 보호 하려면 기회를 제공 합니다. SMB 암호화는 대부분의 San (저장 영역 네트워크)에 대 한 필요한 전용된 하드웨어 솔루션 보다 사용 하기가 더 쉽습니다.

>[!IMPORTANT]
>암호화 되지 않은 비교 했을 때 종단 간 암호화 보호를 사용 하 여 비용을 운영 하는 주목할 만한 성능은 점에 유의 해야 합니다.

## <a name="enable-smb-encryption"></a>SMB 암호화를 사용 하도록 설정

전체 파일 서버 또는 특정 파일 공유에만 SMB 암호화를 사용할 수 있습니다. SMB 암호화를 사용 하도록 설정 하려면 다음 절차 중 하나를 사용 합니다.

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell 사용 하 여 SMB 암호화를 사용 하도록 설정

1. 개별 파일 공유에 SMB 암호화를 사용 하려면 서버에서 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. 전체 파일 서버에 대 한 SMB 암호화를 사용 하려면 서버에서 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. 사용 하도록 설정 하는 SMB 암호화를 사용 하 여 새로운 SMB 파일 공유를 만들려면 다음 다음 스크립트를 입력 합니다.
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>서버 관리자를 통한 SMB 암호화를 사용 하도록 설정

1. 서버 관리자에서 엽니다 **File and Storage Services**합니다.
2. 선택 **공유** 공유 관리 페이지를 엽니다.
3. SMB 암호화를 사용 하 여 선택 하려는 공유를 마우스 오른쪽 단추로 클릭 **속성**합니다.
4. 에 **설정을** 공유를 선택 페이지 **데이터 액세스 암호화**합니다. 이 공유에 원격 파일 액세스 암호화 됩니다.

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 암호화를 배포 하기 위한 고려 사항

기본적으로 파일 공유 또는 서버에 대해 SMB 암호화를 사용 하는 경우 SMB 3.0 클라이언트에만 액세스할 수 있습니다 지정된 된 파일 공유 합니다. 이 관리자의 의도의 공유에 액세스 하는 모든 클라이언트에 대 한 데이터 보호를 적용 합니다. 그러나 경우에 따라 관리자 (예를 들어, 혼합된 클라이언트 운영 체제 버전을 사용할 때 전환 기간이) 중 SMB 3.0을 지원 하지 않는 클라이언트에 대 한 암호화 되지 않은 액세스를 허용 하도록 할 수 있습니다. SMB 3.0을 지원 하지 않는 클라이언트에 대 한 암호화 되지 않은 액세스를 허용 하려면 Windows PowerShell에서 다음 스크립트를 입력 합니다.

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

다음 섹션에 설명 된 보안 언어 협상 기능에서 SMB 3.0에서 SMB 2.0 (암호화 되지 않은 액세스 사용)에 대 한 연결을 다운 그레이드 중간자 개입 공격을 방지 합니다. 그러나 암호화 되지 않은 액세스도 될 수 있는 SMB 1.0으로 다운 그레이드를 방지 하지 않습니다. SMB 3.0 클라이언트가 항상 암호화를 사용 SMB 암호화 된 공유에 액세스를 보장 하기 위해 SMB 1.0 서버를 해제 해야 합니다. (자세한 내용은 섹션을 참조 하십시오 [SMB 1.0 사용 하지 않도록 설정](#disabling-smb-10).) 경우는 **– RejectUnencryptedAccess** 설정의 기본 설정 그대로 **$true**, 암호화 지원만 SMB 3.0 클라이언트 (SMB 1.0 클라이언트는 또한 거부할) 파일 공유에 액세스할 수 있습니다.

>[!NOTE]
>* 고급 암호화 표준 (AES)을 사용 하 여 SMB 암호화-CCM 알고리즘은 데이터 암호화 및 해독 합니다. 또한 AES CCM (서명) 암호화 된 파일 공유의 경우 SMB 서명 설정에 관계 없이 데이터 무결성 유효성 검사를 제공 합니다. SMB 서명을 암호화 하지 않고을 사용 하도록 설정 하려는 경우에이 위해 계속 수 있습니다. 자세한 내용은 [의 The Basics SMB 서명](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)합니다.
>* 조직 광역 네트워크 (WAN) 가속 어플라이언스를 사용 하는 경우 파일 공유 나 서버에 액세스 하려고 할 때 문제가 발생할 수 있습니다.
>* 기본 구성을 사용 하 여 (암호화 된 파일 공유에 허용 된 암호화 되지 않은 액세스가 없는) 하는 경우 이벤트 ID 1003 암호화 된 파일 공유에 액세스 하려고 하는 SMB 3.0을 지원 하지 않는 클라이언트는 Microsoft-Windows-SmbServer/Operational 이벤트 로그에 기록 하는 경우 클라이언트는 수신 하 고는 **액세스가 거부 되었습니다** 오류 메시지입니다.
>* SMB 암호화 및 파일 시스템 EFS (암호화) NTFS 파일 시스템에 관련 된 되지 않으며 SMB 암호화 필요 하지 않거나 EFS를 사용 하 여에 따라 달라 집니다.
>* SMB 암호화 및 BitLocker 드라이브 암호화에 관련 되지 않으며 SMB 암호화 필요 하거나 BitLocker 드라이브 암호화를 사용 하 여 종속 되지 않습니다.

## <a name="secure-dialect-negotiation"></a>안전한 언어 협상

SMB 3.0은 SMB 2.0 또는 SMB 3.0 프로토콜 또는 클라이언트와 서버 협상 하는 기능을 다운 그레이드 하려고 하는 중간자 개입 공격을 감지할 수 있습니다. 클라이언트 또는 서버에서 이러한 공격이 감지 되 면 연결이 끊어질 때 하 고 이벤트 ID 1005 Microsoft-Windows-SmbServer/Operational 이벤트 로그에 기록 됩니다. 언어 보안 협상 검색 하거나 SMB 1.0 SMB 2.0 또는 3.0에서 다운 그레이드를 방지할 수 없습니다. 이 인해 및 SMB 암호화의 전체 기능을 활용 하려면 SMB 1.0 서버를 사용 하지 않도록 설정 하는 것이 좋습니다. 자세한 내용은 [SMB 1.0 사용 하지 않도록 설정](#disabling-smb-10)합니다.

다음 섹션에서 설명 하는 안전한 언어 협상 기능 (암호화 되지 않은 액세스 사용)는 SMB 2; SMB 3에서 연결을 다운 그레이드에서 중간자 개입 공격을 방지 그러나 암호화 되지 않은 액세스도 될 수 있는 SMB 1로 다운 그레이드 방지 하지 않습니다. SMB의 이전 Windows가 아닌 구현 사용 하 여 잠재적인 문제에 대 한 자세한 내용은 참조는 [Microsoft 기술 자료](http://support.microsoft.com/kb/2686098)합니다.

## <a name="new-signing-algorithm"></a>새 서명 알고리즘

SMB 3.0에서는 서명 최신 암호화 알고리즘을 사용합니다. Advanced Encryption Standard (AES)-암호화-기반 메시지 인증 코드 (CMAC) 합니다. SMB 2.0 이전 HMAC-SHA256 암호화 알고리즘을 사용 합니다. AES-CMAC 및 AES-CCM 지원 AES 명령에 있는 대부분의 최신 Cpu에서 데이터 암호화를 가속화할 크게 수 있습니다. 자세한 내용은 [의 The Basics SMB 서명](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)합니다.

## <a name="disabling-smb-10"></a>SMB 1.0을 사용 하지 않도록 설정

기존 컴퓨터 브라우저 서비스 및 SMB 1.0에서 원격 관리 프로토콜 기능을 이제 별도 되며 제거할 수 있습니다. 이러한 기능은 기본적으로 여전히 사용할 수 있지만 Windows Server 2003 또는 Windows XP를 실행 하는 컴퓨터와 같은 이전 SMB 클라이언트가 없는 경우 보안을 강화 하 고 패치를 잠재적으로 줄일 SMB 1.0 기능을 제거할 수 있습니다.

>[!NOTE]
>SMB 2.0은 Windows Server 2008 및 Windows Vista에서 도입 되었습니다. Windows Server 2003 또는 Windows XP를 실행 하는 컴퓨터 등의 이전 클라이언트는 SMB 2.0을 지원 하지 않습니다. 따라서 파일 공유에 액세스 하거나 SMB 1.0 서버를 사용 하지 않도록 설정 하는 경우 공유를 인쇄 하려면 없게 됩니다 것을 또한 일부 타사 SMB 클라이언트는 SMB 2.0 파일 공유에 액세스 하거나 프린터 공유 (예: "검색 공유" 기능을 사용 하 여 프린터) 수 있습니다.

SMB 1.0을 사용 하지 않도록 설정 시작 하기 전에 SMB 클라이언트가 SMB 1.0을 실행 하는 서버에 현재 연결 된 경우 확인 해야 합니다. 이렇게 하려면 Windows PowerShell에서 다음 cmdlet을 입력 합니다.

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>감사 내역을 만들려고 요일 (여러 번 매일)에 걸쳐 반복 해 서이 스크립트를 실행 해야 합니다. 예약된 된 태스크로도 실행할 수 있습니다.

SMB 1.0을 사용 하지 않으려면 Windows PowerShell에서 다음 스크립트를 입력 합니다.

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>SMB 1.0을 실행 하는 서버가 비활성화 되었으므로 SMB 클라이언트 연결을 거부 되 면 Microsoft-Windows-SmbServer/Operational 이벤트 로그에서 이벤트 ID 1001이 로깅됩니다.

## <a name="more-information"></a>자세한 정보

SMB 및 Windows Server 2012의 관련된 기술에 대 한 몇 가지 추가 리소스는 다음과 같습니다.

- [서버 메시지 블록](file-server-smb-overview.md)
- [Windows Server에서 저장소](../storage.md)
- [응용 프로그램 데이터용 스케일 아웃 파일 서버](../../failover-clustering/sofs-overview.md)