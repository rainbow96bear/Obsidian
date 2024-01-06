GIF 변환 응용프로그램을 만들기 위하여 ffmpeg와 fyne에 대한 공부가 필요하다고 느꼈습니다.
그 중 우선적으로 ffmpeg를 연습해둔다면 웹 페이지를 통하여 지금의 작업도 직접 만든 gif 변환기로 기록할 수 있다는 생각에 ffmpeg를 활용한 웹을 만들기로 결정하였습니다.

[변환기 작업물 레포지토리](https://github.com/rainbow96bear/gif_converter/tree/master/web/cmd)

# 사용 방법
1. main.go를 빌드하여 실행
2. localhost:8080으로 접속
3. 원하는 동영상을 선택
4. upload and convert 클릭
5. converted 폴더 확인

웹의 경우 ffmpeg를 익히기 위한 작업으로 웹에서 변환된 내용을 확인하는 기능은 미구현되었습니다.   

gui를 활용한 응용프로그램을 만들게 된다면 웹을 추가적으로 보완하겠습니다.