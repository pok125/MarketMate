# MarketMate

## 1. 프로젝트 소개

### 1-1. 개요
- E-Commerce 서비스 베타버전의 기본 기능 구현을 목표 하였고 Django의 DRF를 통한 REST API 서비스 입니다.

### 1-2. 기능 소개
- 사용자 관련 기능
    - 사용자는 구매자와 판매자로 구분되며, 회원 가입 시점에 정할 수 있습니다.
    - 각 회원 유형은 자신의 역할만 수행할 수 있으며, 회원 가입 이후에는 변경할 수 없습니다.
    - 회원 가입, 로그인, 로그아웃, 회원 정보 수정, 회원 탈퇴가 가능합니다.
    - 로그인은 Django REST framework에서 제공하는 토큰 인증 기능을 활용하고 있습니다.

- 상품 관련 기능
    - 모든 상품은 판매자와 구매자 모두 목록과 상세 보기 형식으로 조회할 수 있습니다.
    - 판매자의 경우 자신이 판매할 상품을 등록, 수정, 삭제할 수 있습니다.
    - 구매자의 경우 구매하고자 하는 상품을 바로 구매하거나, 장바구니에 담는 등의 행동을 할 수 있습니다.

- 문의 관련 기능
    - 구매자는 구매하고자 하는 상품에 문의를 작성, 수정, 삭제할 수 있습니다.
    - 이에 대해 판매자는 답변을 작성할 수 있으며, 한 개의 문의는 한 개의 답변을 갖습니다.

- 후기 관련 기능
    - 구매자는 구매한 상품에 대해 후기를 작성, 수정, 삭제할 수 있습니다.

- 장바구니 관련 기능
    - 구매자는 상품을 바로 구매하는 대신 장바구니에 담을 수 있습니다.
    - 장바구니에 담을 시 구매하고자 하는 수량을 정해 담을 수 있습니다.
    - 이미 장바구니에 담은 상품일 경우, 같은 이름의 새 상품을 장바구니에 담는 대신 기존 물품의 개수를 증가시킵니다.
    - 장바구니에 담은 상품은 수량을 증감하거나 삭제할 수 있습니다.

- 구매 관련 기능
    - 상품의 상세 페이지에서, 상품을 바로 구매할 경우, 해당 상품에 대한 주문서를 만들고 정말 구매할 것인지 여부를 확인합니다.
    - 주문서 페이지에서 구매를 선택하게 되면 API를 통해 실제 구매로 넘어가게 됩니다.
    - 이때, API에서 제공하는 사전 결제 정보 등록 기능을 활용하여 주문서와 실제 결제될 내용에 대한 검증하게 됩니다.
    - 또한 상품의 재고와 현재 구매하려는 수량을 비교하여, 상품의 재고가 부족할 경우 결제를 중단시킵니다.
    - 결제가 성공적으로 완료되면 결제 테이블을 관련 정보들로 수정합니다.

### 1-3. 프로젝트 참여 인원 및 역할 분담
- 이광호: 팀장, DB모델 설계, Token을 이용한 인증, 인가, 전체 기능 총괄, S3 이미지 처리
- 성낙훈: 인증, 인가, 전체 기능 총괄, 결제 기능 개발
- 김태은: 상품, 문의, 후기 기능 개발, 문서 작성
- 전정헌: 장바구니, 결제 기능 개발, 문서 작성, 배포

### 1-4. 프로젝트 수행 기간
- 2023년 08월 17일 ~ 2023년 09월 04일(2주)


## 2. 기술 스택 및 배포 URL

### 2-1. 기술 스택
- 사용 언어

    <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white"><img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=JavaScript&logoColor=white">

- 웹 프레임워크

    <img src="https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=Django&logoColor=white">

- 형상 관리

    <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=Git&logoColor=white"><img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=GitHub&logoColor=white">

- 배포

    <img src="https://img.shields.io/badge/Amazon S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white">
    <img src="https://img.shields.io/badge/Amazon EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white">
    <img src="https://img.shields.io/badge/Amazon RDS-527FFF?style=for-the-badge&logo=amazonrds&logoColor=white">

    <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">

