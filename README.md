# px4-quadrotor-HW-parts
storage for 3d printing parts of px4 quadrotor equipped with D435 and T265

for quick writing i gonna use my own language

*목적 : gazebo 와 rviz 에서 이쁜 모델로 쥬얼라이즈 하기 위해서 커스텀 sitl 모델 생성   
   
(1) 솔리드 웍스를 이용하여 3d 모델을 생성하였다. 이때 thingiverse 에서 f450모델을 다운 받은후   
몇몇 부분 수정과 추가를 통해 만들었다.   
(2) https://ola-page.tistory.com/3 를 참고하여 urdf 파일 생성, 결과물은 'drone_without_realsense.zip' 이다.   
(3) 알비즈에서 실행하여 보니 이러한 모양   
![image](https://user-images.githubusercontent.com/72853382/123039706-972f2c00-d42d-11eb-804f-7304ecf6fdc3.png)   
(4) 가지보에서 보니 걍 흰색으로 나옴 그래서 https://answers.ros.org/question/51961/no-color-when-i-open-a-part-exported-from-solidworks-in-gazebo/
의 answer을 참고하여 gazebo reference 를 추가하지 색생이 잘나옴   
색상은 http://wiki.ros.org/simulator_gazebo/Tutorials/ListOfMaterials 리스트에서 보고 적당히 고름   
![image](https://user-images.githubusercontent.com/72853382/123039873-ce054200-d42d-11eb-8221-0bb0a05545d3.png)
