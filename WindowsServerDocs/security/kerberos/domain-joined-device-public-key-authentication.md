---
title: 도메인 가입 장치 공개 키 인증
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 616ebf1a8e01f84618d22d535609a0dc8414d718
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403497"
---
# <a name="domain-joined-device-public-key-authentication"></a>도메인 가입 장치 공개 키 인증

>적용 대상: Windows Server 2016의 경우 Windows 10

Windows Server 2012 및 Windows 8부터 인증서를 사용 하 여 도메인에 가입 된 장치에 로그인 하는 기능이 추가 되었습니다. 이러한 변경을 통해 타사 공급 업체는 도메인에 가입 된 장치에서 도메인 인증에 사용할 인증서를 프로 비전 하 고 초기화 하는 솔루션을 만들 수 있습니다. 

## <a name="automatic-public-key-provisioning"></a>자동 공개 키 프로 비전

Windows 10 버전 1507 및 Windows Server 2016부터 도메인에 가입 된 장치는 Windows Server 2016 DC (도메인 컨트롤러)에 바인딩된 공개 키를 자동으로 프로 비전 합니다. 키가 프로 비전 되 면 Windows는 도메인에 대 한 공개 키 인증을 사용할 수 있습니다.

### <a name="public-key-generation"></a>공개 키 생성
장치에서 Credential Guard를 실행 하는 경우에는 Credential Guard에 의해 보호 되는 공개 키가 생성 됩니다. 

Credential Guard를 사용할 수 없고 TPM이 인 경우 TPM이 보호 하는 공개 키가 생성 됩니다. 

둘 다 사용할 수 없는 경우에는 키가 생성 되지 않으며 장치는 암호만 사용 하 여 인증할 수 있습니다.

### <a name="provisioning-computer-account-public-key"></a>프로 비전 컴퓨터 계정 공개 키
Windows가 시작 될 때 해당 컴퓨터 계정에 대해 공개 키가 프로 비전 되는지 확인 합니다. 그렇지 않으면 바인딩된 공개 키를 생성 하 고 Windows Server 2016 이상 DC를 사용 하 여 AD의 계정에 대해 구성 합니다. 모든 Dc가 하위 수준이 면 키가 프로 비전 되지 않습니다.

### <a name="configuring-device-to-only-use-public-key"></a>공개 키만 사용 하도록 장치 구성
**인증서를 사용 하 여 장치 인증에 대 한 지원** 그룹 정책 설정이 **강제**로 설정 된 경우 장치는 Windows Server 2016 이상을 실행 하는 DC를 검색 하 여 인증 해야 합니다. 설정은 관리 템플릿 > System > Kerberos에 있습니다.

### <a name="configuring-device-to-only-use-password"></a>암호를 사용 하도록 장치 구성
**인증서를 사용 하는 장치 인증에 대 한** 그룹 정책 설정이 사용 하지 않도록 설정 된 경우 항상 암호를 사용 합니다. 설정은 관리 템플릿 > System > Kerberos에 있습니다.

## <a name="domain-joined-device-authentication-using-public-key"></a>공개 키를 사용 하 여 도메인에 가입 된 장치 인증
Windows에 도메인 가입 장치에 대 한 인증서가 있는 경우 Kerberos는 먼저 인증서를 사용 하 여 인증 하 고 암호를 사용 하 여 실패를 다시 시도 합니다. 그러면 장치에서 하위 Dc에 인증할 수 있습니다.

자동으로 프로 비전 된 공개 키에는 자체 서명 된 인증서가 있으므로 키 신뢰 계정 매핑을 지원 하지 않는 도메인 컨트롤러에서 인증서 유효성 검사가 실패 합니다. 기본적으로 Windows는 장치의 도메인 암호를 사용 하 여 인증을 다시 시도 합니다.


