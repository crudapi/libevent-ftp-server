# libevent-ftp-server
linux libevent ftp 

# build
```bash
sudo ldconfig
rm -rf ./CLibEventFtpServer
gcc CLibEventFtpServer.cpp -o CLibEventFtpServer -I /usr/local/include/ -L /usr/local/lib/ -levent
./CLibEventFtpServer
sudo ln -s /usr/local/libevent.so /usr/lib64/libevent.so
sudo ln -s /usr/local/libevent-2.1.so.7 /usr/lib64/libevent-2.1.so.7
sudo ln -s /usr/local/libevent-2.1.so.7.0.1 /usr/lib64/libevent-2.1.so.7.0.1
```

# code
```cpp
#include <sys/types.h>
#include <event2/event-config.h>
#include <stdio.h>
#include <event.h>

struct event ev;
struct timeval tv;

void time_cb(int fd, short event, void *argc)
{
	printf("timer wakeup!\n");
	event_add(&ev, &tv);
}

int main()
{
	printf("main!\n");
	struct event_base* base = event_init();
	tv.tv_sec = 2;
	tv.tv_usec = 0;

	evtimer_set(&ev, time_cb, NULL);
	event_base_set(base, &ev);
	event_add(&ev, &tv);
	event_base_dispatch(base);

	return 0;
}
```


# CMakeList.txt: CLibEventFtpServer 的 CMake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
cmake_minimum_required (VERSION 3.8)

# 如果支持，请为 MSVC 编译器启用热重载。
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("CLibEventFtpServer")

set(libevent_home "/usr/local")
include_directories(${libevent_home}/include)
link_directories(${libevent_home}/lib)
file(GLOB libevent_libs ${libevent_home}/lib/*.*)


# 将源代码添加到此项目的可执行文件。
add_executable (CLibEventFtpServer "CLibEventFtpServer.cpp" )

target_link_libraries(CLibEventFtpServer ${libevent_libs})


if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET CLibEventFtpServer PROPERTY CXX_STANDARD 20)
endif()a

# TODO: 如有需要，请添加测试并安装目标。
