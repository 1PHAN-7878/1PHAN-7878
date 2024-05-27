---
title: udp网络编程
date: 2024-05-27 17:25:31
tags: python
---

# 工具

网络调试助手

![image-20240527172642085](../images/image-20240527172642085.png)

![image-20240527172655990](../images/image-20240527172655990.png)

![image-20240527172703489](../images/image-20240527172703489.png)

![image-20240527172710179](../images/image-20240527172710179.png)

# 创建

```python
# 创建一个 TCP socket 
import socket 
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) 
s.close() 
```

```python
# 创建一个 UDP socket 
import socket 
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
s.close(
```

# 流程图

![image-20240527172844891](../images/image-20240527172844891.png)

# 基本使用

```python
import socket 
def main(): 
 # 创建一个 UDP 套接字
 udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
 # 使用套接字收发数据
 # sendto(发送的数据，接收方的 IP 和 PORT) 
 udp_socket.sendto(b"hello world",("192.168.0.104",8080)) 
 # 关闭套接字
 udp_socket.close() 
if __name__ == '__main__': 
 main() 
```

```python
import socket 
def main(): 
 # 创建一个 UDP 套接字
 udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
 # 准备接收方的地址
 dest_addr = ("192.168.0.104",8080) 
 # 从键盘获取数据
 send_data = input("请输入要发送的数据：") 
 # 使用套接字收发数据
 udp_socket.sendto(send_data.encode("utf-8"),dest_addr) 
 # 关闭套接字
 udp_socket.close() 
if __name__ == '__main__': 
 main() 
```

```python
import socket 
def main(): 
 # 创建一个 UDP 套接字
 udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
 # 准备接收方的地址
 dest_addr = ("192.168.0.104",8080) 
 while True: 
 # 从键盘获取数据
 send_data = input("请输入要发送的数据：") 
 if send_data == "exit": 
 break 
 # 使用套接字收发数据
 udp_socket.sendto(send_data.encode("utf-8"),dest_addr) 
 # 关闭套接字
 udp_socket.close() 
if __name__ == '__main__': 
 main() 

```

客户端

```python
import socket 
def main(): 
 # 创建一个 udp 套接字
 udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
 # 绑定一个本地地址
 localaddr = ("",5555) 
 udp_socket.bind(localaddr) 
 # 接收数据
 recv_data = udp_socket.recvfrom(1024) 
 # recv_data 这个变量中存储的是一个元组（接收到的数据，（发送方的 IP，Port）)
 recv_msg = recv_data[0] 
 send_addr = recv_data[1] 
 # 打印接收到的数据
 print("接收到由{}发送来的数据：{}。".format(str(send_addr),recv_msg.decode("utf-8"))) 
 # 关闭套接字
 udp_socket.close() 
if __name__ == "__main__": 
 main() 
```

简单聊天器

```python
import socket 
def send_msg(u_socket,dest_ip,dest_port): 
 # 获取要发送的内容
 send_data = input("请输入要发送的内容：") 
 # 发送数据
 u_socket.sendto(send_data.encode("utf-8"),(dest_ip,dest_port)) 
def recv_msg(u_socket): 
 # 接收并显示数据
 recv_data = u_socket.recvfrom(1024) 
 # recv_data 这个变量中存储的是一个元组（接收到的数据，（发送方的 IP，
Port））
 recv_msg = recv_data[0] 
 send_addr = recv_data[1] 
 # 打印接收到的数据
 print("接收到由{}发送来的数据：{}。".format(str(send_addr),recv_msg.decode("utf8"))) 
def main(): 
 # 创建一个 udp 套接字
 udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) 
 # 绑定地址信息
 udp_socket.bind(("",5555)) 
 dest_ip = input("请输入对方的 IP：") 
 dest_port = int(input("请输入对方的 PORT：")) 
 # 利用 while 循环来发送和接收
 while True: 
 # 发送数据
 send_msg(udp_socket,dest_ip,dest_port) 
 # 接收数据
 recv_msg(udp_socket) 
 # 关闭套接字
 udp_socket.close() 
if __name__ == "__main__": 
 main() 

```

# 练习

![image-20240527173247222](../images/image-20240527173247222.png)

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

s.bind(('127.0.0.1', 11541))

while True:
    print("test:\n")
    data, addr = s.recvfrom(1024)
    data = data.decode("utf-8")
    if data == 'exit':
        break

    print("大写之后是", data.upper(), '\n')
s.close()
```

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

while True:
    addr = ('127.0.0.1', 11451)
    msg = input("give me a message:")
    s.sendto(msg.encode("utf-8"), addr)
    if msg == 'exit':
        break

s.close()
```

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

addr = ('127.0.0.1', 19198)
s.bind(addr)

print(f"Starting up on localhost port {addr[1]} Waiting to receive message")

recv, addrRecv = s.recvfrom(1024)

print(f"Received a message(size is {len(recv)}) from ", addrRecv)
print(recv.decode("utf-8"))
s.sendto(recv, addrRecv)
print(f"Sent a message(size is {len(recv)}) to ", addrRecv)

```

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

addr = ("127.0.0.1", 19198)
msg = "this is a test message"
s.sendto(msg.encode("utf-8"), addr)
print(f"{msg} is sent to {addr}, waiting for response")

recv , msg = s.recvfrom(1024)
print(f"{msg} is received from {addr}")
```

