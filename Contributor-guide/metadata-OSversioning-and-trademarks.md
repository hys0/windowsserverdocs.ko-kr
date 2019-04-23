# <a name="metadata-and-version-identifiers"></a>메타 데이터 및 버전 식별자

상표, 버전 관리 및 windowsserverdocs pr 리포지토리에서 문서에 대 한 메타 데이터에 대해 알아야 할 내용 같습니다. 문서 작성자는 해당 아티클이 이러한 표준 및 요구 사항을 확인 하는 일을 담당 합니다.

## <a name="trademarks"></a>상표
기술 라이브러리의 문서에서 제품 참조 한 후 상표 기호를 사용 하지 마세요. Technet.microsoft.com, docs.microsoft.com, 및 기타 공식 Microsoft 채널에 게시 하기 때문에 불필요 한 [상표](https://www.microsoft.com/trademarks) Microsoft 상표 목록을 바닥글 링크. 해당 링크는 법적 요건을 충족 합니다. 백그라운드에서 지침을 참조 하세요. [CELA](https://microsoft.sharepoint.com/sites/LCAWeb/Home/Copyrights-Trademarks-and-Patents/Trademarks/Trademark-List-and-Usage), 아래 "웹 사이트"와 Microsoft 쓰기 스타일 가이드 [저작권 및 상표](https://worldready.cloudapp.net/Styleguide/Read?id=2700&topicid=26696) "웹 페이지에서 Microsoft.com" 페이지 

## <a name="versioning"></a>버전 관리
이 리포지토리에서 문서를 여러 종류의 버전 관리에 적용 됩니다. 

-  문서에 적용 되는 제품 버전을 나타내는 버전 관리에는 두 가지 방법으로 수행 됩니다.
    - 게시 된 문서에 텍스트로 표시 되므로 문서의 단일선에서 수동으로입니다.
    - 메타 데이터에서 아래 설명합니다.
-  원본 콘텐츠 버전 관리 파일에 대 한 Github의 기록을 통해 처리 됩니다. 

## <a name="metadata-structure-and-format"></a>메타 데이터 구조 및 형식

- 위의 H1 제목 파일의 맨 위에 있는 메타 데이터를 배치 합니다.
- 블록의 첫 번째 및 마지막 줄에 3 개의 대시를 사용 하 여 파일 내용의 나머지 부분에서 블록을 구분 합니다. 해당 줄에 다른 텍스트를 넣지 마세요.
- 별도 줄에 각 메타 데이터 이름/값 쌍을 배치 합니다.
- 메타 데이터에 미리 정의 된 값이 필요 또는 사용자 지정 값을 허용 하는지 여부에 따라 다음 구문 패턴 중 하나를 사용 합니다. 

        ---
        name1: predefined-value
        name2: "my custom value"
        ---

## <a name="metadata-names-and-values"></a>메타 데이터 이름 및 값

특정 메타 데이터는 다른 메타 데이터는 것이 좋지만 반드시 동안 TechNet 기술 라이브러리의 아티클로 게시 된 모든 파일이 필요 합니다. 경우에 따라 특정 값만 메타 데이터의 특정 부분에 대 한 허용 됩니다. 

|이름|값|
|---|---|
|title|H1 제목을 일치 하는 사용자 지정 값입니다. 브라우저 탭에 표시를 확인 합니다.|
|description|검색 결과에 표시 되 고 SEO에 영향을 줍니다. 적절 한 키워드를 포함 하지만 길이 보다 작거나 160 자 합니다.|
|작성자|기본 문서 작성자의 Github 별칭|
|ms.author|문서에서 다루는 기술 영역을 담당 하는 문서 작성자 또는 콘텐츠 개발자의 MSFT 별칭입니다.|
|ms.date|마지막으로 콘텐츠 업데이트의 날짜입니다. 메타 데이터에만 변경 내용을 업데이트 하지 마십시오. Mm/dd/yyyy 형식의 사용 합니다.|
|ms.prod|BI 보고를 기반으로 미리 정의 된 Windows Server 버전을 식별 [값](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default&IsList=1&ListId=%7b46B17C8A-CD7E-47ED-A1B6-F2B654B55E2B%7d&ListItemId=969)합니다.|
|ms.technology|BI 보고를 기반으로 미리 정의 된 기술 영역을 식별 [값](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default&IsList=1&ListId=%7b46B17C8A-CD7E-47ED-A1B6-F2B654B55E2B%7d&ListItemId=969)|
|ms.asset|BI 보고에 대 한 모든 로캘에서에서 문서를 식별 하는 GUID입니다. 아티클 이전 작성에서 마이그레이션된 시스템은 이러한 지원을 제공 합니다. Github에서 작성 한 문서와 같은 도구를 사용 합니다 [ https://guidgenerator.com/ ](https://guidgenerator.com/)합니다.| 

## <a name="troubleshooting"></a>문제 해결

게시 된 문서 위쪽에 표시 되는 메타 데이터에는 소스 파일에 형식 오류가 있을 때 발생 합니다. 몇 가지 일반적인 오류 다음과 같습니다.

- 블록 또는 잘못 된 개수의 하이픈을 첫 번째 및 마지막 줄에서 삼중 하이픈 없습니다.
- 메타 데이터에는 필수 구문을 따르지 않습니다: \<이름을\>:\<공간 single\>\<값 >

업데이트 된 파일을 게시할 PR 제출 파일에이 함수 및 다른 명확한 오류를 확인 합니다. 문제가 있으면, 전자 메일 PR 검토자 별칭: wssc-pra@microsoft.com

## <a name="see-also"></a>참조
International 콘텐츠 서비스에서 사용 되는 메타 데이터를 기반으로 하는 메타 데이터에서이 리포지토리 사용 \(CSI\)합니다. 선택적 메타 데이터를 비롯 한 자세한 내용은에서 제공 됩니다 [ http://aka.ms/skyeye/meta ](http://aka.ms/skyeye/meta)합니다.
Business intelligence 리소스 참조 CSI BI 팀의 [wiki](https://microsoft.sharepoint.com/teams/STBCSI/Insights/Selfserve%20BI%20wiki/Self-serve%20BI%20wiki.aspx)합니다.