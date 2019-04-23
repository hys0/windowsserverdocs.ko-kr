---
title: HGS에 대 한 인증서를 가져오려면
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 14ee8eb6431a266d05897160d241d63e8cdb09a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887734"
---
# <a name="obtain-certificates-for-hgs"></a>HGS에 대 한 인증서를 가져오려면

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

HGS를 배포할 때 보호 된 VM을 시작 하는 데 필요한 중요 한 정보를 보호 하는 데 사용 되는 인증서를 서명 및 암호화를 위해 묻는 메시지가 나타납니다.
이러한 인증서를 되지 HGS를 두고 실행 중인 호스트는 정상 임을 입증 된 경우에 해독 보호 된 VM 키만 사용 됩니다.
테 넌 트 (VM 소유자) 사용 하 여 공용 인증서의 절반의 보호 된 Vm을 실행 하려면 데이터 센터를 권한 부여.
이 섹션에서는 HGS에 대해 호환 되는 서명 및 암호화 인증서를 얻는 데 필요한 단계를 다룹니다.

## <a name="request-certificates-from-your-certificate-authority"></a>인증 기관에서 인증서를 요청 합니다.

필요 없이 신뢰할 수 있는 인증 기관에서 인증서를 얻는 것이 좋습니다.
이렇게 하면 VM 소유자는 이러한 권한을 부여 하는 보호 된 Vm을 실행 하려면 올바른 HGS 서버 (서비스 공급자 또는 데이터 센터)를 확인 합니다.
엔터프라이즈 시나리오에서 사용자 고유의 엔터프라이즈 CA를 사용 하 여 이러한 인증서를 발급할 수 있습니다.
호스팅 서비스 공급자 및 서비스 공급자는 잘 알려진, 공용 CA를 대신 사용 하 여 고려해 야 합니다.

("권장"으로 표시)를 제외 다음 인증서 속성을 사용 하 여 서명 및 암호화 인증서를 발급 되어야 합니다.

인증서 템플릿 속성 | 필요한 값 
------------------------------|----------------
암호화 공급자               | 모든 키 저장소 공급자 (KSP)입니다. 레거시 암호화 서비스 공급자 (Csp)는 **되지** 지원 합니다.
키 알고리즘                 | RSA
최소 키 크기              | 2048 비트
서명 알고리즘           | 권장: SHA256
Key usage(키 사용)                     | 디지털 서명을 *고* 데이터 암호화
확장 된 키 사용            | 서버 인증
키 갱신 정책            | 동일한 키로 갱신 합니다. 다른 키를 사용 하 여 HGS 인증서 갱신 시작에서 보호 된 Vm 수 없게 됩니다.
주체 이름                  | 권장: 회사 이름 또는 웹 주소입니다. 이 정보 보호 데이터 파일 마법사에서 VM 소유자에 게 표시 됩니다.

이러한 요구 사항은 하드웨어 또는 소프트웨어에서 지 원하는 인증서를 사용 하 여 적용 합니다.
보안상의 이유로 사용자가 만든 HGS 키의 보안 모듈 (HSM (하드웨어)를 시스템에 복사 하는 개인 키를 방지 하기 위해이 좋습니다.
위의 모든 특성을 사용 하 여 인증서를 요청할 HSM 공급 업체의 지침에 따라 및 설치 하 고 모든 HGS 노드에서 HSM KSP에 권한을 부여 해야 합니다.

모든 HGS 노드는 동일한 서명 및 암호화 인증서에 대 한 액세스를 해야 합니다.
소프트웨어 기반 인증서를 사용 하는 경우 암호를 사용 하 여 PFX 파일로 인증서를 내보낼 수 있으며 인증서를 관리 하는 HGS 허용 수 있습니다.
각 HGS 노드에서 로컬 컴퓨터의 인증서 저장소에 인증서를 설치 하 고 지문을 HGS를 제공 하려면 수도 있습니다.
두 옵션 모두에 대해 설명 합니다 [HGS 클러스터 초기화](guarded-fabric-initialize-hgs.md) 항목입니다.

## <a name="create-self-signed-certificates-for-test-scenarios"></a>테스트 시나리오에 대 한 자체 서명 된 인증서 만들기

HGS 랩 환경을 만드는 및 수행 하지 했거나 사용할 인증 기관, 경우에 자체 서명 된 인증서를 만들 수 있습니다.
실딩 데이터 파일 마법사에서 인증서 정보를 가져올 때 경고를 받게 되지만 모든 기능이 동일 하 게 유지 됩니다.

자체 서명 된 인증서를 만들고 PFX 파일로 내보내서 하려면 PowerShell에서 다음 명령을 실행 합니다.

```powershell
$certificatePassword = Read-Host -AsSecureString -Prompt "Enter a password for the PFX file"

$signCert = New-SelfSignedCertificate -Subject "CN=HGS Signing Certificate"
Export-PfxCertificate -FilePath .\signCert.pfx -Password $certificatePassword -Cert $signCert
Remove-Item $signCert.PSPath

$encCert = New-SelfSignedCertificate -Subject "CN=HGS Encryption Certificate"
Export-PfxCertificate -FilePath .\encCert.pfx -Password $certificatePassword -Cert $encCert
Remove-Item $encCert.PSPath
```

## <a name="request-an-ssl-certificate"></a>SSL 인증서를 요청 합니다.

Hyper-v 호스트 간에 전송 된 모든 키 및 중요 한 정보 및 메시지 수준에서 암호화 된 HGS-알려진 HGS 또는 Hyper-v가 네트워크 트래픽을 찾아낸 및 키를 가로채기를 방지 하는 키를 사용 하 여 정보를 암호화 하는 vm에 있습니다.
그러나 준수 reqiurements 했거나 단순히 Hyper-v 및 HGS 간의 모든 통신을 암호화 하려는 경우 전송 수준에서 모든 데이터를 암호화 하는 SSL 인증서를 사용 하 여 HGS를 구성할 수 있습니다.

Hyper-v 호스트와 HGS 노드 하므로 엔터프라이즈 인증 기관에서 SSL 인증서를 요청 하는 것이 좋습니다.를 제공한 SSL 인증서를 신뢰 해야 합니다. 인증서를 요청할 때는 다음을 지정 해야 합니다.

SSL 인증서 속성 | 필요한 값
-------------------------|---------------
주체 이름             | HGS 클러스터 (분산된 네트워크 이름)의 이름입니다. 제공 된 HGS 서비스 이름의 연결 됩니다 `Initialize-HgsServer` 및 HGS 도메인 이름입니다.
주체 대체 이름 | 하는 경우 사용할 다른 DNS 이름을 HGS 클러스터에 연결할 (예: 부하 분산 장치 뒤)를 인증서 요청의 SAN 필드에 해당 DNS 이름을 포함 해야 합니다.

HGS 서버를 초기화할 때이 인증서를 지정 하는 옵션에 나와 [첫 번째 HGS 노드 구성](guarded-fabric-initialize-hgs.md)합니다.
추가 하거나 사용 하 여 이후 시간에서 SSL 인증서를 변경할 수도 있습니다는 [집합 HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver?view=win10-ps) cmdlet.

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[HGS를 설치 합니다.](guarded-fabric-choose-where-to-install-hgs.md)