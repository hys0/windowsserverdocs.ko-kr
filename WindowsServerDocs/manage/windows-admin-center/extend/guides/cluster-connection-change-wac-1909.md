---
title: Windows 관리 센터 v1909의 클러스터 연결 형식 변경 내용
description: Windows 관리 센터 v1909의 클러스터 연결 형식 변경 내용
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 10/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a07b30517f0d45b7e6f4f41f0ef9a6549e6e2117
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952774"
---
# <a name="cluster-connection-type-changes-in-windows-admin-center-v1909"></a>Windows 관리 센터 v1909의 클러스터 연결 형식 변경 내용

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!IMPORTANT]
> 이 문서에서는 장애 조치 (failover) 클러스터 및 하이퍼 수렴 형 클러스터 (HCI) 솔루션을 위해 Windows 관리 센터 도구를 개발 하는 Windows 관리 센터 확장 개발자에 게 필요한 변경 사항을 설명 합니다. 확장이 Windows 관리 센터 v1909 Preview 릴리스 및 향후 GA 릴리스와 호환 되는 데 필요한 필수 변경 내용입니다.

Windows 관리 센터 v1909에서는 두 개의 서로 다른 클러스터 연결 형식 (장애 조치 (failover) 클러스터 및 하이퍼 수렴 형 클러스터 연결)이 단일 클러스터 연결 형식으로 통합 되었습니다. 사용자는 클러스터를 추가 하는 데 사용할 연결 유형을 결정 하기 전에 더 이상 클러스터 구성을 식별할 필요가 없으며 다른 도구 집합에 대 한 액세스 권한을 얻기 위해 클러스터를 다른 연결 유형으로 두 번 추가할 필요가 없습니다. 이제 클러스터를 "Windows Server 클러스터"로 추가할 수 있으며, 스토리지 공간 다이렉트 사용 여부에 따라 적절 한 도구가 로드 됩니다.

이렇게 하려면 연결 유형 정의를 변경 해야 하 고 클러스터 관련 도구가 로드할 시기를 결정 해야 하므로 클러스터 (HCI 또는 HCI 클러스터 또는 둘 다)에 대 한 도구를 제공 하는 확장에는 설명 된 대로 구현이 변경 되어야 합니다. 표에서.

## <a name="manifestjson---solutionsids-and-connectiontypes"></a>매니페스트. json-솔루션 Sid 및 connectionTypes

이전에는 장애 조치 (failover) 클러스터 또는 HCI 클러스터 연결 형식에 대해 도구를 표시 하려면 ```manifest.json``` 파일에서 다음 정의 중 하나를 사용 해야 합니다.

장애 조치 (failover) 클러스터의 경우:
``` json
    {
        "entryPointType": "tool",
        "name": "MyToolName",
        "urlName": "MyToolUrl",
        "displayName": "MyToolDisplayName",
        "description": "MyToolDescription",
        "icon": "MyToolIcon",
        "path": "MyToolPath",
        "iframeId": "MyToolIframeId",
        "requirements": [
        {
            "solutionIds": [
                "msft.sme.failover-cluster!failover-cluster"
            ],
            "connectionTypes": [
                "msft.sme.connection-type.cluster"
            ]
        }
        ]
    }
```

HCI 클러스터의 경우 위의 강조 표시 된 섹션은 다음과 같이 대체 되었습니다.
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster"
        ]
    }
    ]
```

Windows 관리 센터 1909 이상에서는 두 개의 솔루션 Id 및 connectionTypes가 다음과 같이 대체 되었습니다.
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.cluster"
        ]
    }
    ]
```

이는 현재에서 지원 되는 유일한 클러스터 관련 솔루션 Id 및 connectionTypes 유형입니다. 도구가이 솔루션 Id 및 connectionTypes 유형 으로만 정의 된 경우 HCI 클러스터 인지 여부에 관계 없이 모든 장애 조치 (failover) 클러스터 연결에 대해 로드 됩니다. HCI 클러스터 또는 비 HCI 클러스터에 대해서만 도구를 사용할 수 있도록 제한 하려는 경우 다음 섹션에 설명 된 새 인벤토리 속성을 추가로 사용 해야 합니다.

## <a name="manifestjson--inventory-properties"></a>매니페스트. json – 인벤토리 속성
서버 또는 클러스터에 연결하는 경우 Windows 관리 센터에서 도구를 사용할 수 있는 시기를 결정하는 조건을 만드는 데 사용할 수 있는 인벤토리 속성 집합을 쿼리합니다 (도구를 사용하여 컨트롤의 "인벤토리 속성" 섹션 참조). [도구 표시 제어](dynamic-tool-display.md)추가 정보에 대한 표시 유형 문서입니다. Windows 관리 센터 v1909에서 클러스터가 하이퍼 수렴 형 클러스터 인지 여부를 확인 하는 데 사용할 수 있는 두 개의 새로운 속성을이 목록에 추가 했습니다. 

