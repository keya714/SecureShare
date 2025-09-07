# SecureShare

SecureShare is a collaborative real-time text sharing web application that allows one user to edit text while multiple others can view the updates live. It is built using Node.js with Express for the server and Socket.IO for real-time bidirectional communication.

## Features

- Real-time collaborative text sharing with one active editor and multiple viewers.
- Automatic role assignment based on client IP address and predefined IP ranges:
  - Clients within certain IP ranges are assigned as editors.
  - Clients outside these ranges are assigned as viewers.
- Live updates pushed to all connected clients via WebSockets.
- Basic IP range check and encoding/decoding logic for text handling.
- Serves different HTML pages based on the number of connected clients:
  - First client gets a form page to presumably setup or become editor.
  - Subsequent clients get the main text-sharing interface.

## Installation and Setup

1. Clone the repository.
2. Install dependencies via npm:

npm install

3. Run the server:

node server.js

4. By default, the app runs on [http://localhost:3000](http://localhost:3000).

## How It Works

- The server serves static files from the `private` directory and HTML pages from the `public` directory.
- When a client connects:
  - The client's IP address is checked against predefined IP ranges.
  - Based on this check, clients are automatically grouped into editors or viewers.
  - Localhost IPs (`::1` or `::ffff:127.0.0.1`) are assigned as editors by default.
- The editor can update the shared text, which is broadcast in real time to all viewers.
- Clients see live lists of connected editors and viewers.
- Text updates include an offset value used for decoding text on the client side.

## Dependencies

- [Express](https://expressjs.com/) - Web framework for Node.js
- [Socket.IO](https://socket.io/) - Real-time WebSocket communication

## File Structure

- `server.js` - Main server code handling HTTP and WebSocket.
- `public/` - Public HTML and frontend files for users.
- `private/` - Static assets served privately (not detailed here).

## Notes

- IP range checking and text decoding functionality are included but may require additional context or frontend code to be fully operational.
- The current implementation assumes a single editor based on localhost IP; this can be extended for more complex roles.
- Ensure your environment allows local network connections for full functionality.
