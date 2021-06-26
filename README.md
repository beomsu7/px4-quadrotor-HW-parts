# px4-quadrotor-HW-parts
storage for 3d printing parts of px4 quadrotor equipped with D435 and T265

-----------------------------------------------------
-----------------------------------------------------
# setting custom vehicle model for px4 sitl gazebo   
this is how to add new custom quadrotor visual stuff for px4 sitl gazebo   
the default quadrotor's model is iris and my process is just changing the visual part   
every actual parts including motor plugin, gps, etc  is same with px4-autopilot's origin

- git clone https://github.com/beomsu7/px4-quadrotor-HW-parts
- cd px4-quadrotor-HW-parts/
- cp -r custom_f450/ ~/PX4-Autopilot/Tools/sitl_gazebo/models/
- cp 1026_custom_f450 ~/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes/
- gedit ~/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes/CMakeLists.txt 
- // add '1026_custom_f450' in px4_add_romfs_files   
![image](https://user-images.githubusercontent.com/72853382/123205978-c7420200-d4f5-11eb-9d3c-18efe1396352.png)
- gedit ~/PX4-Autopilot/platforms/posix/cmake/sitl_target.cmake
- // add 'custom_f450' in set(models   
![image](https://user-images.githubusercontent.com/72853382/123206638-002ea680-d4f7-11eb-8a03-abc48138b966.png)   
- cd ~/PX4-Autopilot/ && make px4_sitl gazebo_custom_f450   
![image](https://user-images.githubusercontent.com/72853382/123206971-91058200-d4f7-11eb-8d8a-859c902a251b.png)
   
now you can use custom vehicle model
![image](https://user-images.githubusercontent.com/72853382/123207148-e346a300-d4f7-11eb-86e4-7b97f5d3f328.png)

-----------------------------------------------------
-----------------------------------------------------
# setting custom vehicle model for rviz  
- git clone https://github.com/beomsu7/px4-quadrotor-HW-parts
- cd px4-quadrotor-HW-parts/
- cp -r f450 ~/catkin_ws/src
- cd ~/catkin_ws && catkin build f450 && source devel/setup.bash   
now all propellers are cw shape... haha   
![image](https://user-images.githubusercontent.com/72853382/123208424-01150780-d4fa-11eb-82a1-3314e1448d2d.png)
   
final result is   
![image](https://user-images.githubusercontent.com/72853382/123212355-a54d7d00-d4ff-11eb-8314-1678fed25efa.png)

-----------------------------------------------------
-----------------------------------------------------
![image](https://user-images.githubusercontent.com/72853382/123514543-80f3cb00-d6ce-11eb-8b98-13b37c2ffd8e.png)

-----------------------------------------------------
------------------------------------------------------
# private notes for quick writing i gonna use my own language   
*목적 : gazebo 와 rviz 에서 이쁜 모델로 쥬얼라이즈 하기 위해서 커스텀 sitl 모델 생성 에 대한 기록 및 정리용   
   
(1) 솔리드 웍스를 이용하여 3d 모델을 생성하였다. 이때 thingiverse 에서 f450모델을 다운 받은후   
몇몇 부분 수정과 추가를 통해 만들었다.   
(2) https://ola-page.tistory.com/3 를 참고하여 urdf 파일 생성, 결과물은 'drone_without_realsense.zip' 이다.   
(3) 알비즈에서 실행하여 보니 이러한 모양   
![image](https://user-images.githubusercontent.com/72853382/123039706-972f2c00-d42d-11eb-804f-7304ecf6fdc3.png)   
(4) 가지보에서 보니 걍 흰색으로 나옴 그래서 https://answers.ros.org/question/51961/no-color-when-i-open-a-part-exported-from-solidworks-in-gazebo/
의 answer을 참고하여 gazebo reference 를 추가하지 색생이 잘나옴   
색상은 http://wiki.ros.org/simulator_gazebo/Tutorials/ListOfMaterials 리스트에서 보고 적당히 고름   
![image](https://user-images.githubusercontent.com/72853382/123039873-ce054200-d42d-11eb-8221-0bb0a05545d3.png)
   
      
(5) 기본적인 준비는 끝났으니 이제 px4의 iris.sdf를 기반으로 바꿔주려한다. 참고 https://discuss.px4.io/t/create-custom-model-for-sitl/6700   
-    cd ~/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes
-    cp 101_iris_rtps 1025_custom_f450
-    gedit CMakeLists.txt
-    #여기서 1025_custom_f450 추가해줍시다
-    sudo gedit ~/PX4-Autopilot/platforms/posix/cmake/sitl_target.cmake
-    #set(models 부분에 'custom_f450' 추가해주고, 대충 110번째 줄 정도?
-    #그러고는 ~/PX4-Autopilot/Tools/sitl_gazebo/models 에 custom 이라는 이름으로 폴더 만들고 내용물 채우면됨
-    
-    cd ~/PX4-Autopilot/Tools/sitl_gazebo/models
-    cp -r iris/ custom_f450
-    #이제 custom 폴더에서 내용물 수정, meshes 에 필요한 stl 파일들 추가하고   
-    #위와 같이 만들어도 되나 시간이 없다면 해당 깃허브의 custom_f450.zip 압축 해제

여차저차 custom sdf 파일 만들고   
음 stl 로 하니까 가제보 실행했을떄 줌에 문제가 생김   
https://discuss.px4.io/t/cant-zoom-in-gazebo/20996/6 여기서 해결   
이리저리 sdf 만들었고, 리얼센스 카메라 2개를 붙여주자
   
프로펠러의 경우 곡면이 이쁘게 만들기 어려우므로 그냥 iris 의 프로펠러를 사용한다만 색만 바꿔서  
![image](https://user-images.githubusercontent.com/72853382/123189111-2ee95480-d4d8-11eb-9a54-bc1ec40fbe1c.png)   
이런 이상한 2d 프로펠러보다는 기존 제공되는 이쁜 iris 프로펠러 쓰는게 마음이 편할거 같다   
다만 iris 프로펠러 ccw 방향의 경우 중심점이 안맞아서   
![image](https://user-images.githubusercontent.com/72853382/123187885-ffd1e380-d4d5-11eb-90d7-128c84605dfe.png)   

블렌더를 이용하여 중심점을 맞추어주고, 결과적으로 sdf 파일을 완성하였다.   
   
![image](https://user-images.githubusercontent.com/72853382/123188267-b3d36e80-d4d6-11eb-97e6-f546984452f6.png)

