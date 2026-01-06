# hello-docker

# image, container, process list 확인
docker image list -a
docker container list -a
docker ps -a

# image 가져오기
docker pull mysql:9.5.0

docker pull <image name:image tag>

# image로부터 container 만들기 (Container Name은 중복되지 않게)
docker run --name=<container 이름> -e <환경변수>=<환경값> -d <image name:image tag>
# mySql
docker run mysql:9.5.0
docker run --name=mysqldata -p 3306:3306 -v C:/docker/mySqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:9.5.0
# PostgreSql
docker run --name=postgresdata -p 5432:5432 -v C:/docker/pgdata18:/var/lib/postgresql/data -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=root -e POSTGRES_DB=myPGdb -d postgres:18

# Container 기동 또는 중지
docker container stop <container ID or container Name>
docker container start <container ID or container Name>

# Container 삭제
docker container rm <container ID>

# container로 진입 방법
docker exec -it <container ID or name> bash
docker exec -it some-mysql bash

# Image 삭제
docker image rm <image ID>