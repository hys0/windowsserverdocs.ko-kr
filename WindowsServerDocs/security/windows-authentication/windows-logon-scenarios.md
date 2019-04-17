---
title: "Windows 로그온 시나리오"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66b7c568-67b7-4ac9-a479-a5a3b8a66142
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d6a1d52bee3c2d14ea83ccb794ecea1872868df5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="windows-logon-scenarios"></a>Windows 로그온 시나리오

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

일반적인 Windows 로그온 및 로그인 시나리오 여기 참조 IT 전문가 위한 요약 되어 있습니다.

Windows 운영 체제 및 네트워크 리소스에 액세스 로컬에 유효한 계정 사용 하 여 컴퓨터에 로그온 하는 모든 사용자가 필요합니다. Windows 기반 컴퓨터 구현 사용자가 인증 로그온 하 여 리소스를 보호 합니다. After a user is authenticated, authorization and access control technologies implement the second phase of protecting resources: determining if the authenticated user is authorized to access a resource.

이 항목의 내용을에 지정 된 Windows 버전에 적용는 **에 적용** 이 항목의 시작 부분에 목록입니다.

또한 응용 프로그램 및 서비스에 로그인 응용 프로그램 또는 서비스에서 제공 되는 이러한 리소스에 액세스 하기 위해 사용자가 필요할 수 있습니다. 로그인 프로세스는 유효한 계정과 올바른 자격 증명은 필요 하지만 로그온 정보는 저장 로컬 컴퓨터에서 보안 계정을 관리자 (삼로) 데이터베이스 및 Active Directory에 해당 하는 경우 로그온 프로세스가 유사 합니다. 로그인 자격 증명 하 고 계정 정보 응용 프로그램 또는 서비스에서 관리 되 고 필요한 경우 자격 증명 락커에 로컬로 저장 될 수 있습니다.

인증의 작동 방식을 이해 참조 [Windows 인증 개념](windows-authentication-concepts.md)합니다.

이 항목에서는 다음과 같은 경우에 설명 합니다.

