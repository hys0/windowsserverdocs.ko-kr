---
title: Kerberos Constrained Delegation Overview
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e6e62effcb875c0e3a1cdd6c886f3d74923e1b94
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403415"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 개요 항목에서는 Windows Server 2012 R2 및 Windows Server 2012에서 Kerberos 제한 위임에 대 한 새로운 기능을 설명 합니다.

**기능 설명**

Kerberos 제한 위임은 서비스에서 사용할 수 있는 보다 안전한 형식의 위임을 제공하기 위해 Windows Server 2003에 처음 도입되었습니다. Kerberos 제한 위임이 구성되면 이 기능은 지정된 서버가 사용자 대신 작업을 수행할 수 있는 서비스를 제한합니다. 이 경우 서비스의 도메인 계정을 구성하기 위해 도메인 관리자 권한이 필요하며, 계정이 단일 도메인으로 제한됩니다. 오늘날의 기업에서 프런트 엔드 서비스는 해당 도메인의 서비스와만 통합 되도록 제한 되지 않습니다.

도메인 관리자가 서비스를 구성한 이전 운영 체제에서 서비스 관리자는 기업이 소유한 리소스 서비스로 위임되는 프런트 엔드 서비스를 확인하는 데 사용할 수 있는 유용한 방법이 없는 상태입니다. 뿐만 아니라 리소스 서비스로 위임될 수 있는 프런트 엔드 서비스에 잠재적 공격 지점이 있습니다. 프런트 엔드 서비스를 호스팅하는 서버의 보안이 손상되고, 이 서비스가 리소스 서비스로 위임되도록 구성된 경우 리소스 서비스의 보안 역시 손상될 수 있습니다.

Windows Server 2012 R2 및 Windows Server 2012에서 서비스에 대 한 제한 된 위임을 구성 하는 기능이 도메인 관리자에서 서비스 관리자로 전송 되었습니다. 이렇게 하여 백 엔드 서비스 관리자가 프런트 엔드 서비스를 허용하거나 거부할 수 있습니다.

