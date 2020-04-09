---
title: 생성 및 게스트에서 Hyper-v 기능 호환성
description: 키 Hyper-v 기능과 호환 되는 세대 및 운영 체제를 나열 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 81c1f32d-7814-4992-8a66-dd4b77c939b4
author: kbdazure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: 7212cf21858c8031db0a72efa8d79d78974b0309
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853236"
---
# <a name="hyper-v-feature-compatibility-by-generation-and-guest"></a>생성 및 게스트에서 Hyper-v 기능 호환성

>적용 대상: Windows Server 2016
  
이 문서의 표에 세대 및 범주별으로 그룹화 하는 Hyper-v 기능 중 일부와 호환 되는 운영 체제를 보여 줍니다. 일반적으로 최상의 가용성의 최신 운영 체제를 실행 하는 2 세대 가상 컴퓨터 기능을 얻을 수 있습니다.  
  
일부 기능은 하드웨어 또는 기타 인프라를 사용 하는 점을 염두에 두십시오. 하드웨어 세부 정보는 [Windows Server 2016의 hyper-v에 대 한 시스템 요구 사항](System-requirements-for-Hyper-V-on-Windows.md)을 참조 하세요. 일부 경우에는 기능이 지원 되는 게스트 운영 체제에 사용할 수 있습니다. 운영 체제를 지원 세부 정보를 보려면  
  
* [지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  
* [지원되는 Windows 게스트 운영 체제](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)  
  
## <a name="availability-and-backup"></a>가용성 및 백업  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
검사점 | 1과 2 | 모든 지원 되는 게스트  
게스트 클러스터링 | 1과 2 | 게스트 클러스터 인식 애플리케이션을 실행 하 고 iSCSI 대상 소프트웨어를 설치 하는  
복제 | 1과 2 | 모든 지원 되는 게스트  
도메인 컨트롤러 | 1과 2 | 프로덕션 검사점만 사용 하는 모든 지원 되는 Windows Server 게스트입니다. [지원 되는 Windows Server 게스트 운영 체제](https://docs.microsoft.com/windows-server/virtualization/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows#supported-windows-server-guest-operating-systems) 를 참조 하세요.   
  
## <a name="compute"></a>계산  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
동적 메모리 | 1과 2 | 지원 되는 게스트의 특정 버전입니다. 참조 [Hyper-v 동적 메모리 개요](https://technet.microsoft.com/library/hh831766.aspx) Windows 10 및 Windows Server 2016 보다 오래 된 버전입니다.  
핫 추가/제거 메모리 | 1과 2 | Windows Server 2016의 경우 Windows 10  
가상 NUMA | 1과 2 | 모든 지원 되는 게스트  
  
## <a name="development-and-test"></a>개발 및 테스트  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
COM/직렬 포트 | 1과 2 <br>**참고:** 2 세대를 구성 하려면 Windows PowerShell을 사용 합니다. 자세한 내용은 [커널 디버깅을 위한 COM 포트 추가](./plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md#add-a-com-port-for-kernel-debugging)를 참조 하세요. | 모든 지원 되는 게스트  
  
## <a name="mobility"></a>이동성  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
실시간 마이그레이션  | 1과 2 |  모든 지원 되는 게스트  
Import/export(가져오기/내보내기) | 1과 2 |  모든 지원 되는 게스트  
  
## <a name="networking"></a>네트워킹  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
하거나 추가/제거할 가상 네트워크 어댑터의 | 2 | 모든 지원 되는 게스트  
기존 가상 네트워크 어댑터 | 1 | 모든 지원 되는 게스트  
단일 루트 입출력 가상화 (SR-IOV) | 1과 2 | 64 비트 Windows 게스트를 Windows 8 및 Windows Server 2012로 시작 합니다.  
가상 컴퓨터 다중 큐 (VMMQ) | 1과 2  | 모든 지원 되는 게스트  
  
## <a name="remote-connection-experience"></a>원격 연결 환경  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
개별 디바이스 할당 (DDA) | 1과 2 | Windows Server 2016, Windows Server 2012 R2 업데이트 3133690 에서만 설치, Windows 10 <br> **참고:** 3133690 업데이트에 대 한 세부 정보를 참조 하십시오. [이](https://support.microsoft.com/kb/3133690) 지원 문서입니다.  
고급 세션 모드 | 1과 2 | Windows Server 2016, Windows Server 2012 R2, Windows 10 및 Windows 8.1, 원격 데스크톱 서비스 사용 <br>**참고**: 호스트를 구성할 수도 할 수 있습니다. 자세한 내용은 다음을 참조 하십시오. [VMConnect 사용 하 여 Hyper-v 가상 컴퓨터에서 로컬 리소스 사용](./learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)합니다.  
RemoteFx | 1과 2 | 1 세대 Windows 8로 시작 하는 32 비트 및 64 비트 Windows 버전입니다. <br> 64 비트 Windows 10 버전에 2 세대  
  
## <a name="security"></a>보안  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
보안 부팅 | 2 | **Linux**: Ubuntu 14.04 이상, SUSE Linux Enterprise Server 12 및 이후, Red Hat Enterprise Linux 7.0 이상 및 CentOS 7.0 이상<br>**Windows**: 모든 지원 되는 2 세대 가상 컴퓨터에서 실행할 수 있는 버전  
실드 된 가상 컴퓨터 | 2 | **Windows**: 모든 지원 되는 2 세대 가상 컴퓨터에서 실행할 수 있는 버전  
  
## <a name="storage"></a>저장 공간  
  
기능  | 생성 | 게스트 운영 체제  
------------- | ------------- | -----------  
공유 가상 하드 디스크 (VHDX에만 해당) | 1과 2  | Windows Server 2016, Windows Server 2012 R2, Windows Server 2012  
SMB3 | 1과 2 | SMB3을 모두 지 원합니다  
직접 저장소 공간 | 2 | Windows Server 2016  
가상 파이버 채널 | 1과 2 | Windows Server 2016, Windows Server 2012 R2, Windows Server 2012  
VHDX 형식 | 1과 2 | 모든 지원 되는 게스트   
  
  
  
  
    


