# Socket Programming in C

Socket programming is a way of connecting two nodes on a network to communicate with each other. One socket(node) listens on a particular port at an IP, while the other socket reaches out to the other to form a connection. The server forms the listener socket while the client reaches out to the server.
Socket programming is widely used in instant messaging applications, binary streaming, and document collaborations, online streaming platforms, etc.

Below are three demonstrations: a Simple client/server model, a TCP-based model, and a UDP-based model.

---

## 1. Simple Client/Server Model

In this C program we are exchanging one hello message between server and client to demonstrate the client/server model.

### server.c
```c
#include <netinet/in.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>
#define PORT 8080
int main(int argc, char const* argv[])
{
    int server_fd, new_socket;
    ssize_t valread;
    struct sockaddr_in address;
    int opt = 1;
    socklen_t addrlen = sizeof(address);
    char buffer[1024] = { 0 };
    char* hello = "Hello from server";

    // Creating socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    // Forcefully attaching socket to the port 8080
    if (setsockopt(server_fd, SOL_SOCKET,
                   SO_REUSEADDR | SO_REUSEPORT, &opt,
                   sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // Forcefully attaching socket to the port 8080
    if (bind(server_fd, (struct sockaddr*)&address,
             sizeof(address))
        < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }
    if (listen(server_fd, 3) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }
    if ((new_socket
         = accept(server_fd, (struct sockaddr*)&address,
                  &addrlen))
        < 0) {
        perror("accept");
        exit(EXIT_FAILURE);
    }
  
    // subtract 1 for the null
    // terminator at the end
    valread = read(new_socket, buffer,
                   1024 - 1); 
    printf("%s\n", buffer);
    send(new_socket, hello, strlen(hello), 0);
    printf("Hello message sent\n");

    // closing the connected socket
    close(new_socket);
  
    // closing the listening socket
    close(server_fd);
    return 0;
}
```

### client.c
```c
#include <arpa/inet.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>
#define PORT 8080

int main(int argc, char const* argv[])
{
    int status, valread, client_fd;
    struct sockaddr_in serv_addr;
    char* hello = "Hello from client";
    char buffer[1024] = { 0 };
    if ((client_fd = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        printf("\n Socket creation error \n");
        return -1;
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Convert IPv4 and IPv6 addresses from text to binary
    // form
    if (inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr)
        <= 0) {
        printf(
            "\nInvalid address/ Address not supported \n");
        return -1;
    }

    if ((status
         = connect(client_fd, (struct sockaddr*)&serv_addr,
                   sizeof(serv_addr)))
        < 0) {
        printf("\nConnection Failed \n");
        return -1;
    }
  
    // subtract 1 for the null
    // terminator at the end
    send(client_fd, hello, strlen(hello), 0);
    printf("Hello message sent\n");
    valread = read(client_fd, buffer,
                   1024 - 1); 
    printf("%s\n", buffer);

    // closing the connected socket
    close(client_fd);
    return 0;
}
```

**Output:**
*(Open two terminals. Run the server first, then the client)*

**Terminal 1 (Server):**
```text
$ gcc server.c -o server
$ ./server
Hello from client
Hello message sent
```

**Terminal 2 (Client):**
```text
$ gcc client.c -o client
$ ./client
Hello message sent
Hello from server
```

---

## 2. TCP Based (TCP SERVER & TCP CLIENT)

### tcp_server.c
```c
#include <netinet/in.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define PORT 8080

int main() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    socklen_t addrlen = sizeof(address);
    char buffer[1024] = {0};
    char *message = "Hello from TCP Server";

    server_fd = socket(AF_INET, SOCK_STREAM, 0);
    setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt));

    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    bind(server_fd, (struct sockaddr *)&address, sizeof(address));
    listen(server_fd, 3);

    printf("TCP Server listening on port %d...\n", PORT);
    new_socket = accept(server_fd, (struct sockaddr *)&address, &addrlen);

    read(new_socket, buffer, 1024);
    printf("Client: %s\n", buffer);

    send(new_socket, message, strlen(message), 0);

    close(new_socket);
    close(server_fd);
    return 0;
}
```

### tcp_client.c
```c
#include <arpa/inet.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define PORT 8080

int main() {
    int sock;
    struct sockaddr_in serv_addr;
    char *message = "Hello from TCP Client";
    char buffer[1024] = {0};

    sock = socket(AF_INET, SOCK_STREAM, 0);

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);
    inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr);

    connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr));

    send(sock, message, strlen(message), 0);
    read(sock, buffer, 1024);

    printf("Server: %s\n", buffer);

    close(sock);
    return 0;
}
```

**Output:**

**Terminal 1 (Server):**
```text
$ gcc tcp_server.c -o tcp_server
$ ./tcp_server
TCP Server listening on port 8080...
Client: Hello from TCP Client
```

**Terminal 2 (Client):**
```text
$ gcc tcp_client.c -o tcp_client
$ ./tcp_client
Server: Hello from TCP Server
```

---

## 3. UDP Based (UDP SERVER & UDP CLIENT)

### udp_server.c
```c
#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define PORT 8080

int main() {
    int sockfd;
    char buffer[1024];
    char *message = "Hello from UDP Server";
    struct sockaddr_in servaddr, cliaddr;
    socklen_t len;

    sockfd = socket(AF_INET, SOCK_DGRAM, 0);

    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = INADDR_ANY;
    servaddr.sin_port = htons(PORT);

    bind(sockfd, (struct sockaddr *)&servaddr, sizeof(servaddr));

    printf("UDP Server listening on port %d...\n", PORT);
    len = sizeof(cliaddr);

    recvfrom(sockfd, buffer, 1024, 0, (struct sockaddr *)&cliaddr, &len);
    printf("Client: %s\n", buffer);

    sendto(sockfd, message, strlen(message), 0, (struct sockaddr *)&cliaddr, len);

    close(sockfd);
    return 0;
}
```

### udp_client.c
```c
#include <arpa/inet.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define PORT 8080

int main() {
    int sockfd;
    char *message = "Hello from UDP Client";
    char buffer[1024];
    struct sockaddr_in servaddr;
    socklen_t len;

    sockfd = socket(AF_INET, SOCK_DGRAM, 0);

    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(PORT);
    inet_pton(AF_INET, "127.0.0.1", &servaddr.sin_addr);

    sendto(sockfd, message, strlen(message), 0, (struct sockaddr *)&servaddr, sizeof(servaddr));

    len = sizeof(servaddr);
    recvfrom(sockfd, buffer, 1024, 0, (struct sockaddr *)&servaddr, &len);

    printf("Server: %s\n", buffer);

    close(sockfd);
    return 0;
}
```

**Output:**

**Terminal 1 (Server):**
```text
$ gcc udp_server.c -o udp_server
$ ./udp_server
UDP Server listening on port 8080...
Client: Hello from UDP Client
```

**Terminal 2 (Client):**
```text
$ gcc udp_client.c -o udp_client
$ ./udp_client
Server: Hello from UDP Server
```
