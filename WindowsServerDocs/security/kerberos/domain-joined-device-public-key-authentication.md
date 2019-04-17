---
title: "도메인 가입 장치 공개 키 인증"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 8/18/2017
ms.openlocfilehash: 65f39f4900fcd99ef90b160d3db7099edb73bc1c
ms.sourcegitcommit: e94838df702ff0135ebe7c179b228aa67b772d35
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="domain-joined-device-public-key-authentication"></a>도메인 가입 장치 공개 키 인증

>적용 대상: Windows Server 2016, Windows 10

Kerberos는 도메인에 가입 디바이스에 로그인 시작 하는 인증서를 사용 하 여 Windows 8 및 Windows Server 2012에 대 한 지원을 추가 합니다. 이 변경을 통해 제 3 자 공급 업체를 구축 하 고 초기화 도메인 인증에 사용 하 여 도메인 가입 디바이스용 인증서를 솔루션을 만들기 위해 합니다. 

## <a name="automatic-public-key-provisioning"></a>자동 공개 키 준비

도메인 가입 장치부터 Windows 10 버전 1507 및 Windows Server 2016, (DC) Windows Server 2016 도메인 컨트롤러에 바인딩된 공개 키를 구축 자동으로 합니다. 키가 제공 되 면 다음 Windows 인증을 사용할 수 공개 키를 도메인.

### <a name="public-key-generation"></a>공개 키를 생성
디바이스가 Credential Guard을 실행 중인 경우 공개 키는 Credential Guard로 보호 된 생성 됩니다. 

Credential Guard 사용할 수 없는 경우 TPM은 공개 키 TPM으로 보호 된 생성 됩니다. 

모두를 사용할 수 있는 경우 키를 생성 되지 및 디바이스 수만 암호를 사용 하 여 인증 합니다.

### <a name="provisioning-computer-account-public-key"></a>컴퓨터 계정 공개 키를 프로 비전
Windows를 시작 공개 키 컴퓨터 계정을 제공 되는 경우를 확인 합니다. 그렇지 않으면 바인딩된 공개 키를 생성 하 고 Windows Server 2016 또는 높은 DC 사용 하 여 광고에 해당 계정에 대 한 구성 합니다. 모든 Dc 하위 수준 인 경우 키가 없습니다. 프로 비전 됩니다.

### <a name="configuring-device-to-only-use-public-key"></a>만 공개 키를 사용 하 여 디바이스를 구성 합니다.
하는 경우 그룹 정책 설정을 **인증서를 사용 하 여 디바이스 인증에 대 한 지원을** 로 설정 되어 **힘**, 디바이스 DC Windows Server 2016 자동으로 실행 하는 검색을 이상이 인증을 해야 합니다. 관리 템플릿 가리키는 설정 > 시스템 > Kerberos 합니다.

### <a name="configuring-device-to-only-use-password"></a>디바이스에만 암호를 사용 하 여 구성
하는 경우 그룹 정책 설정을 **인증서를 사용 하 여 디바이스 인증에 대 한 지원을** 비활성화 되어 암호는 항상 사용 합니다. 관리 템플릿 가리키는 설정 > 시스템 > Kerberos 합니다.

## <a name="domain-joined-device-authentication-using-public-key"></a>도메인 가입 장치 인증 공개 키를 사용 하 여
Windows가 도메인에 가입 장치에 대 한 인증서, Kerberos 먼저 인증 인증서를 사용 하 여와 암호와 실패 다시 시도 합니다. 이 통해 하위 수준 Dc로에서 인증 하는 디바이스입니다.

자동으로 제공된 공개 키를 사용 하는 자체 서명된 인증서를 이후 계정 간의 키 신뢰를 지원 하지 않는 도메인 컨트롤러의 인증서 유효성 검사에 실패 합니다. 기본적으로 Windows 디바이스의 도메인 암호를 사용 하 여 인증 다시 시도 합니다.


