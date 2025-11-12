# EmergencyService
## Overview
This project implements an **Emergency Service Platform**, a distributed system that enables users to subscribe to and report events on specific emergency channels such as **fire**, **medical**, **police**, and **natural disasters**.

The goal of this project is to simulate real-time communication between users using the **STOMP protocol (Simple Text-Oriented Messaging Protocol)**.  
It consists of two main components:
-  **Server (Java)** – provides centralized message routing and supports two concurrency models:
  - **Thread-Per-Client (TPC)**
  - **Reactor (non-blocking, event-driven model)**
- **Client (C++)** – allows users to connect to the STOMP server, subscribe to topics, send emergency reports, and receive live updates.

---

## Project Structure
```
SPL3/
├── server/           # Java server project (Maven-based)
│   └── pom.xml
├── client/           # C++ client project (Makefile-based)
│   └── makefile
└── README.md
```

---

## Requirements

### For the Server
- **Java JDK 8+**
- **Apache Maven**

### For the Client
- **g++** with C++11 or later  
- **GNU Make**
- **Boost libraries** (`libboost_system`, `libboost_filesystem`)  
- **pthread** (for multithreading)

### Example installation (on Ubuntu/Debian):
```bash
sudo apt update
sudo apt install openjdk-8-jdk maven build-essential libboost-all-dev
```

---

## Build Instructions

### Server (Java)

1. Navigate to the server directory:
```bash
cd SPL3/server
```

2. Compile the project using Maven:
```bash
mvn compile
```

3. Run the server in one of the following modes:

#### Thread-Per-Client mode
Example server for the “NewsFeed” demo:
```bash
java -cp target/classes bgu.spl.net.impl.newsfeed.NewsFeedServerMain
```

#### Reactor mode (STOMP server)
```bash
java -cp target/classes bgu.spl.net.impl.stomp.StompServer <port> <protocol>
```
Example:
```bash
java -cp target/classes bgu.spl.net.impl.stomp.StompServer 7777 stomp
```

> 📝 Note: Each implementation (`NewsFeedServerMain`, `EchoServer`, `StompServer`) demonstrates different server behaviors for learning purposes.

---

### Client (C++)

1. Navigate to the client directory:
```bash
cd SPL3/client
```

2. Build the client using the Makefile:
```bash
make
```

3. After a successful build, you will find the executables in:
```
client/bin/
```

4. Run the client:
```bash
./bin/StompClient
```

or (for echo example):
```bash
./bin/echoClient
```

> The client connects to the STOMP server, subscribes to topics, and interacts with the system in real time.  
> Input commands follow the STOMP protocol structure.

---

## Common Commands Summary

| Task | Command |
|------|----------|
| Compile Java server | `cd server && mvn compile` |
| Run Java server (TPC mode) | `java -cp target/classes bgu.spl.net.impl.newsfeed.NewsFeedServerMain` |
| Run Java server (Reactor mode) | `java -cp target/classes bgu.spl.net.impl.stomp.StompServer 7777 stomp` |
| Build C++ client | `cd client && make` |
| Run client | `./bin/StompClient` |

---

## Technologies & Concepts
- Java multithreading (`Thread-Per-Client` model)
- Reactor design pattern (non-blocking I/O)
- STOMP protocol for text-based messaging
- Client-server architecture
- C++ networking and Boost libraries

---

## Notes
This project was developed as part of a university networking assignment.  
It demonstrates both **low-level concurrency management** and **protocol-based message exchange** in distributed systems.

---

## Example Usage Flow
1. Run the Java STOMP server on port `7777`.  
2. Start several C++ clients and connect to the same port.  
3. Each client can:
   - Subscribe to emergency channels (e.g., `/topic/fire`)
   - Send reports (e.g., `/send /topic/fire`)
   - Receive live notifications from other users


