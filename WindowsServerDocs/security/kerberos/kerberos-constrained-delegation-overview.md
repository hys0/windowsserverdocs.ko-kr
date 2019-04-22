---
title: Kerberos Constrained Delegation Overview
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51923b0a-0c1a-47b2-93a0-d36f8e295589
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d77dd6f6f310ae71a4d9e2d52b44cc9b1bef6401
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821934"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 개요 항목에서는 Windows Server 2012 R2 및 Windows Server 2012에서 Kerberos 제한 위임에 대 한 새 기능을 설명 합니다.

**기능 설명**

Kerberos 제한 위임은 서비스에서 사용할 수 있는 보다 안전한 형식의 위임을 제공하기 위해 Windows Server 2003에 처음 도입되었습니다. Kerberos 제한 위임이 구성되면 이 기능은 지정된 서버가 사용자 대신 작업을 수행할 수 있는 서비스를 제한합니다. 이 경우 서비스의 도메인 계정을 구성하기 위해 도메인 관리자 권한이 필요하며, 계정이 단일 도메인으로 제한됩니다. 오늘날의 기업에서는 프런트 엔드 서비스는 해당 도메인의 서비스와만 통합으로 제한 되도록 설계 되지 않았습니다.

도메인 관리자가 서비스를 구성한 이전 운영 체제에서 서비스 관리자는 기업이 소유한 리소스 서비스로 위임되는 프런트 엔드 서비스를 확인하는 데 사용할 수 있는 유용한 방법이 없는 상태입니다. 뿐만 아니라 리소스 서비스로 위임될 수 있는 프런트 엔드 서비스에 잠재적 공격 지점이 있습니다. 프런트 엔드 서비스를 호스팅하는 서버의 보안이 손상되고, 이 서비스가 리소스 서비스로 위임되도록 구성된 경우 리소스 서비스의 보안 역시 손상될 수 있습니다.

Windows Server 2012 R2 및 Windows Server 2012에서 서비스에 대 한 제한 된 위임을 구성 하는 기능에 도메인 관리자에서 서비스 관리자로 이전 되었습니다. 이렇게 하여 백 엔드 서비스 관리자가 프런트 엔드 서비스를 허용하거나 거부할 수 있습니다.

