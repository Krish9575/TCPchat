# Basic Chat Application

This basic chat application provides a foundation for understanding socket programming and simple client-server communication in a multi-user environment.

## Technologies Used

- **Socket Programming:** The application uses Python's socket module for network communication. Sockets provide a standard mechanism for processes on different devices to communicate over a network.

- **Threading:** Threading is employed to handle multiple clients concurrently. Each client is managed in a separate thread, allowing the server to communicate with multiple clients simultaneously.

## Working

### Server:

1. The server is created and bound to a specific host and port (127.0.0.1:55555).
2. It continuously listens for incoming connections using the `socket.listen()` method.
3. When a new client connects, the server prompts the client for an alias and adds both the client socket and alias to separate lists (clients and aliases).
4. A new thread is started for each connected client using `threading.Thread`. This thread runs the `handle_client` function for that specific client.
5. The `handle_client` function continuously listens for messages from the client and broadcasts them to all other connected clients. If an exception occurs (indicating a client disconnect), it removes the client from the lists and broadcasts a departure message.

### Client:

1. The client is created with a socket, and it connects to the server at the specified address (127.0.0.1:55555).
2. The user is prompted to choose an alias, which is sent to the server.
3. The client has two threads: one for receiving messages (`client_receive`) and another for sending messages (`client_send`).
4. The receiving thread continuously listens for messages from the server. If the server requests an alias, it sends the chosen alias; otherwise, it prints the received message.
5. The sending thread continuously prompts the user for input and sends messages to the server.

## Additional Information

- **Broadcasting:** The server uses a broadcast function to send messages to all connected clients. This ensures that when one client sends a message, all other clients receive it.

- **Error Handling:** Basic error handling is implemented to handle exceptions during message reception on both the client and server sides. In a production environment, more robust error handling mechanisms would be advisable.

- **Thread Safety:** The use of separate threads for each client allows the server to handle multiple clients simultaneously. This is essential for scalability in a chat application where multiple users may connect at the same time.

- **Local Testing:** The application is set up for local testing (127.0.0.1), and the port 55555 is used for communication. In a real-world scenario, you would replace this with the actual server IP and port.
