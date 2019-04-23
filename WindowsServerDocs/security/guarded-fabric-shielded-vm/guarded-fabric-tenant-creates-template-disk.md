---
title: 테 넌 트-템플릿 디스크-선택 사항 만들기에 대 한 보호 된 Vm
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: c1992f8b-6f88-4dbc-b4a5-08368bba2787
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2709c84a16dadc2211af4a6f5b43c13266ede155
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874634"
---
# <a name="shielded-vms-for-tenants---creating-a-template-disk-optional"></a>테 넌 트-(선택 사항) 템플릿 디스크를 만들기에 대 한 보호 된 Vm

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

새 보호 된 VM을 만들려면 특별히 준비, 서명 된 템플릿 디스크를 사용 해야 합니다. 메타 데이터 서명 된 템플릿 디스크에서 디스크를 만든 후 수정 되지 않습니다 보장 및 보호 된 Vm을 만들 디스크를 제한 하는 테 넌 트를 사용할 수 있습니다. 이 디스크를 제공 하는 한 가지 방법은이 항목에 설명 된 대로 만들려면 테 넌 트 사용자입니다. 

> [!IMPORTANT]
> 원하는 경우 호스팅 서비스 공급자가 제공 된 템플릿 디스크 대신 사용할 수 있습니다. 이 작업을 수행 하는 경우 테스트 VM (바이러스 백신, 취약점 스캐너 및 등)에 사용자 고유의 도구를 실행 하 고 해당 템플릿 디스크를 사용 하 여 디스크의 유효성을 검사 하는 실제로 신뢰할 수 있는 상태를 배포 하려면 반드시 합니다.

## <a name="prepare-an-operating-system-vhdx"></a>운영 체제 VHDX를 준비 합니다.

보호 된 템플릿 디스크를 만들려면 먼저 템플릿 디스크 마법사를 통해 실행 되는 OS 디스크를 준비 해야 합니다. 이 디스크를 OS 디스크로 보호 된 Vm에서 사용 됩니다. 이 디스크와 같은 Microsoft 데스크톱 이미지 서비스 관리자 (DISM)을 만들고 또는 수동으로 빈 VHDX 사용 하 여 VM을 설정 하 고 해당 디스크에 OS 설치에 모든 기존 도구를 사용할 수 있습니다. 디스크를 설정할 때 2 세대에 따라 다릅니다 및/또는 보호 된 Vm는 다음 요구 사항을 준수 해야 합니다. 

| VHDX에 대 한 요구 사항 | 이유 |
|-----------|----|
|GUID 파티션 테이블 (GPT) 디스크 여야 합니다. | UEFI를 지 원하는 2 세대 가상 컴퓨터에 필요한|
|디스크 유형 이어야 합니다 **기본적인** 반대인 **동적**합니다. <br>참고: 이 "동적 확장" VHDX 기능이 아니라 Hyper-v에서 지 원하는 논리 디스크 형식을 가리킵니다. | BitLocker는 동적 디스크를 지원 하지 않습니다.|
|디스크에 두 개 이상의 파티션이 있습니다. 한 파티션에 Windows가 설치 된 드라이브를 포함 해야 합니다. 이 드라이브가 BitLocker 암호화 됩니다. 다른 파티션은 활성 파티션입니다, 부팅 로더를 포함 하 고 컴퓨터를 시작할 수 있도록 암호화 되지 않은 상태로 유지 됩니다.|BitLocker에 필요한|
|파일 시스템이 NTFS가 | BitLocker에 필요한|
|VHDX에 설치 된 운영 체제에는 다음 중 하나입니다.<br>-2019 Windows Server, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 <br>- Windows 10, Windows 8.1, Windows 8| 2 세대 가상 컴퓨터 및 Microsoft 보안 부팅 템플릿을 지원 해야 합니다.|
|운영 체제에 일반화 된 (sysprep.exe 실행된) 해야 합니다. | 전문적으로 다루는 포함 템플릿을 프로 비전 특정 테 넌 트의 워크 로드에 대 한 Vm| 

> [!NOTE]
> 이 단계에서 VMM 라이브러리에 템플릿 디스크를 복사 하지 않습니다. 

### <a name="required-packages-to-create-a-nano-server-template-disk"></a>필수 패키지를 Nano Server 템플릿 디스크를 만들려면

게스트 OS 보호 된 vm에서으로 Nano Server를 실행 하려는 경우 Nano Server 이미지에는 다음 패키지가 포함 되어 있습니다. 확인 해야 합니다.

- Microsoft-NanoServer-Guest-Package
- Microsoft-NanoServer-SecureStartup-Package

## <a name="run-windows-update-on-the-template-operating-system"></a>템플릿 운영 체제에서 Windows Update를 실행 합니다.

템플릿 디스크에서 운영 체제에 모든 최신 Windows 업데이트가 설치 되어 있는지를 확인 합니다. 최근에 출시 된 업데이트는 종단 간 보호 프로세스의 안정성 향상-프로세스 템플릿 운영 체제가 완료가 실패할 수 있는 최신 상태가 아닙니다.

