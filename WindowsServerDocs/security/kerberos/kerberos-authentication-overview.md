---
title: Kerberos Authentication Overview
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 646c6309-e865-4be2-b415-44dd125af5c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 33712dc8502035bd9e47e1d2bdd4583eb8347dec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386310"
---
# <a name="kerberos-authentication-overview"></a>Kerberos Authentication Overview

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Kerberos는 사용자나 호스트의 ID를 확인하는 데 사용되는 인증 프로토콜입니다. 이 항목에는 Windows Server 2012 및 Windows 8의 Kerberos 인증에 대 한 정보가 포함 되어 있습니다.

## <a name="BKMK_OVER"></a>기능 설명
Windows Server 운영 체제는 공용 키 인증, 권한 부여 데이터 전송 및 위임을 위한 Kerberos 버전 5 인증 프로토콜 및 확장을 구현합니다. Kerberos 인증 클라이언트는 SSP\)\(보안 지원 공급자로 구현 되며, SSPI\)\(보안 지원 공급자 인터페이스를 통해 액세스할 수 있습니다. 초기 사용자 인증은 아키텍처의 Winlogon 단일 기호\-와 통합 됩니다.

Kerberos 키 배포 센터 \(KDC\)는 도메인 컨트롤러에서 실행 되는 다른 Windows Server 보안 서비스와 통합 됩니다. KDC는 도메인의 Active Directory Domain Services 데이터베이스를 보안 계정 데이터베이스로 사용 합니다. Active Directory Domain Services는 도메인 또는 포리스트 내의 기본 Kerberos 구현에 필요합니다.

## <a name="kerb_tr_Kerb_Benefits"></a>실용적인 응용 프로그램
도메인\-기반 인증에 Kerberos를 사용 하 여 얻을 수 있는 이점은 다음과 같습니다.

-   **위임 된 인증.**

    Windows 운영 체제에서 실행 되는 서비스는 클라이언트를 대신 하 여 리소스에 액세스할 때 클라이언트 컴퓨터를 가장할 수 있습니다. 대부분의 경우 서비스는 로컬 컴퓨터의 리소스에 액세스하여 클라이언트를 위한 작업을 완료할 수 있습니다. 클라이언트 컴퓨터가 서비스의 인증을 받으면 NTLM 및 Kerberos 프로토콜은 서비스가 로컬에서 클라이언트 컴퓨터를 가장하는 데 필요한 인증 정보를 제공합니다. 그러나 일부 분산 응용 프로그램은 프런트\-end 서비스가 클라이언트 컴퓨터의 id를 사용 하 여 다른 컴퓨터의 백 엔드 서비스\-에 연결 하는 경우에만 디자인 됩니다. Kerberos 인증은 서비스가 다른 서비스에 연결될 때 클라이언트를 대신할 수 있도록 하는 위임 메커니즘을 지원합니다.

-   **Single sign-on.**

    포리스트 또는 도메인 내에서 Kerberos 인증을 사용하면 사용자나 서비스는 자격 증명을 여러 번 요청하지 않고도 관리자가 허용한 리소스에 액세스할 수 있습니다. Winlogon을 통한 초기 도메인 로그온 후 Kerberos는 리소스에 대한 액세스가 시도될 때마다 포리스트 전체에서 자격 증명을 관리합니다.

-   **고도의.**

    Microsoft에서 Kerberos V5 프로토콜을 구현 하는 것은 IETF\)인터넷 엔지니어링 작업 Force \(에 권장 되는 표준\-추적 사양을 기반으로 합니다. 따라서 Windows 운영 체제에서 Kerberos 프로토콜은 Kerberos 프로토콜이 인증에 사용되는 다른 네트워크와의 상호 운용성을 위한 토대를 제공합니다. 또한 Microsoft는 Kerberos 프로토콜을 구현하기 위한 Windows 프로토콜 설명서를 게시합니다. 설명서에는 Microsoft의 Kerberos 프로토콜 구현에 대 한 기술 요구 사항, 제한 사항, 종속성 및 Windows\-특정 프로토콜 동작이 포함 되어 있습니다.

-   **서버에 대 한 보다 효율적인 인증.**

    Kerberos 이전의 NTLM 인증에서는 모든 클라이언트 컴퓨터나 서비스를 인증하기 위해 응용 프로그램 서버가 도메인 컨트롤러에 연결해야 했습니다. Kerberos 프로토콜을 사용 하면 갱신 가능한 세션 티켓이 인증을 통해\-전달 됩니다. 권한 특성 인증서 \(PAC\)\)의 유효성을 검사 해야 하는 경우가 아니면 서버는 도메인 컨트롤러 \(으로 이동할 필요가 없습니다. 대신 서버는 클라이언트에서 제공하는 자격 증명을 검사하여 클라이언트 컴퓨터를 인증할 수 있습니다. 클라이언트 컴퓨터는 특정 서버용 자격 증명을 한 번 가져온 다음 네트워크 로그온 세션 전체에서 해당 자격 증명을 다시 사용할 수 있습니다.

-   **상호 인증.**

    Kerberos 프로토콜을 사용하면 네트워크 연결 양쪽의 당사자가 연결 반대쪽의 당사자 엔터티를 확인할 수 있습니다. NTLM에서는 클라이언트가 서버의 id를 확인 하거나 한 서버에서 다른 서버에 대 한 id를 확인할 수 없습니다. NTLM 인증은 서버를 모두 유효하다고 가정하는 네트워크 환경용으로 설계되었습니다. Kerberos 프로토콜에서는 이러한 가정이 사용되지 않습니다.

## <a name="see-also"></a>참고 항목
[Windows 인증 개요](../windows-authentication/windows-authentication-overview.md)


