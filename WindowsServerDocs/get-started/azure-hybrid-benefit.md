---
title: Windows Server의 Azure 하이브리드 혜택
description: 온-프레미스 Windows Server 라이선스를 사용하여 Azure VM에 저장
ms.prod: windows-server
ms.date: 11/10/2017
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.openlocfilehash: 62821abc6c9eec660fa6af832bb1aba151708021
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63686422"
---
# <a name="azure-hybrid-benefit-for-windows-server"></a>Windows Server의 Azure 하이브리드 혜택

>적용 대상: Windows Server

## <a name="benefit-description-rules-and-use-cases"></a>혜택 설명, 규칙 및 사용 사례

Windows Server에 대한 Azure 하이브리드 혜택은 온-프레미스 Windows Server 라이선스와 Software Assurance를 함께 사용하여 Azure에서 Windows Server VM에 최대 40%까지 저장이 가능하도록 합니다.  이 경우 Windows Server에 대한 라이선스에 Software Assurance 혜택이 적용되기 때문에 고객은 VM의 인프라 비용만 지불하면 됩니다.  이 혜택은 2008R2, 2012, 2012R2 및 2016 릴리스에서 Standard 및 Datacenter 버전의 Windows Server에 모두 적용할 수 있습니다.  이 혜택은 모든 지역 및 소버린 클라우드에서 사용할 수 있습니다.


![이미지 1](media/ahb01.png)

Windows Server 라이선스에서 Software Assurance나 EAS, SCE 구독, Open Value 구독 같은 구독 라이선스가 활성 상태이기만 하면 이 혜택을 이용할 수 있는 자격 요건이 됩니다.  

SA/구독이 활성 상태인 Windows Server 2-프로세서 라이선스와 SA/구독이 포함된 16개의 Windows Server 코어 라이선스 세트 각각은 2개 이하의 Azure Base Instance(VM)에 할당된 최대 16개의 가상 코어에서 Microsoft Azure 기반의 Windows Server를 사용할 수 있도록 고객에게 자격을 부여합니다. SA/구독이 포함된 8개의 추가 코어 라이선스 세트 각각은 최대 8개의 가상 코어와 1개의 Base Instance(VM)에서 사용 자격을 부여합니다.

| SA/구독이 포함된 라이선스            | VM 및 코어에 대한 사용 자격 부여            | 사용 방법                                |
|-----------------------------------------|----------------------------------|-----------------------------------------------------|
| WS 데이터 센터(16개 코어 또는 2-프로세서 라이선스)  | 최대 2개의 VM과 최대 16개의 코어 지원 | 온-프레미스와 Azure 환경 모두에서 가상 머신 실행  |
| WS Standard(16개 코어 또는 2-프로세서 라이선스)    | 최대 2개의 VM과 최대 16개의 코어 지원 | 온-프레미스 또는 Azure 환경에서 가상 머신 실행 |

Azure 하이브리드 혜택을 활용하는 VM은 SA/구독 기간 동안에만 Azure에서 실행이 가능합니다. SA/구독 만료 시간이 가까워지면 고객은 선택에 따라 SA/구독을 갱신하거나, VM에 대한 하이브리드 혜택 기능을 해제하거나, 하이브리드 혜택을 사용하여 VM 프로비전을 해제할 수 있습니다. 

### <a name="savings-examples"></a>절약 효과 예제 

![이미지 2](media/ahb02.png)
 
아래에서 혜택 규칙을 보다 세부적으로 이해하는 데 도움이 되는 참조 테이블을 찾을 수 있습니다. 녹색 열은 동일한 형식의 VM 수량을 표시하고, 파란색 행은 각 VM의 핵심 밀도를 표시합니다. 노란색 셀은 특정한 코어 밀도를 가진 특정 수의 VM을 반드시 배포해야 하는 2-프로세서 라이선스(또는 16개 코어 라이선스 세트)의 수를 표시합니다. 

SA 요구 사항이 포함된 Windows Server 참조 테이블:

![이미지 3](media/ahb03.png)
 
또한 Windows Server에 대한 Azure 하이브리드 혜택은 서로 다른 유형의 VM을 결합하는 것은 물론이고, 필요에 따라 구성을 실행할 수 있는 유연성을 제공합니다.

몇몇 라이선스 옵션에 대한 구성 예제:

![이미지 4](media/ahb04.png)
![이미지 5](media/ahb05.png)

 
Windows Server에 대한 Azure 하이브리드 혜택에 대한 자세한 내용은 Azure 하이브리드 혜택 웹사이트를 참조하세요.

## <a name="how-to-maintain-compliance"></a>호환성을 유지하는 방법

Windows Server VM에 Azure 하이브리드 혜택을 적용하고 싶은 고객들은 이 혜택을 정품 인증하기 앞서 자격이 있는 라이선스의 수와 SA/구독의 적용 범위를 확인하고 위의 지침에 따라 혜택과 함께 올바른 수의 VM을 배포해야 합니다. 실행 중인 VM에 이미 Azure 하이브리드 혜택이 적용되고 있는 경우에는 실행 중인 디바이스의 수에 대해 인벤토리를 수행하고 현재 활성 상태인 SA 라이선스와 비교해 확인해야 합니다.  SA 라이선스 위치의 유효성을 검사하려면 Microsoft Enterprise 계약 라이선스 전문가에게 문의하세요.
Windows Server에 대한 Azure 하이브리드 혜택 구독을 통해 배포된 모든 VM을 확인하고 계산하려면 다음 중 하나를 수행하세요.