Windows Server 2003에서 도입된 제한 위임에 대한 자세한 내용은 [Kerberos 프로토콜 전환 및 제한 위임](https://technet.microsoft.com/library/cc739587(v=ws.10))(영문)을 참조하세요.

Kerberos 프로토콜의 Windows Server 2012 R2 및 Windows Server 2012 구현에는 제한 된 위임 전용 확장이 포함 되어 있습니다.  S4U2Proxy(Service for User to Proxy)를 통해 서비스에서 사용자에 대한 Kerberos 서비스 티켓을 사용하여 KDC(키 배포 센터)로부터 백 엔드 서비스에 대한 서비스 티켓을 얻을 수 있습니다. 이러한 확장을 통해 다른 도메인에 있을 수 있는 백 엔드 서비스 계정에 제한 된 위임을 구성할 수 있습니다. 이러한 확장에 대 한 자세한 내용은 [ @ no__t-1MS @ no__t-2를 참조 하세요. 섹션(영문)을 사용자 서비스 및 제한 위임 프로토콜 사양 @ no__t-0 (MSDN Library)

**실용적인 응용 프로그램**

제한 된 위임을 통해 서비스 관리자는 응용 프로그램 서비스가 사용자 대신 작업을 수행할 수 있는 범위를 제한 하 여 응용 프로그램 트러스트 경계를 지정 하 고 적용할 수 있습니다. 서비스 관리자는 백 엔드 서비스에 위임할 수 있는 프런트 엔드 서비스 계정을 구성할 수 있습니다.

Windows Server 2012 R2 및 Windows Server 2012에서 도메인 간 제한 위임을 지원 함으로써 ISA (Microsoft Internet Security and 가속화) 서버, Microsoft Forefront Threat Management Gateway, Microsoft Exchange 등의 프런트 엔드 서비스를 지원 합니다. Outlook 웹 액세스 (OWA) 및 Microsoft SharePoint Server 제한 된 위임을 사용 하 여 다른 도메인의 서버에 인증 하도록 구성할 수 있습니다. 그러면 기존 Kerberos 인프라를 사용한 도메인 간 서비스 솔루션이 지원됩니다. Kerberos 제한 위임은 도메인 관리자나 서비스 관리자가 관리할 수 있습니다.

## <a name="resource-based-constrained-delegation-across-domains"></a>여러 도메인에 걸친 리소스 기반 제한 위임

프런트 엔드 및 리소스 서비스가 같은 도메인에 있지 않아도 Kerberos 제한 위임을 사용하여 제한 위임을 제공할 수 있습니다. 서비스 관리자는 리소스 서비스의 계정 개체에 대해 사용자를 가장할 수 있는 프런트 엔드 서비스의 도메인 계정을 지정하여 새 위임을 구성할 수 있습니다.

**이와 같은 변경을 통해 더해지는 가치**

도메인 간 제한 위임을 지원함으로써 제한 위임을 사용하도록 서비스를 구성하여 제한되지 않은 위임을 사용하지 않고 다른 도메인의 서버로부터 인증을 받을 수 있습니다. 그러면 서비스로의 위임을 위해 프런트 엔드 서비스를 트러스트하지 않고 기존의 Kerberos 인프라를 사용한 도메인 간 서비스 솔루션에 대한 인증이 지원됩니다.

또한 서버에서 위임 된 id의 원본을 위임 도메인 관리자에서 리소스 소유자로 신뢰 해야 하는지 여부에 대 한 결정을 내립니다.

**달라진 기능**

기본 프로토콜의 변경을 통해 도메인 간 제한 위임을 사용할 수 있습니다. Kerberos 프로토콜의 Windows Server 2012 R2 및 Windows Server 2012 구현에는 S4U2Proxy (Service for User to Proxy) 프로토콜에 대 한 확장이 포함 되어 있습니다. 이 확장은 서비스에서 사용자에 대한 Kerberos 서비스 티켓을 사용하여 KDC(키 배포 센터)로부터 백 엔드 서비스에 대한 서비스 티켓을 얻을 수 있도록 해주는 Kerberos 프로토콜에 대한 확장 집합입니다.

이러한 확장에 대 한 구현 정보는 [ @ no__t-1MS-SFU @ no__t-2를 참조 하세요. 섹션(영문)을 사용자 서비스 및 제한 위임 프로토콜 사양 @ no__t-0 (MSDN)

S4U(Service for User) 확장과 비교하여 전달된 TGT(Ticket-Granting Ticket)를 포함한 Kerberos 위임의 기본 메시지 순서에 대한 자세한 내용은 [MS-SFU]: Kerberos 프로토콜 확장: 사용자 서비스 및 제한 위임 프로토콜 사양의 [1.3.3 프로토콜 개요](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx) 섹션(영문)을 참조하세요.

**리소스 기반 제한 위임의 보안 영향**

리소스 기반 제한 위임은 액세스 하는 리소스를 소유 하 고 있는 관리자에 게 위임 제어를 적용 합니다. 대리자에 신뢰 되는 서비스가 아닌 리소스 서비스의 특성에 따라 다릅니다. 따라서 리소스 기반 제한 위임은 이전에 프로토콜 전환을 제어 한 트러스트-인증-위임 비트를 사용할 수 없습니다. KDC는 비트가 설정 된 것 처럼 리소스 기반 제한 위임을 수행할 때 항상 프로토콜 전환을 허용 합니다.

KDC는 프로토콜 전환을 제한 하지 않으므로, 리소스 관리자에 게이 컨트롤을 제공 하기 위해 잘 알려진 두 개의 새 Sid가 도입 되었습니다.  이러한 Sid는 프로토콜 전환이 발생 했는지 여부를 확인 하 고 표준 액세스 제어 목록과 함께 사용 하 여 필요에 따라 액세스를 허용 하거나 제한할 수 있습니다.

|SID|설명|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|클라이언트의 id가 클라이언트 자격 증명의 소유 증명을 기반으로 인증 기관에 의해 어설션 됨을 의미 하는 SID입니다.|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|클라이언트의 id가 서비스에 의해 어설션 됨을 의미 하는 SID입니다.|

백 엔드 서비스는 표준 ACL 식을 사용 하 여 사용자가 인증 된 방법을 결정할 수 있습니다.

**리소스 기반 제한 위임을 구성 하려면 어떻게 해야 하나요?**

사용자를 대신하여 프런트 엔드 서비스 액세스를 허용하도록 리소스 서비스를 구성하려면 Windows PowerShell cmdlet을 사용합니다.

-   보안 주체 목록을 검색 하려면 **PrincipalsAllowedToDelegateToAccount** 매개 변수를 사용 하 여 **uninstall-adserviceaccount** **및 get** **adcomputer** cmdlet을 사용 합니다.

-   리소스 서비스를 구성 하려면 다음을 사용 하 여 **새-ADComputer**, **uninstall-adserviceaccount**, **새-adcomputer**, **uninstall-adserviceaccount**및 **set-** **adcomputer** cmdlet **을 사용 합니다. PrincipalsAllowedToDelegateToAccount** 매개 변수입니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
리소스 기반 제한 위임은 Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 도메인 컨트롤러 에서만 구성할 수 있지만 혼합 모드 포리스트 내에서 적용할 수 있습니다.

Windows Server 이전 버전의 운영 체제를 실행 하는 프런트 엔드 도메인 및 백 엔드 도메인 간 조회 경로의 사용자 계정 도메인에서 Windows Server 2012를 실행 하는 모든 도메인 컨트롤러에 다음 핫픽스를 적용 해야 합니다.  Windows Server 2008 R2 기반 도메인 컨트롤러가 있는 환경에서 리소스 기반 제한 위임 KDC_ERR_POLICY 실패 (https://support.microsoft.com/en-gb/help/2665790/resource-based-constrained-delegation-kdc-err-policy-failure-in-enviro).
