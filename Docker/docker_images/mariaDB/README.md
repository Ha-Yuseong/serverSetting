# Docker에 MariaDB 설치

<details>
<summary> <b>MariaDB란 무엇일까요?</b> </summary><br>

#### MariaDB란 MariaDB는 "MySQL"에서 Fork(분기, 분파)한 오픈소스 기반 관계형 데이터 베이스 관리 시스템 (RDBMS) 입니다.<br>
MySQL은 1995년에 릴리즈된 오픈소스 RDBMS입니다. 매우 인기가 많은 RDBMS로 현재도 여러 환경에서 이용되고 있는 대표적인 RDBMS입니다.<br>
그런데 MySQL은 2009년 OracleDB로 유명한 Oracle에 인수되게 됩니다.<br>
이 과정에서 라이선스 관련한 분쟁이 일어났고 이에 반발한 MySQL의 창시자가 2009년에 완성된 MySQL 5.1.38의 버전의 코드에서 Fork하여 만든 것이 MariaDB입니다.<br>

#### 쉽게 말해서 MaraiDB는 MySQL이라는 조상에서 분파된 RDBMS입니다.

( 이건 기억을 더듬어 쓰는 것이기 때문에 확실하진 않은 이야기로만 들어주세요. 제가 인턴 때 강사에게 들었던 얘기로는 OracleDB가 당시 MySQl을 인수하고 있었던 썬이라는 기업(JAVA를 만든걸로 유명하죠)을 합병할 때 MySQL 업데이트를 반드시 책임지고 합병해야하는 조건이 붙게 되었다고 합니다. 그런데 Oracle입장에서는 자신들의 DB만으로도 충분한데 굳이 MySQL까지 담당해야하는것이 여간 껄그러운 일이 아닐 수 없었다고 합니다. 그래서 합병 과정 중 여러 충돌이 발생하게 되다보니 MySQL을 개발하던 많은 개발자들이 이탈하여 MariaDB를 만들게 되었다고 합니다. )

저는 개인 프로젝트 이용 시 학부시절엔 MySQL을 사용하다가 현재는 MariaDB를 더욱 사용하고 있습니다. MariaDB를 이용하는 이유는 다음과 같습니다.<br>
1. MySQL의 수정 버전이므로 MySQL보다 복제 및 쿼리 속도 등의 성능이 약간 더 좋다.
2. MySQL에서 Fork한 RDBMS이기 때문에 MySQL과의 호환성이 매우 뛰어나다.
3. 오픈소스 기반 RDBMS이기 때문에 자유롭게 사용이 가능하다.
4. 업데이트가 MySQL보다 더욱 활발하다.
   
위의 사항 외에도 보안성이 더 좋고 스토리지 엔진이 더욱 뛰어나다는 장점도 존재합니다.<br>

더욱 자세한 설명은 아래의 링크들에서 확인할 수 있습니다.

https://aws.amazon.com/ko/compare/the-difference-between-mariadb-vs-mysql/<br>
https://linuxnatives.net/2015/10-reasons-to-migrate-to-mariadb-if-still-using-mysql

</details>

### Docker에 MariaDB image 설치

    Docker를 설치해보도록 합시다.
    
    ubuntu 기준으로는 아래에 공식사이트에서 실행시켜야할 명령들을 제공합니다.
    https://docs.docker.com/engine/install/ubuntu/

    1. 먼저 도커 레포지터리를 세팅해야합니다. 이유는 추후 docker install, update를 레포지터리에서 수행 가능하게 되기 때문이라고 합니다.

    아래의 명령들을 위에서부터 차례대로 수행해줍니다.

    # Add Docker's official GPG key (아래는 도커 공식 GPG key 추가하는 코드들):
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg

    # Add the repository to Apt sources (레포지터리를 apt 소스에 추가하는 코드들):
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

    2. docker pakage를 install합니다.
    
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    3. docker engine이 제대로 설치되었는지 hello-world 이미지를 실행하여 확인해봅니다.

    sudo docker run hello-world

정상적으로 설치하고 3번을 수행하면 결과는 다음과 같습니다.<br><br>
<img src="./result_image/docekr_result.png"><br>