---
title: Azure 스택 HCI 개요
description: '필요에 따라 클라우드 기반 백업, 사이트 복구 등에 대 한 Azure 서비스에 연결을 사용 하는 Windows Server 2019 하이퍼 수렴 형 클러스터 가상화 된 워크 로드 온-프레미스를 실행 하는 하드웨어 유효성 검사 azure 스택 HCI에서입니다. Azure 스택 HCI 솔루션 Microsoft 검증 하드웨어를 사용 하 여 최적의 성능과 안정성 및 NVMe 드라이브, 영구 메모리 및 원격 직접 메모리 액세스 (RDMA) 네트워킹 등의 기술에 대 한 지원을 포함 합니다.'
ms.technology: storage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/26/2019
---

# Azure 스택 HCI 개요

>적용 대상: Windows Server 2019

필요에 따라 클라우드 기반 백업, 사이트 복구 등에 대 한 Azure 서비스에 연결을 사용 하는 Windows Server 2019 하이퍼 수렴 형 클러스터 가상화 된 워크 로드 온-프레미스를 실행 하는 하드웨어 유효성 검사 azure 스택 HCI에서입니다. Azure 스택 HCI 솔루션 Microsoft 검증 하드웨어를 사용 하 여 최적의 성능과 안정성 및 NVMe 드라이브, 영구 메모리 및 원격 직접 메모리 액세스 (RDMA) 네트워킹 등의 기술에 대 한 지원을 포함 합니다.

## Azure Stack 제품군

Azure 스택 HCI Azure의 일부 이며 동일한 소프트웨어 정의 사용 하 여 Azure Stack 제품군 컴퓨팅, 저장소 및 네트워킹 Azure Stack 소프트웨어. 다음은 서로 다른 솔루션의 빠른 요약이입니다.

- [Azure](https://azure.microsoft.com) -공용 클라우드 서비스 사용
- [Azure Stack](https://azure.microsoft.com/overview/azure-stack) -작동 클라우드 서비스 온-프레미스
- [Azure 스택 HCI](https://azure.microsoft.com/overview/azure-stack/hci) -실행 앱 온-프레미스, Azure에 대 한 선택적 연결을 사용 하 여 가상화

![가상화 된 응용 프로그램 온-프레미스 azure 및 Azure 스택 HCI 실행 되는 동안 클라우드 서비스를 실행 하는 Azure 스택](media/azure-and-azure-stack-family.png)

자세한 내용을 보려면:

- 2019 년 3 월 28에 [하이브리드 클라우드 가상 이벤트](https://info.microsoft.com/ww-landing-building-a-successful-hybrid-cloud-strategy.html) 를 등록 합니다.
- [Azure 스택 HCI](https://azure.microsoft.com/overview/azure-stack/hci) 솔루션 웹 사이트에서 자세한 내용을 합니다.
- 시청 Microsoft 전문가 Jeff Woolsey와 Vijay Tewari [새로운 Azure 스택 HCI 솔루션에 설명](https://aka.ms/AzureStackOverviewVideo)합니다.

## 하드웨어 파트너

15 파트너 로부터 Windows Server 2019를 실행 하는 유효한 Azure 스택 HCI 솔루션을 구입할 수 있습니다. 기본 Microsoft 파트너 긴 디자인 및 빌드 시간 없이 작동 가져오고 구현 및 지원 서비스에 대 한 연락처의 있는 단일 액세스 지점을 제공 합니다.

70 + Azure 스택 HCI 솔루션 이러한 Microsoft 파트너에서 현재 사용 가능한 보려면 [Azure 스택 HCI 웹 사이트](https://azure.microsoft.com/overview/azure-stack/hci) 를 방문: ASUS, Axellio, bluechip DataON, Dell EMC, Fujitsu, 패키지는 HPE, Hitachi, Huawei, Lenovo, NEC, primeLine 솔루션, QCT, SecureGUARD 및 Supermicro 합니다.

## FAQ

### 어떤 Azure Stack 및 Azure 스택 HCI 솔루션 않았을 공통? 
Azure 스택 HCI 솔루션으로 Azure Stack 동일한 Hyper-v 기반 소프트웨어 정의 컴퓨팅, 저장소 및 네트워킹 기술을 기능. 두 제품에 대 한 안정성 및 기본 하드웨어 플랫폼과의 호환성을 보장 하는 엄격한 테스트 및 유효성 검사 조건을 충족 해야 합니다.

### 어떻게 다른 란?
Azure Stack 서비스 온-프레미스 클라우드 실행할 수 있습니다. Azure IaaS를 실행할 수 및 PaaS 서비스 온-프레미스를 일관 되 게 빌드 및 클라우드 응용 프로그램 어디서 나 Azure 포털에서 온-프레미스 관리를 실행 합니다.

Azure 스택 HCI 가상화 된 워크 로드 온-프레미스, 실행할 수 있는 도구에 따라 Windows Admin Center 및 친숙 한 Windows Server 관리. 필요에 따라 클라우드 기반 사이트 복구, 모니터링, 등과 같은 하이브리드 시나리오에 대 한 Azure에 연결할 수 있습니다.

### Microsoft은 Azure Stack 제품군에 제공 하는 HCI을 창출 하는 이유는? 
Microsoft의 하이퍼 수렴 형 호스트용 기술을 이미 Azure Stack의 기초입니다. 

많은 Microsoft 고객이 복잡 한 IT 환경 있고 오른쪽 비즈니스에 가장 적합 한 기술을 사용 하 여는 것을 만족 하는 솔루션을 제공 하려면이 목표입니다. Azure 스택 HCI 하드웨어 파트너가에서 이전에 사용할 수 있는 Windows Server 2016 기반 windows server 소프트웨어 정의 (WSSD) 솔루션의 발전 된 형태입니다. 우리 것에 가져올 Azure Stack 패밀리 인프라 관리 서비스에 대 한 Azure와 원활 하 게 연결할 새 옵션을 제공 하려면 시작 했습니다. 

### Azure 스택 HCI에서 Azure Stack 업그레이드 할 수 있나요? 
아니요, 고객이 Azure 스택 또는 Azure에서 Azure 스택 HCI의 워크 로드에 마이그레이션할 수 있지만 합니다.

### Azure 스택 HCI에 연결할 수 있는 Azure 서비스

Azure 스택 HCI에 연결할 수 있는 Azure 서비스의 업데이트 된 목록을 [Azure 하이브리드 서비스에 Windows Server 연결](../azure-hybrid-services/index.md)을 참조 하세요.

### Azure 스택 HCI 솔루션을 구입 하는 어떻게 하나요?
다음 단계를 따르세요.

1. 기본 하드웨어 파트너에서는 Microsoft 검증 하드웨어 시스템을 구입 합니다.
1. Windows Server 2019 Datacenter 버전 및 관리 및 클라우드 서비스에 대 한 Azure에 연결 하는 기능에 대 한 Windows Admin Center 설치
1. 필요에 따라 Azure 계정에 사용 하 여 작업을 클라우드 기반 관리 및 보안 서비스 연결.