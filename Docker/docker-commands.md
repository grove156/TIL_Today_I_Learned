## Docker Commands

### 도커 명령어
1. pull - 도커허브에서 도커 이미지 다운로드(깃허브의 clone과 유사함)
2. images - 도커 이미지 리스트 보기
3. run - 도커 적재
4. ps - 도커 프로세스 상태 확인
5. attach - 정지된 도커 프로세스 탑제
6. logs - 도커 프로세스 로그 확인
7. tag - 도커 이미지명 변경
8. commit - 도커 프로세스 스냅샷 형태로 이미지 저장
9.  login - 도커허브에 로그인
10. push - 도커 허브에 image push (깃허브의 push와 유사함)
11. rmi - 시스템에 저장된 도커 이미지 삭제
12. save - 도커 이미지를 파일로 저장
13. load - 파일로 저장된 도커 이미지 시스템에 저장
14. prune - 도커 데몬이 사용하는 시스템 purge
15. cp - 도커 컨테이너 내부의 파일을 호스트로 복사해서 꺼내옴

### 도커 명령어 예제
1. pull - **docker pull** busybox
2. images - docker images
3. run - docker run -it busybox
4. ps - docker ps -a
5. attach - docker attach {process_id}
6. logs - docker logs {process_id}
7. tag - docker tag {current_image_name} {new_image_name}
8. commit - docker commit {process_id}  {image_name:version}
9. login - docker login {url}
10. push - docker push {image_name:version}
11. rmi - docker rmi {image_name:version}
12. save - dicjer save {image_name} > ./test.tgz
13. load - docker load < ./test.tgz
14. docker volume prune
15. docker cp {process_id}:/tmp.test.txt ./