## <a name="sign-and-protect-the-vhdx-with-the-template-disk-wizard"></a>로그인 하 고 템플릿 디스크 마법사를 사용 하 여 VHDX를 보호 합니다.

보호 된 Vm에서 템플릿 디스크를 사용 하려면에 디스크를 서명 하 고 BitLocker로 암호화 된 수 해야 합니다. 이렇게 하려면 보호 된 템플릿 디스크 만들기 마법사를 사용 합니다. 이 마법사는 디스크에 대 한 해시를 생성 하 고 볼륨 서명 카탈로그 (VSC)에 추가 합니다. VSC는 지정 하 고 테 넌 트에 대 한 배포 되는 디스크 없습니다 변경 하거나 테 넌 트를 신뢰할 수 없는 디스크를 사용 하 여 대체 되도록 프로 비전 프로세스 중에 사용 되는 인증서를 사용 하 여 서명 됩니다. 마지막으로 BitLocker에 설치 됩니다 디스크의 운영 체제 (이 아직 없는) 하는 경우 VM 프로 비전 중에 암호화에 대 한 디스크를 준비 하기.

> [!NOTE]
> 템플릿 디스크 마법사는 현재 위치를 지정 된 템플릿 디스크를 수정 합니다. 나중에 디스크를 업데이트 하려면 마법사를 실행 하기 전에 보호 되지 않는 VHDX의 복사본을 확인 하려는 경우. 템플릿 디스크 마법사를 사용 하 여 보호 된 디스크를 수정할 수 없습니다.

(보호 된 호스트 또는 VMM 서버가 필요 하지 않습니다)는 Windows Server 2016을 실행 하는 컴퓨터에서 다음 단계를 수행 합니다.

1. 만든 일반화 된 VHDX를 복사 [운영 체제 VHDX를 준비](#prepare-an-operating-system-vhdx) 서버에 아직 없는 경우.

2. 설치를 **보호 된 VM 도구** 에서 기능 **원격 서버 관리 도구** 컴퓨터에 있습니다.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart

3. 구하거 나 새 보호 된 Vm에 대 한 템플릿 디스크에 VHDX를 서명 인증서를 만듭니다. 이 인증서에 대 한 세부 정보를 신뢰할 수 있는 디스크를 디스크로 권한을 부여 하는 보호 데이터 파일에 통합 됩니다. 따라서 하 고 호스팅 서비스 공급자 트러스트는 인증 기관에서이 인증서를 사용 하는 것입니다. 호스팅 서비스 공급자 및 테 넌 트 둘 다 있는 엔터프라이즈 시나리오에서이 인증서를 발급 하 여 PKI에서 고려할 수 있습니다.

    테스트 환경을 설정 하는 자체 서명 된 인증서를 사용 하 여 템플릿 디스크 서명 하려는 경우 컴퓨터에 다음과 비슷한 명령을 실행 합니다.

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. 시작 합니다 **템플릿 디스크 마법사** 에서 합니다 **관리 도구** 폴더를 입력 하 여 또는 시작 메뉴에서 **TemplateDiskWizard.exe** 명령 프롬프트에.

5. 에 **인증서** 페이지에서 **찾아보기** 인증서의 목록을 표시 합니다. 디스크 템플릿을 서명 된 인증서를 선택 합니다. **확인**을 클릭하고 **다음**을 클릭합니다.

6. 가상 디스크 페이지에서 클릭 **찾아보기** 준비한 VHDX를 선택 하려면 클릭 **다음**합니다.

7. 서명 카탈로그 페이지의 친숙 한 제공할 **디스크 이름** 및 **버전입니다.** 이러한 필드는 서명 된 후 디스크를 식별 하는 데 도움이 되기 위해 존재 합니다.

    예를 들어 **디스크 이름** 입력할 수 있습니다 _WS2016_ 한 **버전**, _1.0.0.0_

8. 마법사의 설정 검토 페이지에서 선택 내용을 검토 합니다. 클릭 하면 **생성**, 마법사는 템플릿 디스크에서 BitLocker를 활성화, 디스크의 해시를 계산 및 VHDX 메타 데이터에 저장 된 볼륨 서명 카탈로그를 만듭니다.

    서명 프로세스를 탑재 하거나 템플릿 디스크를 이동 하기 전에 완료 될 때까지 기다립니다. 이 프로세스는 디스크의 크기에 따라 완료 하는 데 걸릴 수 있습니다. 

9. 에 **요약** 페이지를 디스크 템플릿 서식 파일을 서명 하는 데 사용 하는 인증서에 대 한 정보 및 인증서 발급자가 표시 됩니다. **닫기**를 클릭하여 마법사를 종료합니다.


에 설명 된 대로 보호 된 디스크 템플릿을 직접 작성 하는 보호 데이터 파일을 함께 호스팅 서비스 공급자에 게 제공 [보호 된 VM을 정의 하는 데이터 보호 만들기](guarded-fabric-tenant-creates-shielding-data.md)합니다.

## <a name="see-also"></a>참조

- [보호 된 Vm 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호 된 패브릭 및 보호 된 Vm](guarded-fabric-and-shielded-vms-top-node.md)