Windows Server 2003에서 도입된 제한 위임에 대한 자세한 내용은 [Kerberos 프로토콜 전환 및 제한 위임](https://technet.microsoft.com/library/cc739587(v=ws.10))(영문)을 참조하세요.

Kerberos 프로토콜의 Windows Server 2012 R2 및 Windows Server 2012 구현에는 제한 된 위임에 맞게 확장이 포함 됩니다.  S4U2Proxy(Service for User to Proxy)를 통해 서비스에서 사용자에 대한 Kerberos 서비스 티켓을 사용하여 KDC(키 배포 센터)로부터 백 엔드 서비스에 대한 서비스 티켓을 얻을 수 있습니다. 이러한 확장에는 위임을 다른 도메인에 있을 수 있는 백 엔드 서비스의 계정에 구성할 수 있습니다. 이러한 확장에 대 한 자세한 내용은 참조 하세요. [ \[MS-SFU\]: 섹션(영문)을 사용자 서비스 및 제한 위임 프로토콜 사양](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx) MSDN 라이브러리에서.

**실제 응용 프로그램**

제한 된 위임을 통해 서비스 관리자는 지정 하 고 응용 프로그램 서비스 사용자를 대신 하 여 작업할 수 있는 범위를 제한 하 여 응용 프로그램 트러스트 경계를 적용 하는 기능입니다. 서비스 관리자는 백 엔드 서비스에 위임할 수 있는 프런트 엔드 서비스 계정을 구성할 수 있습니다.

Windows Server 2012 R2 및 Windows Server 2012, Microsoft Internet Security and Acceleration (ISA) Server, Microsoft Forefront Threat Management Gateway, Microsoft Exchange 등의 프런트 엔드 서비스에서 도메인 간 제한 위임을 지원 하 여 Outlook Web Access (OWA) 및 Microsoft SharePoint Server는 다른 도메인의 서버에 인증할 수 제한 된 위임을 사용 하도록 구성할 수 있습니다. 그러면 기존 Kerberos 인프라를 사용한 도메인 간 서비스 솔루션이 지원됩니다. Kerberos 제한 위임은 도메인 관리자나 서비스 관리자가 관리할 수 있습니다.

## <a name="resource-based-constrained-delegation-across-domains"></a>여러 도메인에 걸친 리소스 기반 제한 위임

프런트 엔드 및 리소스 서비스가 같은 도메인에 있지 않아도 Kerberos 제한 위임을 사용하여 제한 위임을 제공할 수 있습니다. 서비스 관리자는 리소스 서비스의 계정 개체에 대해 사용자를 가장할 수 있는 프런트 엔드 서비스의 도메인 계정을 지정하여 새 위임을 구성할 수 있습니다.

**이와 같은 변경을 통해 더해지는 가치**

도메인 간 제한 위임을 지원함으로써 제한 위임을 사용하도록 서비스를 구성하여 제한되지 않은 위임을 사용하지 않고 다른 도메인의 서버로부터 인증을 받을 수 있습니다. 그러면 서비스로의 위임을 위해 프런트 엔드 서비스를 트러스트하지 않고 기존의 Kerberos 인프라를 사용한 도메인 간 서비스 솔루션에 대한 인증이 지원됩니다.

또한 서버 도메인에서 위임 관리자가 리소스 소유자에 게 위임 된 id의 소스를 신뢰 해야 하는지 여부를 결정 하는 만큼 이동 합니다.

**달라진 기능**

기본 프로토콜의 변경을 통해 도메인 간 제한 위임을 사용할 수 있습니다. Kerberos 프로토콜의 Windows Server 2012 R2 및 Windows Server 2012 구현에는 프록시 (S4U2Proxy) 프로토콜에 서비스 사용자에 대 한 확장이 포함 됩니다. 이 확장은 서비스에서 사용자에 대한 Kerberos 서비스 티켓을 사용하여 KDC(키 배포 센터)로부터 백 엔드 서비스에 대한 서비스 티켓을 얻을 수 있도록 해주는 Kerberos 프로토콜에 대한 확장 집합입니다.

이러한 확장에 대 한 구현 정보를 참조 하세요 [ \[MS-SFU\]: 섹션(영문)을 사용자 서비스 및 제한 위임 프로토콜 사양](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx) MSDN에 있습니다.

S4U(Service for User) 확장과 비교하여 전달된 TGT(Ticket-Granting Ticket)를 포함한 Kerberos 위임의 기본 메시지 순서에 대한 자세한 내용은 [MS-SFU]: Kerberos 프로토콜 확장: 사용자 서비스 및 제한 위임 프로토콜 사양의 [1.3.3 프로토콜 개요](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx) 섹션(영문)을 참조하세요.

**리소스 기반 제한 위임은의 보안 요구 사항**

리소스 기반의 제한 위임 puts 제어 액세스 되는 리소스를 소유 하는 관리자의 손에 위임 합니다. 가 대리자를 신뢰할 수 있는 서비스 보다는 리소스 서비스의 특성에 따라 다릅니다. 결과적으로, 리소스 기반 제한 위임은 이전에 프로토콜 전환 제어 되는 신뢰할 수 있는-에-인증--위임을 위한 비트를 사용할 수 없습니다. KDC는 비트가 설정 된 것 처럼 제한 된 위임 리소스를 기반으로 수행 하는 경우 항상 프로토콜 전환을 허용 합니다.

KDC는 프로토콜 전환에 제한 하지 않으므로 리소스 관리자에 게이 컨트롤을 제공 하려면 두 개의 새 잘 알려진 Sid 도입 되었습니다.  이러한 Sid 프로토콜 전환을 발생 하 고 권한을 부여 하거나 필요에 따라 액세스를 제한 하려면 표준 액세스 제어 목록을 사용 하 여 사용할 수 있는지 여부를 식별 합니다.

|SID|설명|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|클라이언트의 id를 의미 하는 SID는 클라이언트 자격 증명의 소유 증명에 따라 인증 기관이 어설션 됩니다.|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|클라이언트의 id를 의미 하는 SID는 서비스에 의해 어설션 됩니다.|

백 엔드 서비스를 사용자가 인증 하는 방법을 확인 하려면 표준 ACL 식을 사용할 수 있습니다.

**리소스 기반 제한 된 위임을 어떻게 구성 합니까?**

사용자를 대신하여 프런트 엔드 서비스 액세스를 허용하도록 리소스 서비스를 구성하려면 Windows PowerShell cmdlet을 사용합니다.

-   주체 목록을 검색 하려면 사용 합니다 **Get-adcomputer**, **Get-adserviceaccount**, 및 **Get-aduser** cmdlet을 **속성 PrincipalsAllowedToDelegateToAccount** 매개 변수입니다.

-   리소스 서비스를 구성 하려면 사용 합니다 **New-adcomputer**, **New-adserviceaccount**를 **New-aduser**를 **Set-adcomputer**,  **Set-adserviceaccount**, 및 **Set-aduser** cmdlet의 **PrincipalsAllowedToDelegateToAccount** 매개 변수입니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
리소스 기반 제한 위임은 Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 도메인 컨트롤러 에서만 구성할 수 있지만 혼합 모드 포리스트에 적용 될 수 있습니다.

Windows Server 2012 실행 사용자에서 계정 도메인 유입 경로의 Windows Server 이전 버전 운영 체제를 실행 하는 프런트 엔드 및 백 엔드 도메인 사이의 모든 도메인 컨트롤러에 핫픽스를 적용 해야 합니다.  Windows Server 2008 R2 기반 도메인 컨트롤러가 있는 환경에서 리소스 기반의 제한 위임 KDC_ERR_POLICY 실패 핫픽스를 적용해야 합니다.
