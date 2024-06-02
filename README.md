# libevent-ftp-server
linux libevent ftp 

# build
```bash
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