### 2-2. 배포 URL
- 프론트엔드: https://front.marketmate.digital/
- 백엔드(API 서버): https://www.marketmate.digital/

### 2-3. 테스트 계정
```
구매자 계정: buyer1@email.com / qwerty123!@#
판매자 계정: seller1@email.com / qwerty123!@#
```

## 3. 프로젝트 구조, 아키텍처 구성도, API 명세서, 데이터베이스 모델링

### 3-1. 프로젝트 구조
```
📦MarketMate
 ┣ 📂carts
 ┃ ┣ 📂migrations
 ┃ ┃ ┗ ...
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜permissions.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂main
 ┃ ┣ 📜asgi.py
 ┃ ┣ 📜env.py
 ┃ ┣ 📜settings.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜wsgi.py
 ┃ ┗ 📜__init__.py
 ┣ 📂nginx
 ┃ ┣ 📜Dockerfile
 ┃ ┣ 📜marketmate.conf
 ┃ ┗ 📜nginx.conf
 ┣ 📂products
 ┃ ┣ 📂migrations
 ┃ ┃ ┗ ...
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂purchases
 ┃ ┣ 📂migrations
 ┃ ┃ ┗ ...
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂questions
 ┃ ┣ 📂migrations
 ┃ ┃ ┗ ...
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂reviews
 ┃ ┣ 📂migrations
 ┃ ┃ ┣ 📂__pycache__
 ┃ ┃ ┗ ...
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂static
 ┃ ┣ 📂admin
 ┃ ┃ ┃ ┗ ...
 ┃ ┗ 📂rest_framework
 ┃ ┃ ┃ ┗ ...
 ┣ 📂users
 ┃ ┣ 📂migrations
 ┃ ┃ ┗ ...
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜permissions.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂utils
 ┃ ┗ 📜images.py
 ┣ 📜.env
 ┣ 📜.gitignore
 ┣ 📜docker-compose.yml
 ┣ 📜Dockerfile
 ┣ 📜manage.py
 ┣ 📜README.md
 ┗ 📜requirements.txt
```

### 3-2. 아키텍처 구성도
- AWS 서비스를 많이 활용했습니다.
    - 프론트엔드는 S3에 배포했습니다.
    - 백엔드는 EC2에 배포했습니다.
        - 도커를 활용하여 웹 서버와 WSGI + Django를 분리하되 연동되도록 만들었습니다.
    - 사용자가 업로드하는 이미지는 백엔드 서버가 아니라, S3에 업로드됩니다.
    - DB는 RDS에 설치했습니다.
        - PostgreSQL을 사용하고 있습니다.
![아키텍처](./readme_images/00_아키텍처구성도.png)

### 3-3. API 명세서
- https://www.notion.so/0ea2c4da504b4289a5e04bfcaff160c3
![API명세서_1](./readme_images/00_API명세_1.png)
![API명세서_1](./readme_images/00_API명세_2.png)

### 3-4. 데이터베이스 모델링
- ERDCloud를 사용한 DB 모델링
![ERD](./readme_images/20_ERD.png)


## 4. 상세 페이지 설명
- 메인 페이지
    - (비로그인시) 상품 목록, 로그인, 회원가입 메뉴를 사용할 수 있습니다.
![메인(비로그인)](./readme_images/01_메인(비로그인).JPG)
    - (로그인시) 상품 목록, 로그아웃, 회원정보, 장바구니 메뉴를 사용할 수 있습니다.
![로그인(구매자)](./readme_images/02_로그인시(구매자).JPG)
![로그인(판매자)](./readme_images/02_로그인시(판매자).JPG)

- 회원가입
    - 회원가입시 구매자와 판매자를 구분합니다.
    - 구매자는 구매만, 판매자는 판매만 가능합니다.
    - 역할 변경은 불가합니다.
![회원가입](./readme_images/03_회원가입.JPG)