-   [대화형 로그온](#BKMK_InteractiveLogon)

-   [네트워크 로그온](#BKMK_NetworkLogon)

-   [스마트 카드 로그온](#BKMK_SmartCardLogon)

-   [생체 인식 로그온](#BKMK_BioLogon)

## <a name="BKMK_InteractiveLogon"></a>대화형 로그온
로그온 프로세스 중 하나 자격 증명 입력 대화 상자에서 자격 증명을 입력 하는 경우 스마트 카드 스마트 카드 판독기에 삽입할 때 또는 생체 인식 하는 디바이스와 상호 작용할 때 시작 합니다. 사용자가 컴퓨터에 로그온 할 로컬 사용자 계정이 나 도메인 계정을 사용 하 여 대화형 로그온을 수행할 수 있습니다.

다음 그림 대화형 로그온 요소와 로그온 합니다.

![대화형 로그온 요소와 로그온 프로세스를 보여 주는 다이어그램](../media/windows-logon-scenarios/AuthN_LSA_Architecture_Client.gif)

**Windows 클라이언트 인증 건축물**

### <a name="BKMK_LocaDomainLogon"></a>로컬 및 도메인 로그온
도메인 로그온 한 사용자가 제시 자격 증명 로컬 로그온, 계정 이름 및 암호 또는 인증서, Active Directory 도메인 정보 등을 위해 필요한 모든 요소를 포함 합니다. 프로세스 Active Directory 도메인 하거나 사용자의 로컬 컴퓨터에서 보안 데이터베이스에는 사용자의 id를 확인합니다. 사용자 도메인에 대 한이 필수 로그온 프로세스 해제할 수 없습니다.

사용자는 두 가지 방법 중 하나 대화형 컴퓨터에 로그온을 수행할 수 있습니다.

-   로컬에서 때 사용자가 직접 물리적 액세스할 수는 컴퓨터 또는 컴퓨터가 네트워크 컴퓨터의 일부입니다.

    로컬 로그온 로컬 컴퓨터에서 Windows 리소스에 액세스 권한이 부여 됩니다. 로컬 로그온 하면 사용자가 사용자 계정에는 보안 계정을 관리자 (삼로) 로컬 컴퓨터에 있어야 합니다. 삼로 보호 하 고 사용자 및 그룹 로컬 컴퓨터 레지스트리에 저장 된 보안 계정의 형식 정보를 관리 합니다. 컴퓨터에서 네트워크 액세스를 수 있지만 필요 하지 않습니다. 로컬 사용자 계정 및 그룹 구성원 정보 로컬 리소스에 대 한 액세스를 관리 하는 데 사용 됩니다.

    네트워크 로그온 권한이 정의 된 대로만 자격 증명의 액세스 토큰 네트워크에 연결 된 컴퓨터에서 모든 리소스 뿐 아니라 로컬 컴퓨터에서 Windows 리소스에 액세스할 수 부여 합니다. 로컬 로그온 한 네트워크 로그온 하면 사용자가 사용자 계정에는 보안 계정을 관리자 (삼로) 로컬 컴퓨터에 필요 합니다. 로컬 사용자 계정 및 그룹 구성원 정보는 현지 리소스에 대 한 액세스를 관리 하는 데 하 고 사용자에 대 한 액세스 토큰 정의 어떤 리소스 네트워크에 연결 된 컴퓨터에 액세스할 수 있습니다.

    네트워크 로그온 하 고 로컬 로그온 액세스 도메인 리소스를 사용할 수 있는 사용자와 컴퓨터 권한을 부여한 충분 하지 않습니다.

-   원격으로 터미널 서비스 또는 RDS 원격 데스크톱 서비스 (), 경우 로그온이 더 이상 서비스 공급자는 원격 대화형 합니다.

대화형 로그온 한 후 Windows는 사용자를 대신 하 여 응용 프로그램을 실행 하 고 사용자 해당 응용 프로그램와 상호 작용할 수 있습니다.

로컬 로그온 로컬 컴퓨터에 리소스에 액세스 하거나 네트워크에 연결 된 컴퓨터에서 리소스 권한이 부여 됩니다. 컴퓨터가 도메인에 가입, Winlogon 기능은 도메인에 로그온 할 때 시도 합니다.

도메인 로그온 로컬에 액세스할 수 있는 권한을 사용자 및 도메인 리소스 부여 합니다. 도메인 로그온 사용자 Active Directory에 사용자 계정이 있어야 합니다. 컴퓨터 Active Directory 도메인에 있는 계정이 있어야 하 고 실제로 네트워크에 연결 되어 있습니다. 사용자는 도메인 또는 로컬 컴퓨터에 로그온 할 때 사용자 권한이 있어야 합니다. 도메인 계정 정보 사용자 및 그룹 구성원 정보 도메인 및 로컬 리소스에 대 한 액세스를 관리 하는 데 사용 됩니다.

### <a name="BKMK_RemoteLogon"></a>원격 로그온
Windows에서 원격 로그온 통해 다른 컴퓨터에 액세스 하는 원격 데스크톱 프로토콜 (RDP)에 의존 합니다. 해야 이미 있는 성공적으로 로그인 클라이언트 컴퓨터에서 원격 연결을 시도 하기 전에, 대화형 로그온 프로세스 성공적으로 완료 됩니다.

RDP 원격 데스크톱 클라이언트를 사용 하 여 사용자가 입력 하는 자격 증명을 관리 합니다. 대상 컴퓨터를 위한 자격 증명 하 고 사용자 해당 대상 컴퓨터에서 계정이 있어야 합니다. 또한 대상 컴퓨터 원격 연결을 수락 하도록 설정 해야 합니다. 대상 컴퓨터 자격 증명 인증 프로세스를 수행 하려고 전송 됩니다. 인증에 성공 로컬에 연결 되어 있고 네트워크 리소스 액세스할 수 있는 제공된 자격 증명을 사용 하 여 합니다.

## <a name="BKMK_NetworkLogon"></a>네트워크 로그온
네트워크 로그온 사용자, 서비스 또는 컴퓨터 인증 수행한 후에 사용할 수 있습니다. 네트워크 로그온 하는 동안 프로세스 데이터 수집을 자격 증명 입력 대화 상자를 사용 하지 않습니다. 대신, 이전에 자격 증명을 설정 하거나 다른 방법을 자격 증명을 수집 하는 데 사용 됩니다. 이 프로세스에 액세스 하려고 사용자는 네트워크 서비스는 사용자의 id를 확인 합니다. 이 프로세스를 제공할 수 있는 다른 자격 증명 하지 않은 사용자에 게 일반적으로 표시 되지 않습니다.

이러한 유형의 인증을 제공 하려면의 보안 시스템에 이러한 인증 메커니즘 포함 됩니다.

-   Kerberos 5 버전 프로토콜

-   공개 키 인증서

-   보안 소켓 Transport Layer/TLS 계층 보안 (SSL /)

-   요약

-   NTLM, for compatibility with Microsoft Windows NT 4.0-based systems

위의 대화형 로그온 다이어그램은 요소 및 프로세스에 대 한 정보를 참조 합니다.

## <a name="BKMK_SmartCardLogon"></a>스마트 카드 로그온
스마트 카드에 로그온 하지 로컬 계정 도메인 계정에만 사용할 수 있습니다. 스마트 카드 인증 Kerberos 인증 프로토콜을 사용을 해야 합니다. Windows 2000 server, Windows 기반 운영 체제의 공개 키 확장을 소개 프로토콜의 초기 인증 요청 구현 Kerberos. In contrast to shared secret key cryptography, public key cryptography is asymmetric, that is, two different keys are needed: one to encrypt, another to decrypt. 함께 모두 작업을 수행 하는 데 필요한 키 개인 월 공개 키 쌍을 확인 합니다.

일반적인 로그온 세션을 시작 하려면 사용자만 사용자에 게 기본 Kerberos 프로토콜 인프라 알려진 정보를 제공 하 여 신원을 증명 해야 합니다. 비밀 정보는 암호화 공유 키 사용자의 암호에서 파생 되었습니다. 공유 비밀 키는 대칭적 암호화와 해독 같은 키를 사용 됩니다.

다음 다이어그램은 요소 및 스마트 카드 로그온 하는 데 필요한 프로세스를 보여 줍니다.

![요소 및 스마트 카드 로그온 하는 데 필요한 프로세스를 보여 주는 다이어그램](../media/windows-logon-scenarios/SmartCardCredArchitecture.gif)

**스마트 카드 자격 증명 공급자 구조**

암호를 대신 스마트 카드를 사용 하면 사용자의 암호에서 파생 공유 비밀 키를 사용자의 스마트 카드에 저장 된 개인 월 공개 키 쌍 대체 됩니다. 개인 키 스마트 카드에만 저장 됩니다. 공개 키 가능 사용할 수 있는 소유자 기밀 정보 교환 하려면 연락처가 누구 모든 사용자에 게 합니다.

Windows의 스마트 카드 로그온 프로세스에 대 한 자세한 내용은 참조 [어떻게 스마트 카드로 로그인 Windows의 작동](https://technet.microsoft.com/library/ff404285.aspx)합니다.

## <a name="BKMK_BioLogon"></a>생체 인식 로그온
디바이스를 캡처하고, 지문 같은 보물의 디지털 특징 빌드 사용 됩니다. 디지털이 표현은 같은 인공의 샘플 비교 다음 되 고 두를 비교 성공적으로 인증 발생할 수 있습니다. 에 지정 된 운영 체제 중 하나를 실행 하는 컴퓨터의 **적용** 목록이이 항목의 시작 부분에 로그온이 형식을이 동의 하도록 구성할 수 있습니다. 그러나 로컬 로그온, 생체 인식 로그온 구성만 된 경우 사용자 Active Directory 도메인에 액세스할 때 도메인 자격 증명을 제공 해야 합니다.

## <a name="additional-resources"></a>추가 리소스
Windows 로그온 과정 자격 증명을 관리 하는 방법에 대 한 정보를 참조 하세요. [자격 증명 관리 Windows 인증에서](https://technet.microsoft.com/library/dn169014.aspx)합니다.

[Windows 로그온 및 인증 기술 개요](https://technet.microsoft.com/library/dn169029.aspx)


