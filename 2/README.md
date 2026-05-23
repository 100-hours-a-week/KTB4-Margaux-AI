## 사용법
```
uv add "fastapi[standard]"
uv add ollama
uv add sqlmodel
source .venv/bin/activate
fastapi dev main.py
```

## 환경설정
- fastapi[standard]>=0.136.1
- uvicorn>=0.47.0
- ollama: gemma4:e4b
- sqlmodel>=0.0.38
- sqlalchemy>=2.0.49

## 느낀 점
- 자바 스프링을 활용한 백엔드 서버를 구성해본 경험이 다수 있기에, 구조를 이해하는 데에 어려움은 없었다.
- FastAPI를 활용한 백엔드 서버를 구성하며, FastAPI와 starlette, pydantic의 관계에 대해 정확히 파악할 수 있었다.
  - 내가 내린 정의는 starlette은 FastAPI의 기반이 되는 ASGI 프레임워크이며, pydantic은 데이터 검증, 직렬화/역직렬화를 해주는 라이브러리이다.
  - 택배를 처리하는 물류공장을 예시로 들면
    - "택배 분류소가 FastAPI
    - 분류소의 심장인 컨테이너벨트가 starlette
    - 마지막으로 택배를 검증하고 포장하는 분류원이 pydantic
  - 이라고 생각했다.
- 현재는 Validation을 HTTPException을 사용하여 Default Class만으로 관리하고 있지만, Custom Exception Class를 만들고, Global Exception Handler 모듈로 분리해 오류 관리 기능을 분리하고 싶다.

## 개선 방안
- Custom Exception Class로 반복되는 예외를 정의하기.
- Global Exception Handler로 오류 관리 기능 분리하기.
- 현재는 post 요청 후 LLM을 이용한 요약을 바로 생성하여, 클라이언트에게 응답이 30초 지연되는 문제가 있다. -> 클라이언트에겐 생성완료 응답을 바로 주고, LLM에겐 요약 생성 요청을 비동기로 처리하도록 개선하기.
