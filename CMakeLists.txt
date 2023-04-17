cmake_minimum_required(VERSION 3.17)
project(server)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY release)

add_executable(shooter_server
        # game:
        Source.cpp
        Player.cpp
        Player.h
        network/ShooterServer.cpp
        network/ShooterServer.h
        ShooterConsts.h
        network/ShooterMsgType.cpp
        network/ShooterMsgType.h
        # 3d flashflashEngine:
        flashEngine/Consts.h
        flashEngine/math/Vec4D.h
        flashEngine/math/Vec4D.cpp
        flashEngine/math/Vec3D.cpp
        flashEngine/math/Vec3D.h
        flashEngine/math/Vec2D.cpp
        flashEngine/math/Vec2D.h
        flashEngine/math/Matrix4x4.h
        flashEngine/math/Matrix4x4.cpp
        flashEngine/Triangle.h
        flashEngine/Triangle.cpp
        flashEngine/math/Plane.h
        flashEngine/math/Plane.cpp
        flashEngine/Mesh.h
        flashEngine/Mesh.cpp
        flashEngine/utils/Log.h
        flashEngine/utils/Log.cpp
        flashEngine/utils/Time.h
        flashEngine/utils/Time.cpp
        flashEngine/utils/Timer.cpp
        flashEngine/utils/Timer.h
        flashEngine/utils/ResourceManager.h
        flashEngine/utils/ResourceManager.cpp
        flashEngine/World.h
        flashEngine/World.cpp
        flashEngine/Camera.h
        flashEngine/Camera.cpp
        flashEngine/io/Screen.h
        flashEngine/io/Screen.cpp
        flashEngine/Engine.h
        flashEngine/Engine.cpp
        flashEngine/io/Keyboard.cpp
        flashEngine/io/Keyboard.h
        flashEngine/io/Mouse.cpp
        flashEngine/io/Mouse.h
        flashEngine/io/SoundController.cpp
        flashEngine/io/SoundController.h
        flashEngine/utils/ObjectController.cpp
        flashEngine/utils/ObjectController.h
        flashEngine/animation/Animation.h
        flashEngine/animation/Timeline.cpp
        flashEngine/animation/Timeline.h
        flashEngine/animation/Interpolation.h
        flashEngine/animation/Animation.cpp
        flashEngine/animation/ATranslate.h
        flashEngine/animation/AScale.h
        flashEngine/animation/ARotate.h
        flashEngine/animation/AWait.h
        flashEngine/animation/AFunction.h
        flashEngine/animation/AAttractToPoint.h
        flashEngine/animation/ARotateRelativePoint.h
        flashEngine/animation/ARotateLeft.h
        flashEngine/animation/Interpolation.cpp
        flashEngine/animation/Animations.h
        flashEngine/animation/AShowCreation.h
        flashEngine/animation/AShowUncreation.h
        flashEngine/animation/ARotateLeftUpLookAt.h
        flashEngine/animation/ADecompose.h
        flashEngine/physics/RigidBody.cpp
        flashEngine/physics/RigidBody.h
        flashEngine/physics/Simplex.h
        flashEngine/physics/HitBox.cpp
        flashEngine/physics/HitBox.h
        flashEngine/Object.cpp
        flashEngine/Object.h
        flashEngine/gui/Button.cpp
        flashEngine/gui/Button.h
        flashEngine/gui/Window.cpp
        flashEngine/gui/Window.h
        flashEngine/network/ClientUDP.cpp
        flashEngine/network/ClientUDP.h
        flashEngine/network/MsgType.cpp
        flashEngine/network/MsgType.h
        flashEngine/network/ReliableMsg.cpp
        flashEngine/network/ReliableMsg.h
        flashEngine/network/ServerUDP.cpp
        flashEngine/network/ServerUDP.h
        flashEngine/network/UDPConnection.cpp
        flashEngine/network/UDPConnection.h
        flashEngine/network/UDPSocket.cpp
        flashEngine/network/UDPSocket.h
        )

if(APPLE OR UNIX)
    include_directories(/usr/local/include)
else()
    set(SFML_DIR "C:/Libraries/SFML/lib/cmake/SFML")
    set(SFML_STATIC_LIBRARIES TRUE)
endif()

find_package(SFML 2.5.1 COMPONENTS graphics audio REQUIRED)

if (SFML_FOUND)
    include_directories(${SFML_INCLUDE_DIR})
endif()

target_link_libraries(shooter_server sfml-audio sfml-network sfml-graphics sfml-window sfml-system)

if (APPLE)
    set(GLEW_H /usr/local/Cellar/glew/2.1.0/include/GL)
    set(GLFW_H /usr/local/Cellar/glfw/3.2.1/include/GLFW)
    include_directories(${GLEW_H} ${GLFW_H})

    set(GLEW_LINK /usr/local/Cellar/glew/2.1.0/lib/libGLEW.2.1.dylib)
    set(GLFW_LINK /usr/local/Cellar/glfw/3.2.1/lib/libglfw.3.dylib)
    link_libraries(${OPENGL} ${GLEW_LINK} ${GLFW_LINK})

    target_link_libraries(${CMAKE_PROJECT_NAME} "-framework OpenGL")
    target_link_libraries(${CMAKE_PROJECT_NAME} "-framework GLUT")
elseif(UNIX)
    find_package(OpenGL REQUIRED)
    find_package(GLUT REQUIRED)

    target_link_libraries(${CMAKE_PROJECT_NAME} ${OPENGL_LIBRARIES})
    target_link_libraries(${CMAKE_PROJECT_NAME} ${GLUT_LIBRARY})
endif()