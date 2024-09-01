# Qt Chat Application based on TCP/IP protocol

### ServerManager

```ServerManager``` manages the chat server, handling new connections and routing messages between clients. Its primary role is to start the server and monitor incoming connections. When a client connects to the server, ```ServerManager``` creates a ```QTcpSocket``` object representing the connection and passes it to the ```MainWindow::newClientConnected()``` slot, where a corresponding ```ClientChatWidget``` interface element is created for each client. This class is also responsible for routing messages between clients, receiving messages from one client and distributing them to others. 

### ClientManager

```ClientManager``` handles the client's connection to the server, as well as the processing and sending messages from the client. ```ClientManager``` is responsible for establishing a connection to the server through the ```connectToServer()``` method and disconnecting it via ```disconnectFromHost()```. Incoming data is processed in the ```readyRead()``` slot, which reads the data from the socket and passes it to the ```ChatProtocol``` object for further processing. Additionally, this class is integrated with the user interface through signals and slots, providing UI updates when the client's name changes or new messages are received.

### ChatProtocol

```ChatProtocol``` defines the messaging protocol between a client and a server in the chat application. Its primary role is to simplify and standardize communication, ensuring consistent data transfer over the network. The class uses enumerations for different message types (```MessageType```), which makes it easy to identify and handle various kinds of data. ```ChatProtocol``` serves as a bridge between clients and the server, providing correct encoding and decoding of messages, allowing all the clients to send messages seamlessly.

### Interaction

Interaction between ```ServerManager``` and ```ClientManager``` is structured so that each new client receives a unique instance of ```ClientManager```, which manages its connection and communication with the server. Messages sent by clients through ```ClientManager``` are transmitted to the server, where ```ServerManager``` processes them and forwards them to other clients. This setup ensures coordination of all interactions on the server, maintains communication between all chat clients, and handles the forwarding of messages. Together, ```ServerManager``` and ```ClientManager``` create an architecture that efficiently manages a multi-user chat, providing user-friendly communication between clients.
