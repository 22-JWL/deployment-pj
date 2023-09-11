sudo apt update # 패키지 리스트 업데이트
sudo apt install nodejs # ubuntu에 node 설치
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash # pm2 모듈 설치를 위해서는 node 버전이 최소 14이상이어야 해서 nvm 모듈 설치
source ~/.bashrc # nvm 활성화
nvm -v # nvm 버전 확인
node -v # node 버전 확인

# 다음 중 한가지로 노드 설치

$ nvm install node # 최신 버전 설치
$ nvm install --lts # 최신 LTS 버전 설치
$ nvm install 16.14.0 # 특정 버전 설치
$ nvm install 16 # 특정 버전 16의 최신 릴리즈 설치

# 현재 설치된 node 버전 목록 확인

$ nvm ls

# 설치한 노드 버전으로 변경

$ nvm use 16.14.0

# node 버전 확인시 16 버전대로 변경 되어야 함

$ node -v

# mysql 설치 (설치 중간에 비밀번호 입력창 나오면 나중에 헷갈리지 않게 1234로 설정 권장)

$ apt install mysql-server

# mysql 설치 완료시, mysql 명령어로 원격 서버의 mysql 서버에 접속

$ mysql

# mysql 서버에 접속해서 sesac 데이터베이스, user 유저(비번: 1234) 생성

-- sesac 데이터 베이스 생성
create database sesac character set utf8mb4 collate utf8mb4*unicode_ci;
-- user 계정 생성하기 (비밀번호 1234)
CREATE USER 'user'@'%' IDENTIFIED WITH mysql_native_password BY '1234';
-- user 계정에 모든 권한 부여
GRANT ALL PRIVILEGES ON *.\_ TO 'user'@'%' WITH GRANT OPTION;
-- 현재 사용중인 mysql 캐시 지우고 새로운 설정 적용
FLUSH PRIVILEGES;
-- 생성된 계정 확인
SELECT host, user from mysql.user;

mysql 서버 종료하기 exit 명령어

# 무중단 배포를 위한 pm2 모듈 전역 설치

$ npm install pm2 -g

# 프로젝트(deployment-pj) 경로로 이동해서 프로젝트 실행 준비하기

$ cd deployment-pj
$ npm i # package.json으로 부터 node_modules 설치하기

#pm2 모듈 명령어 모음
$ pm2 start app.js # status가 online 상태라면 실행중
$ pm2 start app.js --watch # 소스 고치고 프로그램 재시동 자동화
$ pm2 monit # 프로세스 감시
$ pm2 list # 프로세스 목록 확인
$ pm2 stop [name] # name으로 프로세스 중단 (status가 stopped로 변경)
$ pm2 stop [id] # id로 프로세스 중단
$ pm2 kill # pm2 자체를 종료
$ pm2 log # 로그 확인 (재시동 자동화시 에러 메세지 확인시 유용)
