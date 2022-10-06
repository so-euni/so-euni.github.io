## 프로젝트 전체적인 서버 구성 ## 
### nginx + uvicorn(ASGI 웹 서버) + gunicorn + Django-ninja(Django+FastApi) ###

- nginx<br>
대중적으로 많이 사용하는 apache와 nginx,
속도나 부하 등 여러가지 면을 고려해 nginx를 사용하기로 한다.


- uvicorn / uvicorn<br>
보통 uvicorn/gunicorn 중 택일하여 사용하는데, 이번 프로젝트에서는 왜 두개를 모두 사용할까?
uvicorn: single Thread만 지원 (1 Worker가 모든 요청을 처리, 동시 대용량 처리가 어려움)
gunicorn: multi Thread를 지원 (비동기는 아님)

일반적으로, Python 애플리케이션을 실행하기 위해서는 WSGI 구현이 필요하다.
WSGI는 요청을 받고 응답을 반환하는 동작이 단일 동기 호출 방식으로 처리되기 때문에, 오랜 시간 연결을 유지하는 Websocket이나 긴 HTTP 요청을 처리하기에 적합하지 않다.
ASGI는 이러한 단점을 보완해 비동기 통신을 지원하며, 클라이언트간의 여러 통신을 주고 받을 수 있다.

gunicorn은 여러 개의 worker를 보유하고 있으며, 각 worker는 모두 uvicorn을 가지고 있다.
Master Worker 하위에 Slave Worker들이 존재한다. (아래 이미지 참고)
Master Worker가 죽으면 끝이지만, Slave Worker가 죽게 되면 해당 Worker에만 영향을 끼치게 된다.
![workers](/assets/img/custom/worker.png "workers img")


- Django-ninja(Django+FastApi)<br>