### <a name="iss2denabled"></a>isS2dEnabled
기술적으로 하이퍼 수렴 형 클러스터는 S2D (스토리지 공간 다이렉트)를 사용 하는 장애 조치 (failover) 클러스터로 정의 됩니다. 하이퍼 수렴 형 클러스터에 대해서만 도구를 사용할 수 있도록 하려면 (예: S2D를 사용 하는 경우) 다음 인벤토리 조건을 추가 합니다.
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.cluster"
        ],
        "conditions": [
        {
            "inventory": {
                "isS2dEnabled": {
                    "type": "boolean",
                    "operator": "is"
                }
            }
        }
        ]
    }
    ]
```
> [!TIP] 
> S2D를 사용 하도록 설정 하지 않은 경우에만 도구를 사용할 수 있게 하려면 "operator" 값을 "not"으로 변경 합니다.

### <a name="isbritannicaenabled"></a>isBritannicaEnabled
또한 SDDC 관리 클러스터 리소스에 종속 되어 있고 SDDC 개체 모델을 사용 하는 경우 다음 조건을 확인할 수 있습니다.
``` json
    "conditions": [
        {
            "inventory": {
                "isS2dEnabled": {
                    "type": "boolean",
                    "operator": "is"
                },
                "isBritannicaEnabled": {
                    "type": "boolean",
                    "operator": "is"
                }
            }
        }
    ]
```

## <a name="backward-compatibility-to-support-previous-versions-of-windows-admin-center"></a>이전 버전의 Windows 관리 센터를 지 원하는 이전 버전과의 호환성
확장이 v1904 GA 릴리스와 같은 이전 버전의 Windows 관리 센터에서 계속 작동 하도록 하기 위해 이전 솔루션 Id 및 connectionTypes 정의를 새 정의와 함께 사용할 수 있습니다. 모든 버전의 Windows 관리 센터에서 HCI 클러스터에 대 한 도구만 표시 하려면 아래 예제를 참조 하세요.
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster"
        ]
    },
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC",
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster",
            "msft.sme.connection-type.cluster"
        ],
        "conditions": [
            {
                "inventory": {
                    "isS2dEnabled": {
                        "type": "boolean",
                        "operator": "is"
                    }
                }
            }
        ]
    }
    ]
```

## <a name="known-issue-appcontextserviceactiveconnectionishyperconvergedclusterisfailovercluster-is-not-set-properly-in-windows-admin-center-v1909"></a>알려진 이슈: AppContextService. activeConnection. isHyperConvergedCluster/isFailoverCluster가 Windows 관리 센터 v1909에서 제대로 설정 되지 않았습니다.
최근 변경 내용의 재발은 ```AppContextService.activeConnection.isHyperConvergedCluster/isFailoverCluster``` 속성이 Windows 관리 센터 v1909에서 올바르게 설정 되지 않으며 항상 false가 된다는 것입니다. 이 문제는 다음 릴리스에서 v1910 수정 될 예정 이지만, 더 이상 사용 되지 않으며 2020의 GA 릴리스에서 더 이상 사용할 수 없습니다. 나중에이 코드를 아래 코드로 바꾸고 ```this.connectHCI```을 사용할 수 있습니다.
```
    import { ClusterInventoryCache } from '@msft-sme/core';

    constructor(
        ...
        private appContextService: AppContextService,
        ...
    ) {
        ...
        this.clusterInventoryCache = new ClusterInventoryCache(
            this.appContextService,
            <SharedCacheOptions>{ expiration: Constants.sharedCacheExpiration }
        );

         this.isBritannicEnabled().subscribe(result => this.connectHCI = result);
    }

    private isBritannicEnabled(): Observable<boolean> {
        return this.clusterInventoryCache.query(this.getClusterInventoryQueryParameters())
        .pipe(
            map(inventory => {
                return inventory.instance.isBritannicaEnabled;
        }));
    }

    private getClusterInventoryQueryParameters(): ClusterInventoryParams {
        const nodeName = this.appContextService.activeConnection.validNodeName;
        const endpoint = this.appContextService.authorizationManager.getJeaEndpoint(nodeName);
        const options = { powerShellEndpoint: endpoint };
        return {
            name: nodeName,
            requestOptions: options
        };
    }
```