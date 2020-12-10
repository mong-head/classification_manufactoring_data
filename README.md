# classification_manufactoring_data
제조업 데이터 classification

## data characteristic 및 preprocessing

* preprocessing위해서 적용해본 것 

|방법|사용해본 이유|사용여부|이유|
|---|---|---|---|
|gray scale |연산량 줄임, 애초에 이미지가 흑백 이미지임|O| 사용한 이유와 동일|
|addition and subtraction|밝게, 어둡게 만듦|X|이미지의 특징을 살리는 것과 관련없음|
|contrast adjustment * histogram equalization|선명하게 만듦|X| 이미지 외곽선을 뽑으려 할 때, 조금 검던 부분이 완전 검게 되거나 그 반대의 경우도 있어서 외곽선이 끊겨서 표현됨|
|edge detection(laplacian,sobel,scharr,gradient) | 외곽선을 따려고 사용|X| 이미지의 특징을 살리지 못함|
|gaussian blur| 노이즈 줄이기 |X|노이즈를 줄이려 하면 결함까지 없어져 버림|
|adaptive threshold|외곽선따기|O| gaussian blur사용, 이미지의 특징을 가장 잘 나타낸다고 생각하였음. K=5,C=5사용함|
|Homomorphic Filter|제품마다 이미지 광원에 영향을 많이 받아서 광원을 줄이기 위함|X| 실제로 사용해보니 광원효과를 완전히 없애지 못하였고, 외곽선 뽑는데 도움을 주지 못함|

* 결함이 잘 나타나지 않는 이미지로 특징 잘 보이는지 비교

 1. gray scale -> 2. (histogram equalization) -> 3. (gaussian blur) -> 4. adaptive threshold

    * ()는 적용한 것과 안한 것 비교함. 즉 (1-2-3-4, 1-2-4, 1-3-4, 1-4) 모두 비교
    * gaussian blur는 kernel filter size 1x1,3x3,5x5비교

  | 1-2-3 or 1-3 or 1 | 그 후, 4적용 |
  |---|---|
  |<img src="https://user-images.githubusercontent.com/52481037/101777914-7d379700-3b36-11eb-9d8d-79183286eb37.jpg" width="600"/>|<img src="https://user-images.githubusercontent.com/52481037/101777951-87599580-3b36-11eb-94d8-c60696a1c01d.jpg" width="600"/>|
 
  * sobel등을 포함한 외곽선 뽑는 방식 사용하지 않은 이유
  
    <img src="https://user-images.githubusercontent.com/52481037/101779407-96414780-3b38-11eb-9f1c-001d247047d7.jpg" width="200"/>
 
 * 결함이 잘 보이는 이미지로 다시 확인
  
  <img src="https://user-images.githubusercontent.com/52481037/101778839-c3d9c100-3b37-11eb-9653-71399fd750a9.jpg" width="600"/>

* 결론

  * preprocessing : gray scale -> adaptive threshold
  * 이유 : sobel등을 포함한 외곽선 따는 방식은 제일 중요한 결함을 보여주지 못하였고, histogram equalization과 gaussian blur는 어떤 이미지인가에 따라서 영향을 많이 받았다.
  


