- User agents, Mail servers, Simple Mail Transfer Protocols
- User Agent: (the software that lets you read and write emails)
	- mail reader
	- composing, editing, reading mail messages
- Mail Servers
	- mail box contains incoming messages for user
	- message queue of outgoing mail messages
	- use SMTP **between** mail servers for sending email messages
		- client: sending mail server
		- server: receiving mail server
- **SMTP:** 
	- protocol for exchanging email messages
	- deliver/storage of email messages to receivers server
- **IMAP:** 
	- internet mail access protocol
	- messages stored on server
	- provides retrieval, deletion, folders of stored messages on server
	- emails are left on the server until the user deletes them
- **HTTP:** 
	- gmail, hotmail, yahoo provides web based interface on top of SMTP (to send), IMAP to retrieve email messages
- **POP**:
	- uses TCP to retrieve email from a remote server on port 110
	- encrypted communication is done via SSL on TCP port 995
	- supports download and delete on the server
	- you can leave email on the server (like IMAP)
- How does transmission work?
	- uses TCP to reliably transfer email messages from client to server
	- direct transfer
	- 3 phases
		- handshaking
		- transfer of messages
		- closure
- Steps
	- 1) User writes in UA to compose email message to some email address
	- 2) UA sends message to her mail server, message placed in message queue
	- 3) client mail server opens TCP connection with receiving mail server
	- 4) SMTP sends the message over connection
	- 5) message is placed in receiver's mail box
	- 6) recipient uses UA to see the message


### Compare  HTTP with SMTP

| Feature / Behavior           | HTTP                                         | SMTP                                            |
| ---------------------------- | -------------------------------------------- | ----------------------------------------------- |
| Communication Model          | Pull                                         | Push                                            |
| Command/Response Interaction | ASCII command/response, status codes         | ASCII command/response, status codes            |
| Message Structure            | Each object encapsulated in its own response | Multiple objects sent in multipart message      |
| Connection Type              | Typically non-persistent (unless keep-alive) | Persistent connections                          |
| Encoding Requirement         | Supports various encodings                   | Requires message (header & body) in 7-bit ASCII |
| End of Message Determination | Content-Length or chunked transfer encoding  | CRLF.CRLF sequence                              |

### Compare IMAP with POP3

| Feature                              | **POP3**                                               | **IMAP**                                                   |
|--------------------------------------|---------------------------------------------------------|-------------------------------------------------------------|
| Message Storage                      | Downloads to client (can delete or keep)                | Stored on server                                            |
| Access from Multiple Devices         | Difficult (no sync between clients)                     | Easy (syncs across devices)                                |
| State Preservation                   | Stateless across sessions                               | Maintains state across sessions (folders, read/unread)     |
| Email Re-read After Client Change    | Not possible if deleted from server                     | Always possible since emails remain on server              |
| Folder Support                       | Not supported                                           | Allows multiple folders/mailboxes                          |
| Concurrent Access                    | Not designed for multiple clients                       | Supports multiple clients accessing concurrently           |
| Server-Side Search                   | Not supported                                           | Supported                                                  |
| Partial Download                     | Not supported                                           | Can download just headers (useful for mobile devices)      |
| Protocol Port                        | Uses port 110                                           | Uses port 143 (or 993 with TLS)                            |
| Current Version                      | Typically POP3                                          | IMAP version 4 (RFC 9051)                                  |

#### MIME 
- supplementary protocol that allows non ASCII data to be sent through SMTP
- Non ASCII -> MIME -> SMTP <--ASCII --> SMTP -> MIME -> Non ASCII
- NOT a mail protocol, cannot replace SMTP