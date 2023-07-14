# dockerfile_example

1. vagrant 안에서 git clone https://github.com/devlukej/dockerfile_example.git 실행
2. 디렉토리 경로 dockerfile_example로 이동
3. 명령어 docker compose -d 실행 - 해당 경로 docker-compose.yml 실행이 되는 것
4. docker ps -a 명령어 실행하여 컨테이너가 잘 실행 되고 있는지 확인
5. 192.168.33.200 접속하여 잘 뜨는지 확인

- nginx 컨테이너 html 기본 경로 : /usr/share/nginx/html
- apache2 컨테이너 html 기본 경로 : /usr/www/html