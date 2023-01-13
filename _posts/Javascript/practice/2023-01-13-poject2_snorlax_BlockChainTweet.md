---
title:  "프로젝트2 - BlockChain Tweet"
excerpt: "BlockChain을 Token을 이용한 tweet 작성"

categories:
  - Javascript_Practice
tags:
  - [Javascript,codestates,poject]

comment: true

author: Beomhyuck

toc: true
toc_sticky: true
 
date: 2023-01-13
last_modified_at: 2023-01-13
---

Porject2 - BlockChain Tweet
===

두번째 프로젝트의 주제는 BlockChain의 토큰을 이용하여 글을 작성하고 공유할 수 있는 트위터와 비슷한 게시판을 만드는 것이다.
이번의 주제도 저번과 같이 4명으로 팀을 구성하여 작업을 진행하였다.  
2주일의 시간동안 프로젝트를 진행하였는데 저번 프로젝트의 경험을 살려 이번에는 설계에 좀더 집중을 하고 프로젝트를 시작하기로 하였다.


설계의 과정은 아래 와 같이 진행하였다.   
1. 필요한 기능 정리
2. 플로우 차트 작성

![flowChart](/img/Blog/2023-01-13-Project2/flowChart1.PNG)

![flowChart2](/img/Blog/2023-01-13-Project2/flowChart2.PNG)

3. DB 테이블 설정
4. API 정리

https://docs.google.com/spreadsheets/d/1P64hLyROHWVclFQrc7v2e1hDKYZaBX7Lcif6gadV3oo/edit?usp=sharing

![API](/img/Blog/2023-01-13-Project2/API.png)



<br>

이번에는 프론트 엔드, 백엔드(DB,API), 스마트 컨트랙트로 역할을 나눠서 역할을 맡았는데 내가 맡은 역할을 백엔드에서 API를 작성하는 역할이었다.

결과물
===
메인페이지   
메인 페이지에서 게시글을 바로 쓸 수 있도록 되어 있다.
글을 쓸때는 1 token이 필요하고 좋아요를 10개받을떄마다 1token씩 받을 수 있다.   
![main](/img/Blog/2023-01-13-Project2/mainPage.PNG)

회원가입 페이지   
회원가입 페이지에서 가입을 할떄 Id, nickname이 중복되지 않으면 가입 된다.   
회원 가입시 지갑이 만들어지며 지갑의 keystore은 db에 저장된다.   
만들어진 지갑으로 token을 관리하게된다.   
개인이 지갑의 주소는 myPage에 들어가면 확인 가능하다.
![signUp](/img/Blog/2023-01-13-Project2/signUp.PNG)


로그인 페이지
매일 첫 로그인시 10token을 지급한다.   
![login](/img/Blog/2023-01-13-Project2/loginPage.PNG)

나의 페이지   
myPage에서는 nft민팅이 가능하고 다른 유저에게 토큰을 보낼 수 있다.
![myPage](/img/Blog/2023-01-13-Project2/myPage1.PNG)
![myPage](/img/Blog/2023-01-13-Project2/myPage2.PNG)

어려웠던 점
===
1. DB연결
 서버에서 API를 만들고 db를 쿼리문으로 접근해서 사용하는 역할을 하는데 만들어진 DB에 원격에서 연결이 안되어 db의 테이블만 공유해서 각자 Test를 진행하였다.
 이렇게 진행하다보니 DB의 내용이 공유가 안되어 내가 작성했을때 정상동작되었던 기능들이 다른 사람이 Test를 할때는 DB에 데이터가 없어 기능을 확인하는데 많은 시간이 들었다.
 DB의 원격 접속 하는 방법을 추후에 학습이 필요하다.

2. eth 수수료
 smartContract로 erc20과 erc721(nft)를 작성하고 이용하였는데 두개의 경우 모두 eth수수료가 발생하였다. erc20의 경우 글을 작성할때, nft민팅할때 사용되고 erc721의 경우 프로필 이미지를 바꿀때 사용된다.
 이 모든 기능에서 eth의 수수료가 발생하였고 transaction fee를 제대로 마련하지 못할경우 transaction을 만들지 못하고 에러가 나버렸다. 그런데 이 페이지의 경우 회원가입을 할때 지갑을 신규로 만들었기 때문에 eth는 0으로 시작하는 부분이 문제였다.
 이를 해결하기 위해서 첫 로그인 할떄 수수료로 사용할 eth도 같이 지급하는 방식으로 해결했지만 명쾌한 해결책은 안되는 듯 하다.

3. 비동기화
 서버에서 DB의 데이터를 읽어오는 과정과 smartContract를 이용하는 과정 모두 시간이 얼마간 필요한 일이고 db에서 읽어온 데이터를 smartContract에서 이용하는 경우가 많아 비동기화 이슈가 발생했다. 당장은 기능을 위해서 코드를 길게 적으며 해당 이슈를 해결했는데 시간이 좀 더 있었다면 깔끔하게 코드를 정리했으면 가독성 좋은 코드를 만들수 있었을 듯하다.

아쉬웠던 점
===
이번 프로젝트의 경우 처음 설계를 하는데 하루를 쓰고 진행해서 그런지 저번 프로젝트 보다 좀 더 쉽게 진행되었다. 하지만 프로젝트를 진행하면서 아쉬웠던 부분이 몇몇 있는데 나 혼자 작업하는게 아니라 다른 사람들과 협업을 통해서 일을 진행하다 보니 내가 만든 기능을 postman으로는 확인 되었지만 연결해 봤을때 이런저런 문제가 발생하는 경우가 많았다. DB연결의 경우도 각자 DB를 만들어서 테스트를 진행하다보니 DB의 내용이 달라 여러 시행착오를 겪었다. 이런 개발환경과 관련된 부분을 개선하기 위한 방법을 고려해 봐야될 듯 하다.

git Hub : https://github.com/codestates-beb/beb-07-second--04