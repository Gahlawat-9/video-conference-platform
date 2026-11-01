# Video Conferencing Platform

A real-time, browser-based video calling app. Two people join a room and talk over peer-to-peer video with chat, screen sharing and microphone controls, with nothing to install.

## Features

- Two-participant rooms: share a room link and the second person joins instantly
- Peer-to-peer audio and video using WebRTC
- In-call text chat
- Screen sharing
- Microphone mute / unmute

## Tech stack

| Layer | Tools |
| --- | --- |
| Frontend | React.js |
| Backend / signalling | Node.js, Socket.io |
| Real-time media | WebRTC (peer-to-peer) |

## How it works

Media flows directly between the two browsers over WebRTC, so the server never handles video. The server only helps the two peers find each other:

1. A user creates or joins a room, and the client opens a Socket.io connection.
2. When the second participant joins, the server tells both peers to start a connection.
3. The peers exchange an **offer**, an **answer** and **ICE candidates** through the Socket.io signalling channel.
4. Once the connection is established, audio and video stream directly between the browsers.
5. Chat messages and mic state are sent over the same real-time channel.

## Getting started

### Prerequisites

- Node.js 18 or later
- npm
- A modern browser (Chrome, Edge, Firefox or Safari) with camera and microphone access

### Run locally

```bash
# 1. Clone the repository
git clone [repo-url]
cd [repo-folder]

# 2. Start the server
cd server
npm install
npm start

# 3. Start the client (in a second terminal)
cd client
npm install
npm start
```

Open `http://localhost:3000` in two browser windows (or on two devices on the same network), create a room in one and join it from the other.

### Environment variables

| Variable | Description | Example |
| --- | --- | --- |
| `PORT` | Port for the signalling server | `5000` |
| `CLIENT_URL` | Allowed client origin for CORS | `http://localhost:3000` |


## Testing

Tested manually with 6+ concurrent users across 25+ call sessions, checking that connections establish reliably and streams stay stable during chat and screen sharing.

## Limitations

- Rooms support two participants (one-to-one calls only)
- Peer-to-peer connections can fail on some restrictive networks without a TURN relay [confirm and edit to match your setup]

## Roadmap

- [ ] Support more than two participants
- [ ] Add a TURN server for reliable connections behind strict firewalls
- [ ] Add automated tests for the signalling flow

## Author

**Priyanshi Gahlawat**
