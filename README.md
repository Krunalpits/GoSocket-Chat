# GoSocket Chat 💬

A **real-time chat application** built with **Go**, **WebSockets**, and **Goroutines** — enabling multiple users to communicate instantly across rooms without page refresh.

---

## 🚀 Tech Stack

| Layer | Technology |
|---|---|
| Backend | Go (Golang) |
| Real-Time Communication | WebSockets (gorilla/websocket) |
| Concurrency | Goroutines + Channels |
| Frontend | HTML, CSS, JavaScript |
| Server | Go net/http |

---

## ⚙️ Architecture

```
Client (Browser) ←──WebSocket──→ Go Server ←──broadcast channel──→ All Clients
```

Each connected client runs **two independent goroutines**:
- **ReadPump** — listens for incoming messages from the browser
- **WritePump** — pushes outgoing messages to the browser

A central **Room goroutine** manages all connected clients using Go channels:
- `register` — adds new clients
- `unregister` — removes disconnected clients
- `broadcast` — fans out messages to all clients in the room

This architecture handles **thousands of concurrent connections** efficiently because goroutines are extremely lightweight compared to OS threads.

---

## ✨ Features

- 🔴 **Real-time messaging** — messages delivered instantly via persistent WebSocket connections
- 🏠 **Multiple chat rooms** — users can create and join named rooms
- 👥 **Multi-client support** — unlimited concurrent users per room
- ⚡ **Goroutine-based concurrency** — non-blocking, high-performance connection handling
- 🔄 **Auto-disconnect handling** — clients cleanly removed on browser close
- 🌐 **Lightweight frontend** — no frameworks, pure HTML/CSS/JS

---

## 🛠️ Getting Started

### Prerequisites
- Go 1.21+ installed → [Download Go](https://go.dev/dl/)
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/Krunalpits/GoSocket-Chat.git

# Navigate into the project
cd GoSocket-Chat

# Install dependencies
go mod tidy

# Run the server
go run .
```

Open your browser at:
```
http://localhost:8080
```

### Testing Real-Time Communication
1. Open `http://localhost:8080` in **two browser tabs**
2. Enter the **same room name** in both tabs
3. Type a message in one tab — it appears instantly in the other

---

## 📁 Project Structure

```
GoSocket-Chat/
├── main.go          # Entry point — HTTP server setup and routing
├── room.go          # Room logic — manages clients, broadcast, register/unregister
├── client.go        # Client logic — ReadPump and WritePump goroutines
├── go.mod           # Go module dependencies
├── go.sum           # Dependency checksums
├── templates/
│   ├── index.html   # Landing page — room selection
│   └── chat.html    # Chat room UI
└── static/
    ├── css/
    │   └── styles.css
    └── js/
        └── chat.js  # WebSocket client-side logic
```

---

## 🔑 Key Go Concepts Demonstrated

**Goroutines** — Each client connection spawns two goroutines (ReadPump + WritePump) that run concurrently without blocking the main thread.

**Channels** — Thread-safe communication between goroutines using Go's built-in channel primitives — no mutexes or locks needed.

**WebSocket Upgrade** — HTTP connections are upgraded to persistent WebSocket connections using the `gorilla/websocket` library.

**Hub Pattern** — Central room struct acts as a hub, coordinating all client registrations and message broadcasts through a single goroutine.

---

## 📈 Roadmap

- [ ] Deploy to AWS EC2
- [ ] Add Redis Pub/Sub for horizontal scaling across multiple servers
- [ ] User authentication with JWT
- [ ] Message persistence with PostgreSQL
- [ ] Typing indicators
- [ ] Online user count per room
- [ ] React.js frontend rewrite

---

## 👨‍💻 Author
**Krunal Pithadia**
- GitHub: [@Krunalpits](https://github.com/Krunalpits)
- LinkedIn: [linkedin.com/in/krunal-pithadia](https://linkedin.com/in/krunal-pithadia)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).