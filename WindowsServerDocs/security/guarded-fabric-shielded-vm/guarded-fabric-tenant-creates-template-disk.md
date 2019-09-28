---
title: 테 넌 트 용 보호 된 Vm-템플릿 디스크 만들기-선택 사항
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: c1992f8b-6f88-4dbc-b4a5-08368bba2787
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8e5080dd74506e86687dddb7be0fd35af92f5b56
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403434"
---
# <a name="shielded-vms-for-tenants---creating-a-template-disk-optional"></a>테 넌 트 용 보호 된 Vm-템플릿 디스크 만들기 (선택 사항)

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

새 보호 된 VM을 만들려면 특별히 준비 되 고 서명 된 템플릿 디스크를 사용 해야 합니다. 서명 된 템플릿 디스크의 메타 데이터는 디스크가 생성 된 후 수정 되지 않고 보호 된 Vm을 만드는 데 사용할 수 있는 디스크를 제한 하는 테 넌 트로 사용할 수 있도록 하는 데 도움이 됩니다. 이 디스크를 제공 하는 한 가지 방법은이 항목에서 설명 하는 것 처럼 사용자를 위한 테 넌 트를 만드는 것입니다. 

> [!IMPORTANT]
> 선호 하는 경우 호스팅 서비스 공급자가 제공 하는 템플릿 디스크를 대신 사용할 수 있습니다. 이 작업을 수행 하는 경우 해당 템플릿 디스크를 사용 하 여 테스트 VM을 배포 하 고 사용자 고유의 도구 (바이러스 백신, 취약성 스캐너 등)를 실행 하 여 디스크가 신뢰할 수 있는 상태 인지 실제로 확인 하는 것이 중요 합니다.

## <a name="prepare-an-operating-system-vhdx"></a>운영 체제 VHDX 준비

보호 된 템플릿 디스크를 만들려면 먼저 템플릿 디스크 마법사를 통해 실행 되는 OS 디스크를 준비 해야 합니다. 이 디스크는 보호 된 Vm에서 OS 디스크로 사용 됩니다. 기존 도구를 사용 하 여이 디스크를 만들 수 있습니다 (예: DISM (Microsoft Desktop Image Service Manager)). 또는 새 VHDX를 사용 하 여 VM을 수동으로 설정 하 고 해당 디스크에 OS를 설치 합니다. 디스크를 설정 하는 경우 2 세대 및/또는 차폐 Vm과 관련 된 다음 요구 사항을 준수 해야 합니다. 

| VHDX에 대 한 요구 사항 | Reason |
|-----------|----|
|GPT (GUID 파티션 테이블) 디스크 여야 합니다. | UEFI를 지원 하기 위해 2 세대 가상 컴퓨터에 필요|
|디스크 유형은 **동적**이 아닌 **기본** 이어야 합니다. <br>참고: 이는 Hyper-v에서 지 원하는 "동적 확장" VHDX 기능이 아니라 논리 디스크 유형을 나타냅니다. | BitLocker는 동적 디스크를 지원 하지 않습니다.|
|디스크에 파티션이 두 개 이상 있습니다. 한 파티션에는 Windows가 설치 된 드라이브가 포함 되어야 합니다. BitLocker가 암호화 하는 드라이브입니다. 다른 파티션은 부팅 로더를 포함 하 고 컴퓨터를 시작할 수 있도록 암호화 되지 않은 상태로 유지 되는 활성 파티션입니다.|BitLocker에 필요|
|파일 시스템이 NTFS입니다. | BitLocker에 필요|
|VHDX에 설치 된 운영 체제는 다음 중 하나입니다.<br>-Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 <br>-Windows 10, Windows 8.1, Windows 8| 2 세대 가상 컴퓨터 및 Microsoft 보안 부팅 템플릿을 지 원하는 데 필요 합니다.|
|운영 체제를 일반화 해야 합니다 (sysprep.exe 실행). | 템플릿 프로 비전에는 특정 테 넌 트의 작업에 대 한 특수화 Vm이 포함 됩니다.| 

> [!NOTE]
> 이 단계에서는 템플릿 디스크를 VMM 라이브러리에 복사 하지 마십시오. 

### <a name="required-packages-to-create-a-nano-server-template-disk"></a>Nano Server 템플릿 디스크를 만드는 데 필요한 패키지

보호 된 Vm에서 게스트 OS로 Nano 서버를 실행 하려는 경우 Nano Server 이미지에 다음 패키지가 포함 되어 있는지 확인 해야 합니다.

- Microsoft-NanoServer-Guest-Package
- Microsoft-NanoServer-SecureStartup-Package

## <a name="run-windows-update-on-the-template-operating-system"></a>템플릿 운영 체제에서 Windows 업데이트 실행

템플릿 디스크에서 운영 체제에 최신 Windows 업데이트가 설치 되어 있는지 확인 합니다. 최근 릴리스된 업데이트는 템플릿 운영 체제가 최신 상태가 아닌 경우 완료 되지 못할 수 있는 프로세스 인 종단 간 보호 프로세스의 안정성을 향상 시킵니다.

