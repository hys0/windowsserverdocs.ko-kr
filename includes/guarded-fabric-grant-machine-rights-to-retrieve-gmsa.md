1. 모든 HGS gMSA 계정을 사용 하 여 해당 서버에 허용 되는 HGS 서버를 포함 하는 보안 그룹에 새 노드에 대 한 컴퓨터 계정을 추가 하는 디렉터리 서비스 관리자를 있습니다.

2. 해당 보안 그룹에 컴퓨터의 멤버 자격을 포함 하는 새 Kerberos 티켓을 가져올 새 노드를 다시 부팅 합니다. 다시 부팅이 완료 되 면 컴퓨터의 로컬 관리자 그룹에 속하는 도메인 id로 로그인 합니다.

3. 노드에 HGS 그룹 관리 서비스 계정을 설치 합니다.

   ```powershell
   Install-ADServiceAccount -Identity <HGSgMSAAccount>
   ```
