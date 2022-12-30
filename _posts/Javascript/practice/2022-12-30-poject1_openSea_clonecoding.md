---
title:  "프로젝트1 - OpenSea clone Coding"
excerpt: "openSea를 흉내낸 페이지 만들기"

categories:
  - Javascript_Practice
tags:
  - [Javascript,codestates,poject]

comment: true

author: Beomhyuck

toc: true
toc_sticky: true
 
date: 2022-12-30
last_modified_at: 2022-12-30
---

Porject1 - openSea clone coding
===

첫번째 프로젝트의 주제는 NFT거래 사이트인 openSea와 같은 홈페이지를 만드는 것을 목표로 하여 
4명으로 팀을 구성하여 작업을 진행하였다.  
1주일의 시간동안 프로젝트를 진행하였는데 시간을 생각해 봤을때 openSea의 모든기능을 구현하는것은 무리라는 생각이 들어 만들 목록을 정했다.  
page 별로 다음과 같은 구성을 목표로 하였다.

1. MyPage - 개인정보를 담아 두는 페이지
2. Explore - NFT 검색
3. Collection
4. Minting - NFT 생성 페이지
5. NFT구매 페이지

<br>

그 중에서 내가 맡은 역할을 NFT관련한 부분을 맡아서 NFT 민팅, 구매를 구현하는 역할 이었다.

결과물
===
결과물에는 더미데이터를 넣어 두었다.

메인페이지
![main](/img/Blog/2022-12-30-Project1/main_page.PNG)

검색페이지
NFT를 검색하는 페이지
![explore](/img/Blog/2022-12-30-Project1/explore_page.PNG)

NFT 생성 페이지   
NFT를 생성할수 있는 페이지로
이미지 파일을 올리고 제목, 설명을 적으면 그 데이터를 ipfs로 저장하고 NFT로 minting을 진행한다. 연결된 계정으로 민팅 진행
![minting1](/img/Blog/2022-12-30-Project1/minting_page.PNG)
![minting2](/img/Blog/2022-12-30-Project1/minting_page2.PNG)
![minting3](/img/Blog/2022-12-30-Project1/minting.PNG)

NFT 구매 페이지
NFT를 구매할 수 있는 페이지
![buy](/img/Blog/2022-12-30-Project1/buy_page.PNG)


어려웠던 점
===
1. 리액트 사용
- 리액트를 배우지 시간이 꽤 지나기도 해서 리액트를 통해 페이지를 만드는데 바로 방법이 떠오르지 않아 구글링 하는데 많은 시간을 소모했다.

2. smart contract
- 스마트 컨트랙트에 대한 이해가 부족하여 컨트랙트를 어떻게 사용하는지에 대해서 학습하면서 진행하여야 했다.

3. ipfs
- NFT를 만들면서 이미지 데이터를 저장할 방법을 생각해야 됬는데 ipfs를 사용하는게 서버를 따로 만들 필요가 없어보여 사용하였다.
infura를 이용하여 ipfs를 사용했는데 infura의 정책변경으로 예전에 올라왔던 자료들을 참고하여 만든 코드가 정상작동 하지 않는 부분이 많아 이를 해결하기 위해 해결방법을 찾는데 많은 시간이 걸렸다.


아쉬웠던 점
===
시간이 부족하다고 느껴서 설계를 치밀하게 하지 못하고 작업에 들어가니 작업을 진행하면서 다른 팀원이 작업한 내용과 내가 작업한 내용이 충돌하는 경우가 많았고 개발환경을 세팅하는데에도 충돌이 발생해 이를 해결하는데 시간이 들었다. 이번 경험을 통해서 설계의 중요성을 느낄수 있었다. 다음 프로젝트를 진행할때는 설계에 좀더 많은 시간을 들이는게 결과물에 있어서나 작업을 수월하게 진행하는데에 도움이 될것이다.

그외 에도 프로트엔드/백엔드와 같이 역할을 나누지 않고 각 페이지별로 각자 맡아서 하다보니 이거했다 저거했다 하는 느낌이 많이 들어 효율적이지 못하다는 느낌을 받았다. 다음에는 프론트엔드/백엔드/스마트컨트랙트로 역할을 나눠서 개발을 진행하는게 좋을듯 하다.