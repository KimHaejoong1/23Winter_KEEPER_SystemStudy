## 과제

- CMake를 활용해서 helloworld 디렉토리 내부에 파일들을 구성해 helloworld 실행 파일 생성하기
    - cmake 참고자료
        
        [CMake Tutorial — CMake 3.28.1 Documentation](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
        
        [CMake 할때 쪼오오금 도움이 되는 문서](https://gist.github.com/luncliff/6e2d4eb7ca29a0afd5b592f72b80cb5c?permalink_comment_id=2831356)
        
    - 거의 아무 정보없이 참고자료만 가지고 과제를 내드리지만, 질문을 주셔도 좋고 구글링을 하셔도 됩니다. 최대한 해보시기 바랍니다.

## 해결

### Window (Window 11 Edu)

- 1 폴더 하나 만들어서 `main.cpp` `CMakeLists.txt` 파일을 만듭니다.
    
    ```
    C:.
    │  CMakeLists.txt
    │  main.cpp
    ```
    
    `main.cpp`
    
    ```cpp
    #include <iostream>
    
    int main() {
        std::cout << "Hello, World!" << std::endl;
        return 0;
    }
    ```
    
    `CMakeLists.txt`
    
    ```
    cmake_minimum_required(VERSION 3.10)
    project(HelloWorld)
    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED True)
    add_executable(helloworld main.cpp)
    ```
    
- 2 `build` 폴더를 만든 후 `cmake` 해줍니다
    
    ```
    $ mkdir build
    $ cd build
    ```
    
    ```
    $ cmake -G "MinGW Makefiles" ..
    -- The C compiler identification is GNU 6.3.0
    -- The CXX compiler identification is GNU 6.3.0
    -- Detecting C compiler ABI info
    -- Detecting C compiler ABI info - done
    -- Check for working C compiler: C:/MinGW/bin/gcc.exe - skipped
    -- Detecting C compile features
    -- Detecting C compile features - done
    -- Detecting CXX compiler ABI info
    -- Detecting CXX compiler ABI info - done
    -- Check for working CXX compiler: C:/MinGW/bin/c++.exe - skipped
    -- Detecting CXX compile features
    -- Detecting CXX compile features - done
    -- Configuring done (2.5s)
    -- Generating done (0.0s)
    -- Build files have been written to: C:/WORKS/KEEPER/CY_Cmake/build
    ```
    
    - ⚠️ `cmake ..` 대신 `cmake -G "MinGW Makefiles" ..` 를 쓴 이유?
        
        ```
        -- Building for: NMake Makefiles
        CMake Error at CMakeLists.txt:2 (project):
          Running
        
           'nmake' '-?'
        
          failed with:
        
           no such file or directory
        
        CMake Error: CMAKE_C_COMPILER not set, after EnableLanguage
        CMake Error: CMAKE_CXX_COMPILER not set, after EnableLanguage
        -- Configuring incomplete, errors occurred!
        ```
        
        CMake가 ‘NMake Makefiles’ 생성기를 사용하려했지만
        → NMake를 찾을 수 없다!
        
        →MinGW를 사용하고 있기 때문에 ‘MinGW Makefiles’ 생성기를 사용하도록 해줌.
        
        - `cmake -G "MinGW Makefiles" ..` 해석
            
            `cmake` : CMake 도구 호출
            
            `-G` : 생성기(Generator)를 지정할 때 사용
            
            `“MinGW Makefiles”` : 생성기 이름
            
            `..` : 현재 디렉토리의 부모 디렉토리
            
        
        C/C++ 컴파일러 설정이 완료되지 않았음!
        
- 3 `cmake —build .` 하여 실행파일 생성
    
    ```
    $ cmake --build .
    [ 50%] Building CXX object CMakeFiles/helloworld.dir/main.cpp.obj
    [100%] Linking CXX executable helloworld.exe
    [100%] Built target helloworld
    ```
    
    - `cmake —build .` 해석
        
        `cmake` : CMake 도구 호출
        
        `--build` : CMake에게 빌드 작업 수행 지시
        
        `.` : 현재 디렉토리에서
        
    
    ```
    $ helloworld.exe
    Hello, World!
    ```
    

### Linux (WLS Ubuntu 22.04.2 LTS)

- 1 ubuntu에 CMake 설치
    
    사전 패키지 설치
    
    ```
    $ sudo apt install wget
    $ sudo apt install build-essential
    $ sudo apt install openssl
    ```
    
    다운로드
    
    ```
    $ wget https://github.com/Kitware/CMake/releases/download/v3.28.1/cmake-3.28.1.tar.gz
    $ tar -cvf cmake-3.28.1.tar.gz
    ```
    
    압축 해제 및 빌드
    
    ```
    $ cd cmake-3.28.1/
    $ ./bootstrap
    $ make
    $ sudo make install
    ```
    
- 2 폴더 하나 만들어서 `main.cpp` `CMakeLists.txt` 파일을 만듭니다.
    
    ```
    C:.
    │  CMakeLists.txt
    │  main.cpp
    ```
    
    `main.cpp`
    
    ```cpp
    #include <iostream>
    
    int main() {
        std::cout << "Hello, World!" << std::endl;
        return 0;
    }
    ```
    
    `CMakeLists.txt`
    
    ```
    cmake_minimum_required(VERSION 3.10)
    project(HelloWorld)
    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED True)
    add_executable(helloworld main.cpp)
    ```
    
- 3 `build` 폴더를 만든 후 `cmake` 해줍니다
    
    ```
    $ mkdir build
    $ cd build
    ```
    
    ```
    $ cmake ..
    -- The C compiler identification is GNU 11.4.0
    -- The CXX compiler identification is GNU 11.4.0
    -- Detecting C compiler ABI info
    -- Detecting C compiler ABI info - done
    -- Check for working C compiler: /usr/bin/cc - skipped
    -- Detecting C compile features
    -- Detecting C compile features - done
    -- Detecting CXX compiler ABI info
    -- Detecting CXX compiler ABI info - done
    -- Check for working CXX compiler: /usr/bin/c++ - skipped
    -- Detecting CXX compile features
    -- Detecting CXX compile features - done
    -- Configuring done (0.9s)
    -- Generating done (0.0s)
    -- Build files have been written to: /home/hjkim2124/CY_Cmake/build
    ```
    
- 4 `cmake —build .` 하여 실행파일 생성
    
    ```
    $ cmake --build .
    [ 50%] Building CXX object CMakeFiles/helloworld.dir/main.cpp.o
    [100%] Linking CXX executable helloworld
    [100%] Built target helloworld
    ```
    
    ```
    $ ./helloworld
    Hello, World!
    ```
    

### 참고자료

`cmake -G “MinGW Makefiles” ..`

[Can't get CMAKE to compile a project](https://stackoverflow.com/questions/51274789/cant-get-cmake-to-compile-a-project/51274842#51274842)

사전 패키지
다운로드

[Ubuntu에서 CMake 설치 방법](https://mong9data.tistory.com/124)

tar.gz
압축 해제

[우분투 리눅스 tar, gz, tar.gz (tar & gzip) 압축하기 및 압축 풀기](https://starseeker711.tistory.com/161)

CMake 설치

[[개발 환경] CMake 최신 버전 설치하기](https://growingdev.blog/entry/개발-환경-CMake-최신-버전-설치하기)

CMake 설명

[CMake  총정리 및 자세한 설명](https://cho001.tistory.com/229)
