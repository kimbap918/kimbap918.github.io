## github.io 블로그 업로드 오류시 확인사항

며칠 전에 GitHub.io 업로드 에러가 발생해서 블로그에 TIL업로드를 한동안 못한 적이 있었다.

주말에 검점 차 확인해보니 원인이 확인돼서 다시 비슷한 일이 일어났을 때 대처할 수 있도록 기록해두려고 한다.

<br>

#### github.io 푸시 반영이 안될때  

![githubError_image]({{site.baseurl}}/images/githubError(3).png)

 빨간 네모 부분을 클릭

<br>

![githubError_image]({{site.baseurl}}/images/githubError(2).png)

Build를 클릭해서 에러 내용 확인

<br>

![githubError_image]({{site.baseurl}}/images/githubError(1).png)

에러 내용 확인 후 해당 파일 찾아서 수정

<br>

#### 자주 발생하는 실수

![githubError_image]({{site.baseurl}}/images/githubError(4).png)

포스팅 정보 입력하는 부분에서 콜론(:) 사용 후 띄워쓰기를 하지 않았을때 오류가 발생함. 

<br>

![githubError_image]({{site.baseurl}}/images/githubError(5).png)

{% raw %}{% %}{% endraw %} 태그 사용시, Liquid tag error 발생,

위 사진과 같이 `사용되는 태그 사이에{% raw %}, {% endraw %} ` 를 삽입하면 해결됨

<br>