## <a name="sign-and-protect-the-vhdx-with-the-template-disk-wizard"></a>템플릿 디스크 마법사를 사용 하 여 VHDX 서명 및 보호

보호 된 Vm에서 템플릿 디스크를 사용 하려면 디스크가 서명 되 고 BitLocker로 암호화 되어야 합니다. 이렇게 하려면 차폐 템플릿 디스크 만들기 마법사를 사용 합니다. 이 마법사는 디스크에 대 한 해시를 생성 하 여 VSC (볼륨 서명 카탈로그)에 추가 합니다. VSC는 지정 하는 인증서를 사용 하 여 서명 되 고, 프로 비전 프로세스 중에 테 넌 트에 대해 배포 되는 디스크가 변경 되지 않았는지 확인 하거나 테 넌 트가 신뢰 하지 않는 디스크로 대체 되도록 하는 데 사용 됩니다. 마지막으로 VM을 프로 비전 하는 동안 디스크의 암호화를 준비 하기 위해 BitLocker가 디스크의 운영 체제에 설치 됩니다 (아직 없는 경우).

> [!NOTE]
> 템플릿 디스크 마법사는 현재 위치의 지정 된 템플릿 디스크를 수정 합니다. 마법사를 실행 하 여 나중에 디스크를 업데이트할 때까지 보호 되지 않는 VHDX의 복사본을 만들 수 있습니다. 템플릿 디스크 마법사를 사용 하 여 보호 된 디스크는 수정할 수 없습니다.

Windows Server 2016를 실행 하는 컴퓨터에서 다음 단계를 수행 합니다 (보호 된 호스트나 VMM 서버가 될 필요는 없음).

1. [운영 체제 VHDX](#prepare-an-operating-system-vhdx) 를 서버에 준비 (아직 없는 경우) 하 여 만든 일반화 된 vhdx를 복사 합니다.

2. 컴퓨터의 **원격 서버 관리 도구** 에서 **보호 된 VM 도구** 기능을 설치 합니다.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart

3. 새 보호 된 Vm의 템플릿 디스크가 될 VHDX에 서명할 인증서를 가져오거나 만듭니다. 이 인증서에 대 한 세부 정보는 디스크를 신뢰할 수 있는 디스크로 권한 부여 하는 보호 데이터 파일에 통합 됩니다. 따라서 사용자 및 호스팅 서비스 공급자 트러스트의 인증 기관에서이 인증서를 가져오는 것이 중요 합니다. 호스터 및 테 넌 트 인 엔터프라이즈 시나리오에서는 PKI에서이 인증서를 발급 하는 것을 고려할 수 있습니다.

    테스트 환경을 설정 하 고 자체 서명 된 인증서를 사용 하 여 템플릿 디스크에 서명 하려는 경우 컴퓨터에서 다음과 같은 명령을 실행 합니다.

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. 시작 메뉴의 **관리 도구** 폴더에서 **템플릿 디스크 마법사** 를 시작 하거나 명령 프롬프트에 템플릿 **disk마법사나 .Exe** 를 입력 하 여 템플릿 디스크 마법사를 시작 합니다.

5. **인증서** 페이지에서 **찾아보기** 를 클릭 하 여 인증서 목록을 표시 합니다. 디스크 템플릿에 서명 하는 데 사용할 인증서를 선택 합니다. **확인**을 클릭하고 **다음**을 클릭합니다.

6. 가상 디스크 페이지에서 **찾아보기** 를 클릭 하 여 준비한 VHDX를 선택 하 고 **다음**을 클릭 합니다.

7. 서명 카탈로그 페이지에서 **디스크 이름** 및 버전을 제공 **합니다.** 이러한 필드는 서명 된 후 디스크를 식별 하는 데 도움이 됩니다.

    예를 들어 **디스크 이름** 에 대해 _WS2016_ 를 입력 하 고 **버전**, _1.0.0.0_ 을 입력할 수 있습니다.

8. 마법사의 설정 검토 페이지에서 선택 사항을 검토 합니다. **생성**을 클릭 하면 마법사가 템플릿 디스크에서 BitLocker를 사용 하도록 설정 하 고, 디스크의 해시를 계산 하 고, VHDX 메타 데이터에 저장 되는 볼륨 서명 카탈로그를 만듭니다.

    템플릿 디스크를 탑재 하거나 이동 하기 전에 서명 프로세스가 완료 될 때까지 기다립니다. 디스크 크기에 따라이 프로세스를 완료 하는 데 다소 시간이 걸릴 수 있습니다. 

9. **요약** 페이지에서 디스크 템플릿에 대 한 정보, 템플릿 서명에 사용 된 인증서 및 인증서 발급자가 표시 됩니다. **닫기**를 클릭하여 마법사를 종료합니다.


보호 된 [VM을 정의 하는 차폐 데이터 만들기](guarded-fabric-tenant-creates-shielding-data.md)에 설명 된 대로 사용자가 만드는 보호 데이터 파일과 함께 보호 된 디스크 템플릿을 호스팅 서비스 공급자에 제공 합니다.

## <a name="see-also"></a>참조

- [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
