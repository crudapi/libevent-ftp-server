# libevent-ftp-server
linux libevent ftp 

# build
```bash
gcc CLibEventFtpServer.cpp -o CLibEventFtpServer -I /opt/libevent/include/ -L /opt/libevent/lib/ -levent
./CLibEventFtpServer
sudo ln -s /opt/libevent/lib/libevent.so /usr/lib64/libevent.so
sudo ln -s /opt/libevent/lib/libevent-2.1.so.7 /usr/lib64/libevent-2.1.so.7
```