---
title: 도메인 가입 장치 공개 키 인증
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 80906e7cfe3740200938704a4b4eaf0759af303a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885034"
---
# <a name="domain-joined-device-public-key-authentication"></a>도메인 가입 장치 공개 키 인증

>적용 대상: Windows Server 2016의 경우 Windows 10

Kerberos에는 Windows Server 2012 및 Windows 8을 사용 하 여 시작 하는 인증서를 사용 하 여 로그인 하려면 도메인에 가입 된 장치에 대 한 지원이 추가 되었습니다. 이 변경에는 타사 공급 업체를 프로 비전 하 고 도메인 인증에 사용할 도메인에 가입 된 장치에 대 한 인증서를 초기화 하는 솔루션을 만들 수 있습니다. 

## <a name="automatic-public-key-provisioning"></a>자동 공용 키 프로 비전

Windows 10 버전 1507 및 Windows Server 2016 부터는 도메인 가입 장치의 자동으로 프로 비전 할 Windows Server 2016 도메인 컨트롤러 (DC)에 바인딩된 공개 키. 키를 프로 비전 되 면, Windows 도메인에 공개 키 인증을 사용할 수 있습니다.

### <a name="public-key-generation"></a>공용 키 생성
장치는 Credential Guard 실행 하는 경우 공개 키도 Credential Guard 보호 생성 됩니다. 

Credential Guard 사용할 수 없는 경우 TPM은 공개 키를 TPM으로 보호 생성 됩니다. 

모두를 사용할 수 있는 경우 키 생성 되지 않습니다 하 고 장치 암호를 사용 하 여 인증 될 수 있습니다.

### <a name="provisioning-computer-account-public-key"></a>컴퓨터 계정에 대 한 공개 키를 프로 비전
Windows 시작 되 면 해당 컴퓨터 계정에 대 한 공개 키가 프로 비전 하는 경우를 확인 합니다. 그러지 않으면 바인딩된 공개 키를 생성 하 고 해당 계정에 대 한 Windows Server 2016 또는 더 높은 DC를 사용 하 여 AD에서 구성 합니다. 모든 Dc 하위 수준 경우 키가 없습니다. 프로 비전 됩니다.

### <a name="configuring-device-to-only-use-public-key"></a>공개 키만 사용 하도록 장치를 구성
경우 그룹 정책 설정을 **인증서를 사용 하 여 장치 인증에 대 한 지원을** 로 설정 된 **Force**, 장치를 Windows Server 2016을 실행 하는 DC를 찾을 이상 인증 해야 합니다. 설정을 관리 템플릿 > 시스템 > Kerberos입니다.

### <a name="configuring-device-to-only-use-password"></a>만 암호를 사용 하는 장치를 구성 합니다.
하는 경우 그룹 정책 설정을 **인증서를 사용 하 여 장치 인증에 대 한 지원을** 사용 하지 않으면 암호는 항상 사용 됩니다. 설정을 관리 템플릿 > 시스템 > Kerberos입니다.

## <a name="domain-joined-device-authentication-using-public-key"></a>공개 키를 사용 하 여 도메인에 가입 된 장치 인증
Windows 도메인에 가입 된 장치에 대 한 인증서에 있는 경우 Kerberos 처음 사용 하 여 인증 인증서 및 암호를 사용 하 여 오류 다시 시도 합니다. 따라서 장치를에서 하위 수준 Dc로 인증할 수 있습니다.

자동으로 프로 비전 된 공개 키 자체 서명 된 인증서가 인증서 유효성 검사 키 트러스트 계정 매핑을 지원 하지 않는 도메인 컨트롤러에서 실패 합니다. 기본적으로 Windows 장치의 도메인 암호를 사용 하 여 인증을 다시 시도 합니다.


