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
   
      
(5) 기본적인 준비는 끝났으니 이제 px4의 iris.sdf를 기반으로 바꿔주려한다.
-    cd ~/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes
-    cp 101_iris_rtps 1025_custom
-    gedit CMakeLists.txt
-    #여기서 1025_custom 추가해줍시다
-    #뎁스카메라부분은 저는 이미 추가되어있으므로, 여기 참고 https://github.com/beomsu7/Fast-Planner
-    sudo gedit ~/PX4-Autopilot/platforms/posix/cmake/sitl_target.cmake
-    #set(models 부분에 custom 추가해주고, 대충 110번째 줄 정도?
-    #그러고는 ~/PX4-Autopilot/Tools/sitl_gazebo/models 에 custom 이라는 이름으로 폴더 만들고 내용물 채우면됨
-    
-    cd ~/PX4-Autopilot/Tools/sitl_gazebo/models
-    cp -r iris/ custom
-    #이제 custom 폴더에서 내용물 수정, meshes 에 필요한 stl 파일들 추가하고   
![image](https://user-images.githubusercontent.com/72853382/123041974-170ac580-d431-11eb-8452-7233370f48a6.png)   

여차저차 custom sdf 파일 만들고  
-    cd ~/PX4-Autopilot && DONT_RUN=1 make px4_sitl_default gazebo_iris_depth_camera   
이걸로 확인해보면, 음 에러가 나는군요. https://discuss.px4.io/t/create-custom-model-for-sitl/6700/4 이걸 참고했는데