- 로그인
    - 이메일과 비밀번호로 로그인 할 수 있습니다.
![로그인](./readme_images/04_로그인.JPG)
    - 로그인 성공 시 토큰이 발급되며, 이후 이를 통해 인증을 시도하게 됩니다.
    - 현재 로그인은 일회성입니다. 따라서 세션 스토리지에 저장하여, 브라우저나 탭 종료시 휘발되는 것을 의도했습니다.
![토큰](./readme_images/05_토큰.JPG)

- 마이페이지
    - 구매자와 판매자의 마이페이지를 별도로 구성하였습니다.
    - (공통) 회원 정보 수정, 비밀번호 변경, 회원 탈퇴를 할 수 있습니다.
    - (판매자) 판매 상품을 등록·조회·수정할 수 있습니다. 
    - (구매자) 주문 현황 조회, 주문 상품 환불을 할 수 있습니다.
![회원정보_공통](./readme_images/06_회원정보_공통.JPG)
![회원정보_구매자](./readme_images/06_구매자전용.JPG)
![회원정보_판매자](./readme_images/06_판매자전용.JPG)
![비밀번호수정](./readme_images/06_정보수정.JPG)
![비밀번호수정](./readme_images/06_비밀번호변경.JPG)
![탈퇴](./readme_images/06_회원탈퇴.JPG)

- 상품 등록 페이지
    - 구매자는 상품을 등록할 수 없습니다.
    - 판매자의 경우 카테고리, 상품명, 가격, 수량, 상품 설명, 상품 판매 상태 등을 설정하여 판매할 물품을 등록할 수 있습니다.
    - 대표 이미지는 1장, 상세 이미지는 여러 장을 등록할 수 있습니다.
    - 등록한 이미지는 S3 버킷에 저장되고, DB에는 경로가 저장됩니다.
![상품등록](./readme_images/07_상품등록.JPG)

- 상품 목록 페이지
    - 현재 등록된 모든 상품의 목록을 확인할 수 있습니다.
    - 검색창을 통해 검색하거나, 카테고리 버튼을 눌러 각 카테고리에 맞는 상품만 필터링 할 수 있습니다.
![상품목록](./readme_images/08_상품목록.JPG)

- 상품 상세 보기 페이지
    - 모든 사용자는 상품 목록에서 원하는 상품을 선택하여 상세 내용을 확인할 수 있습니다.
    - 상품명, 카테고리, 가격, 재고, 상품 설명, 판매 상태, 평점, 상품에 대한 문의, 상품에 대한 후기를 확인할 수 있습니다.
![상품상세](./readme_images/09_상품상세.JPG)

- 상품 문의 페이지
    - (구매자) 상품에 대해 문의할 내용을 입력한 후 등록할 수 있습니다.
    - 기 입력된 문의 내용을 수정, 삭제할 수 있습니다.
    - (판매자) 구매자가 등록한 문의 내용에 답변할 수 있습니다.
    - 기 입력된 답변 내용을 수정, 삭제할 수 있습니다.
    - 하나의 문의에 하나의 답변을 제공할 수 있습니다.
![상품문의](./readme_images/10_문의.JPG)

- 상품 후기 페이지
    - 해당 상품을 구매한 구매자만 평점과 상품 후기를 등록할 수 있습니다.
    - 기 입력된 평점과 상품 후기는 수정할 수 있습니다.
![상품후기](./readme_images/11_후기.JPG)

- 장바구니 페이지
    - 구매자는 상품 상세 보기 페이지에서 수량을 지정하고 해당 상품을 장바구니에 담을 수 있습니다.
    - 기존에 등록되어 있던 상품을 다시 장바구니에 등록할 시, 새 상품으로 등록되는 것이 아니라 기존의 물품을 수량만 변경합니다.
    - 장바구니에 등록된 상품의 수량을 변경할 수 있으며 삭제도 가능합니다.
    - 체크박스에 체크한 상품 전체를 구매할 수 있습니다.
![장바구니](./readme_images/12_장바구니.JPG)

