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
docker pull mysql:9.5.0
docker run mysql:9.5.0
docker run --name=mysqldata -p 3306:3306 -v C:/docker/mySqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:9.5.0
# PostgreSql
docker pull postgres:18
docker run --name=postgresdata -p 5432:5432 -v C:/docker/pgdata18:/var/lib/postgresql/data -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=root -e POSTGRES_DB=myPGdb -d postgres:18
# msSql
docker pull mcr.microsoft.com/mssql/server:2022-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=msSQL1234!" -p 14330:1433  --name mssql -d mcr.microsoft.com/mssql/server:2022-latest
  # docker run (with backup 폴더 연결 옵션)
mkdir C:\workspace\hello-docker\backup
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=msSQL1234!" -p 14330:1433  --name mssql -d -v C:\workspace\hello-docker\backup:/var/opt/mssql/backup mcr.microsoft.com/mssql/server:2022-latest

# docker backup 만들기
docker exec -it mssql /opt/mssql-tools18/bin/sqlcmd -S localhost -U sa -P "msSQL1234!" -Q "BACKUP DATABASE [MyDb] TO DISK = N'/var/opt/mssql/backup/MyDb.bak' WITH INIT, COMPRESSION" -C

# docker backup file restore
docker exec -it mssql /opt/mssql-tools18/bin/sqlcmd -S localhost -U sa -P  msSQL1234!" -C `
  -Q "RESTORE DATABASE [MyDb1234]
      FROM DISK = N'/var/opt/mssql/backup/MyDb1234.bak'
      WITH MOVE N'MyDb'     TO N'/var/opt/mssql/data/MyDb1234.mdf',
           MOVE N'MyDb_log' TO N'/var/opt/mssql/data/MyDb1234_log.ldf',
           REPLACE, RECOVERY;"

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