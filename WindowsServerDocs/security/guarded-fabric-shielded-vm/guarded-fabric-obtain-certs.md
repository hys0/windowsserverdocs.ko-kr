---
title: HGS 용 인증서 가져오기
ms.prod: windows-server
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: da1ae4bacd5a6b2e38b22930aacf06f65b16bb29
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856536"
---
# <a name="obtain-certificates-for-hgs"></a>HGS 용 인증서 가져오기

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

HGS를 배포할 때 보호 된 VM을 시작 하는 데 필요한 중요 한 정보를 보호 하는 데 사용 되는 서명 및 암호화 인증서를 제공 하 라는 메시지가 표시 됩니다.
이러한 인증서는 HGS를 떠나지 않으며, 실행 중인 호스트가 정상 상태를 증명 한 경우 보호 된 VM 키의 암호를 해독 하는 데만 사용 됩니다.
테 넌 트 (VM 소유자)는 인증서의 공개 부분을 사용 하 여 보호 된 Vm을 실행 하도록 데이터 센터에 권한을 부여 합니다.
이 섹션에서는 HGS에 대해 호환 되는 서명 및 암호화 인증서를 가져오는 데 필요한 단계에 대해 설명 합니다.

## <a name="request-certificates-from-your-certificate-authority"></a>인증 기관에서 인증서 요청

반드시 필요한 것은 아니지만 신뢰할 수 있는 인증 기관에서 인증서를 가져오는 것이 좋습니다.
이렇게 하면 VM 소유자가 적절 한 HGS 서버 (즉, 서비스 공급자 또는 데이터 센터)에 게 보호 된 Vm을 실행할 수 있는 권한을 부여 하 고 있는지 확인 하는 데 도움이 됩니다.
엔터프라이즈 시나리오에서는 사용자 고유의 엔터프라이즈 CA를 사용 하 여 이러한 인증서를 발급 하도록 선택할 수 있습니다.
호스팅 서비스 공급자 및 서비스 공급자는 잘 알려진 공용 CA를 대신 사용 하는 것을 고려해 야 합니다.

서명 및 암호화 인증서 모두 다음 certificiate 속성을 사용 하 여 발급 되어야 합니다 ("권장"으로 표시 되지 않은 경우).

인증서 템플릿 속성 | 필요한 값 
------------------------------|----------------
암호화 공급자               | 모든 KSP (키 저장소 공급자)입니다. 레거시 Csp (암호화 서비스 공급자)는 지원 **되지 않습니다** .
키 알고리즘                 | RSA
최소 키 크기              | 2048비트
서명 알고리즘           | 권장: SHA256
키 사용                     | 디지털 서명 *및* 데이터 암호화
확장 된 키 사용            | 서버 인증
키 갱신 정책            | 동일한 키를 사용 하 여 갱신 합니다. 다른 키를 사용 하 여 HGS 인증서를 갱신 하면 보호 된 Vm이 시작 되지 않습니다.
주체 이름                  | 권장: 회사의 이름 또는 웹 주소입니다. 이 정보는 보호 데이터 파일 마법사에서 VM 소유자에 게 표시 됩니다.

이러한 요구 사항은 하드웨어 또는 소프트웨어에 의해 지원 되는 인증서를 사용 하는지에 따라 적용 됩니다.
보안상의 이유로 개인 키가 시스템에 복사 되지 않도록 HSM (하드웨어 보안 모듈)에서 HGS 키를 만드는 것이 좋습니다.
HSM 공급 업체의 지침에 따라 위의 특성으로 인증서를 요청 하 고 모든 HGS 노드에 HSM KSP를 설치 하 고 권한을 부여 해야 합니다.

모든 HGS 노드는 동일한 서명 및 암호화 인증서에 액세스 해야 합니다.
소프트웨어 지원 인증서를 사용 하는 경우 암호를 사용 하 여 인증서를 PFX 파일로 내보내고, HGS에서 인증서를 관리 하도록 허용할 수 있습니다.
각 HGS 노드의 로컬 컴퓨터 인증서 저장소에 인증서를 설치 하도록 선택 하 고 지문을 HGS에 제공할 수도 있습니다.
두 옵션은 모두 [HGS 클러스터 초기화](guarded-fabric-initialize-hgs.md) 항목에 설명 되어 있습니다.

## <a name="create-self-signed-certificates-for-test-scenarios"></a>테스트 시나리오에 대 한 자체 서명 된 인증서 만들기

HGS 랩 환경을 만들고 인증 기관을 사용 하지 않으려는 경우 자체 서명 된 인증서를 만들 수 있습니다.
보호 데이터 파일 마법사에서 인증서 정보를 가져올 때 경고가 표시 되지만 모든 기능은 동일 하 게 유지 됩니다.

자체 서명 된 인증서를 만들어 PFX 파일로 내보내려면 PowerShell에서 다음 명령을 실행 합니다.

```powershell
$certificatePassword = Read-Host -AsSecureString -Prompt "Enter a password for the PFX file"

$signCert = New-SelfSignedCertificate -Subject "CN=HGS Signing Certificate"
Export-PfxCertificate -FilePath .\signCert.pfx -Password $certificatePassword -Cert $signCert
Remove-Item $signCert.PSPath

$encCert = New-SelfSignedCertificate -Subject "CN=HGS Encryption Certificate"
Export-PfxCertificate -FilePath .\encCert.pfx -Password $certificatePassword -Cert $encCert
Remove-Item $encCert.PSPath
```

## <a name="request-an-ssl-certificate"></a>SSL 인증서 요청

Hyper-v 호스트와 HGS 사이에서 전송 되는 모든 키와 중요 한 정보는 메시지 수준에서 암호화 됩니다. 즉,이 정보는 HGS 또는 Hyper-v로 알려진 키로 암호화 되므로 누군가가 네트워크 트래픽을 스니핑 하 고 Vm에 대 한 키를 도용 하는 것을 방지할 수 있습니다.
그러나 준수를 reqiurements 하거나 Hyper-v와 HGS 간의 모든 통신을 암호화 하는 것이 좋습니다. 전송 수준에서 모든 데이터를 암호화 하는 SSL 인증서를 사용 하 여 HGS를 구성할 수 있습니다.

Hyper-v 호스트와 HGS 노드 모두 사용자가 제공 하는 SSL 인증서를 신뢰 해야 하므로 엔터프라이즈 인증 기관에서 SSL 인증서를 요청 하는 것이 좋습니다. 인증서를 요청할 때 다음을 지정 해야 합니다.

SSL 인증서 속성 | 필요한 값
-------------------------|---------------
주체 이름             | HGS 클러스터의 이름 (분산 네트워크 이름 또는 가상 컴퓨터 개체 FQDN 이라고 함)입니다. `Initialize-HgsServer`에 제공 된 HGS 서비스 이름과 HGS 도메인 이름을 연결 하는 것입니다.
주체 대체 이름 | 다른 DNS 이름을 사용 하 여 HGS 클러스터에 연결 하는 경우 (예: 부하 분산 장치 뒤에 있는 경우) 인증서 요청의 SAN 필드에 해당 DNS 이름을 포함 해야 합니다.

HGS 서버를 초기화할 때이 인증서를 지정 하는 옵션은 [첫 번째 hgs 노드 구성](guarded-fabric-initialize-hgs.md)에서 설명 합니다.
나중에 [HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver?view=win10-ps) cmdlet을 사용 하 여 SSL 인증서를 추가 하거나 변경할 수도 있습니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS 설치](guarded-fabric-choose-where-to-install-hgs.md)