- 주문 페이지
    - 상품 상세 보기 페이지와 장바구니 페이지에서 구매를 시도할 수 있습니다.
    - 각 페이지에서 구매 버튼을 클릭시, 데이터를 통해 한 개의 주문이 만들어지며 이를 바탕으로 결제가 이루어지게 됩니다.
    - 결제 수단을 선택할 수 있지만, 현재는 카드 결제만 선택할 수 있습니다.
![주문](./readme_images/13_주문.JPG)

- 결제 페이지
    - 주문 페이지에서 결제 버튼을 클릭시 실결제로 이행합니다.
    - 포트원 API에서 제공하는 사전 결제 등록 시스템을 활용하여 결제 내용을 사전 등록하고, 반환되는 데이터를 활용하여 하나의 결제 데이터를 생성합니다.
    - 이 때 물품의 재고와 주문하려는 물품 수량을 비교한 다음, 재고보다 주문 수량이 많을 경우 결제를 진행할 수 없습니다.
    - 결제가 성공적으로 완료되면 포트원 API에서 반환하는 데이터를 활용해 주문 데이터와 결제 데이터, 물품 수량 데이터를 업데이트합니다.
![결제](./readme_images/14_결제.JPG)

- 결제 내역 페이지
    - 구매자는 자신이 구매한 내역을 확인할 수 있습니다.
    - 해당 페이지에서 기 결제한 주문을 결제 취소할 수 있습니다.
![결제내역](./readme_images/15_결제내역.JPG)


## 5. 프로젝트 완료 후 감상
- 이광호: 처음부터 끝까지 DRF를 이용하여 REST API 프로젝트를 진행해 보며, 최대한 초반에 팀원들과 기능들,  URL, DB 설계를 먼저 진행하고 개발에 들어갔음에도 불구하고 생각했던 대로 진행되지 않았습니다. 이 경험을 통해 다양하게 프로젝트를 진행해 본 경험이 중요하다 느꼈고 개발보다 초반 설계에 더 많은 시간을 들여야 한다고 느꼈습니다.

- 성낙훈: 이번 프로젝트를 통해 처음 접해본 기술들도 사용해 보고 기획부터 배포까지 개발을 진행하면서 많은 걸 배울 수 있었습니다. 개발 단계에서는 처음 접해본 결제 API를 통해 결제 시스템의 개발을 흐름을 이해하는데 어려웠습니다. 이 과정에서 결제 시스템의 작동원리를 배울 수 있었고 또한 클라이언트와 서버의 동작 방식에 대해 좀 더 알 수 있었습니다. 또한 협업에서의 의사소통의 중요성과 개발 기간을 잘 분배해야 한다는 걸 배웠습니다.

- 김태은: 프로젝트를 구성할 때는 구현해야 할 기술과 작업 항목이 많았고, 계획된 기간보다 길어질까 봐 걱정했습니다. 그러나 개발 과정에서 API와 DB 설계, 에러코드 작성, 코드 컨벤션 준수 등 기초 작업의 중요성을 느꼈고, 이는 프로젝트의 완성도를 높이는 데에도 중요하다는 것을 배웠습니다. 
DRF를 사용하면서 백엔드 개발에 대한 이해가 높아진 것 같습니다. 그러나 여전히 프런트와의 연결 관련하여 더 많은 학습과 노력이 필요하다고 느꼈습니다.

- 전정헌: 프로젝트를 진행하면서 가장 많이 느꼈던 것은 왜와 어떻게였습니다. 왜 이렇게 해야 하는지, 어떻게 해야 그렇게 할 수 있는지. 이러한 과정들을 거치며 배울 수 있었던 것은, 혼자 고민만 하는 건 아무 의미가 없다는 것이었습니다. 공식 문서를 찾아보고, 커뮤니티에 관련 내용들을 검색하며, 무엇보다 신뢰할 수 있는 동료들과 훌륭한 조언을 해주시는 멘토님들과 의견을 나누는 것. 고민할 시간에 우선 행동하는 것이 중요하다는 것을 배울 수 있었습니다.