1. Windows Server에 대한 Azure 하이브리드 혜택 사용량을 표시하도록 Microsoft Azure Portal을 구성합니다. Microsoft Azure Portal의 VM 섹션으로 가서 목록 보기에 "Azure 하이브리드 혜택" 열을 추가합니다. 

    ![이미지 6](media/ahb06.png)

2.  PowerShell을 사용하여 Windows Server에 대한 Azure 하이브리드 혜택 사용량 표시

    ```
    $vms = Get-AzureRMVM 
    foreach ($vm in $vms) {"VM Name: " + $vm.Name, "   Azure Hybrid Benefit for Windows Server: "+ $vm.LicenseType}
    ```

3.  Windows Server에 대한 Azure 하이브리드 혜택이 적용되고 있는 VM의 수를 확인하려면 Microsoft Azure 청구서를 확인하세요. 혜택이 적용 중인 인스턴스의 수에 대한 정보는 ‘추가 정보’에 표시됩니다.

    ```
    "{"ImageType":"WindowsServerBYOL","ServiceType":"Standard_A1","VMName":"","UsageType":"ComputeHR"}" 
    ```

실시간으로 청구가 이루어지지 않는다는 점에 유의하세요. 즉, 하이브리드 혜택이 적용되는 VM을 정품 인증한 시점으로부터 몇 시간 후에 청구서에 표시가 됩니다.
아래의 **Windows Server에 대한 Azure 하이브리드 혜택 SA 카운팅 도구**에 나온 결과를 적용하여 필요한 SA 또는 구독이 적용되는 WS 라이선스의 수를 알아낼 수 있습니다.

라이선스 위치에 대한 포괄적인 보기를 생성하려면 소유하고 있는 각 구독마다 인벤토리를 수행해야 합니다.

[Azure 하이브리드 혜택 WS SA 개수 도구](http://download.microsoft.com/download/7/1/2/712FEFF0-155C-4ABF-96C0-CE4EC4DB0516/Azure_Hybrid_Benefit_Windows_Server_SA_Count_Tool.xlsx)

위와 같이 인벤토리를 수행하고 실행 중인 Azure 하이브리드 혜택 인스턴스의 수에 대해 완전히 사용 허가를 받았음을 확인한 경우에는 더 이상의 추가 조치가 필요하지 않습니다. VM 수를 늘려가며 이 혜택을 적용할 수 있음을 확인했다면 전체 비용을 지불하기 보다 혜택이 적용 중인 인스턴스로 전환하여 추가적으로 비용을 최적화하고 싶을 수 있습니다.

이미 배포된 VM 수에 비해 적격 Windows Server 라이선스의 수가 충분하지 않은 경우에는 아래 나열된 채널 중 하나를 통해 Software Assurance가 적용되는 Windows Server 온-프레미스 라이선스를 추가로 구입하거나, 정기적 시간당 요금제로 Windows Server VM을 구입하거나, 일부 VM에 대해 하이브리드 혜택 기능을 해제해야 합니다. 8개씩 코어의 수가 증가하는 코어 라이선스를 구입하면 추가 VM에서 Azure 하이브리드 혜택을 적용 받을 수 있습니다. 

Windows Server Software Assurance 및 구독은 다음과 같은 Microsoft 라이선스 채널 조합 중 하나를 통해 구입이 가능합니다.

| 채널                      | 열기     | OVS      | 선택/추가 선택  | MPSA       | EA/EAS   |
|------------------------------|----------|----------|-----------------------|-----------|----------|
| 일반적인 크기(디바이스 수)  | 5-250    | 5-250    | >250                  | >250      | >500     |
| SA/구독            | 선택 사항 | 포함 | 선택 사항              | 선택 사항  | 포함 |

Microsoft는 Azure 하이브리드 혜택 사용량의 적격 여부를 확인하기 위해 언제든 최종 고객을 감사할 수 있는 권리가 있습니다. 

## <a name="deployment-guidance"></a>배포 지침 

구입 채널에 관계 없이 적격 라이선스를 보유하고 있는 고객이면 누구나 미리 작성된 갤러리 이미지를 사용할 수 있도록 허용하는 것은 물론이고, 파트너가 고객을 대신하여 배포를 수행할 수 있도록 허용하고 있습니다. 

다음을 포함하여 사용 가능한 모든 배포 옵션에 대한 지침은 [여기](https://azure.microsoft.com/pricing/hybrid-use-benefit/)에서 확인하세요. 
-   미리 작성된 갤러리 이미지를 활용한 새로운 배포 서비스를 집중 소개하는 상세 동영상
-   사용자 지정 VM을 업로드하는 방법에 대한 상세 지침 
-   PowerShell을 사용한 Azure 사이트 복구를 통해 기존 VM을 마이그레이션하는 방법에 대한 상세 지침 
