## Docker Command

- 설치여부 및 다운로드 받은 이미지 리스트 확인

  ```
  docker images
  ```



- image 가져오기

  ```
  docker pull httpd
  ```

  

- image 실행 (컨테이너 만들기)

  ```
  docker run httpd
  ```

  ```
  docker run --name ws2 httpd // container 이름 지정
  ```

  

- 실행중인 container들 확인하기

  ```
  docker ps
  ```



- container들 확인하기

  ```
  docker ps // 실행중인 컨테이너들만 나옴
  ```

  ```
  docker ps -a // 멈춘 컨테이너들도 나옴
  ```

  

- container 중단하기

  ```
  docker stop ws2 (이름 또는 id도 가능)
  ```



- 중단했던 container 재시작하기

  ```
  docker start ws2
  ```



- container 재시작 했을때 log 를 보고 싶다면

  ```
  docker logs ws2 // log가 한번만 나오고 끝남
  ```

  ```
  docker logs -f ws2 // 계속 log를 와칭하고 보여줌
  ```



- container를 삭제하고 싶을 때

  ```
  docker stop ws2 // 정지하고
  docker rm ws2 // 삭제
  ```

  ```
  docker rm --force ws2 // 정지없이 바로 삭제
  ```

  

- Image 삭제하고 싶을때

  ```
  docker rmi httpd
  ```

  

- port 지정해주고 싶을 때 (host 의 port 와 container의 port를 연결해준다)

  ```
  docker run -p 80:80 httpd // 앞의 80은 host의 port, 뒤의 80은 container의 port
  docker run -p 8000:80 httpd
  ```

  👉 host 자체에도 65535개의 port가 있음 -> container 각각에도 65535개의 자체 port가 있음 -> port를 지정해주고 싶을때는 host의 port와 container의 port를 각각 지정해줘야함 (image 자체에 container의 고정 port 를 지정되어있기도 함)



- container에 명령어 전달하고 싶을 때

  ```
  docker exec ws3 pwd
  ```

  ```
  docker exec ws3 /bin/sh 
  // container ws3의 shell을 열어줌 하지만 이 명령어는 실행과 동시에 shell을 닫아버림, sh은 본쉘
  ```

  ```
  docker exec -it ws3 /bin/sh 
  // i와 t는 별개의 옵션이나 t를 같이 써주는 것이 좋음 (실행을 유지할때 이 옵션들을 씀) // 이 명령어는 shell 자체를 열어줌
  ```

  ```
  exit // container shell 에서 빠져나올 때
  ```

  👉 /bin/sh 인 본쉘대신 /bin/bash 배쉬쉘이 기능이 더 많아서 이걸 쓰는걸 추천 bash쉘이 없다면 그냥 sh(본)쉘 쓰면 됨
  👉 nano나 vim 을 에디터 같은걸 쓰고 싶다면 apt 나 욤같은걸 사용해서 설치하면 된다

  ```
  apt update // apt 최신상태로 갱신
  apt install nano // nano 설치
  nano index.html // 이 파일이 nano로 편집되는 상태로 열림
  ```

  

- Host 와 container의  파일 시스템을 연결시켜주고 싶을 때 (Volume)

  ```
  docker run -p 8888:80 -v ~/Desktop.htdocs:/usr/local/apache2/ httpd
  ```

  👉 host는 하나의 운영체제 -> host 는 host 만의 file system도 가지며, 여러개의 container를 가짐 -> container들 각각도 내부에 file system이 있음 -> container가 삭제될 때 내부에 저장했던 file system이 지워지지 않도록 하려면 host 의 file system 과 container의 file systeㅐㅇm을 연결시켜주면 됨