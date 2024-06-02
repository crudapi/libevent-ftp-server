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