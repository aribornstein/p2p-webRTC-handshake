# p2p-webRTC-handshake

This project demonstrates a serverless WebRTC chat application. It allows two peers to establish a direct, peer-to-peer connection and exchange messages without the need for a central server, except for initial signaling using URL parameters.

## Features

- **Serverless Communication:** Establishes a direct peer-to-peer connection using WebRTC.
- **SDP Compression:** Compresses the Session Description Protocol (SDP) data to make it URL-friendly using `pako` library.
- **URL-Based Signaling:** Uses URL parameters to exchange offer and answer SDPs between peers.
- **ICE Server Configuration:** Utilizes Google's public STUN server for NAT traversal.
- **Data Channel:** Establishes a data channel for sending and receiving text messages.
- **Shareable URL:** Generates a shareable URL that can be sent to the other peer to initiate the connection.

- **Local Storage:** Temporarily stores offer and answer SDPs in local storage to handle connection establishment across different tabs or browser instances.
- **Copy URL Button:** Provides a button to easily copy the generated shareable URL to the clipboard.
- **Send with Whats App Button:** Sends a shareable URL to someone over what'sapp that can be sent to the other peer to initiate the connection.
- **Clear Storage Button:** Provides a button to clear local storage.

## How it Works

1. **Initiator:** The first peer (initiator) opens the `rtc_test.html` page. The application generates an offer SDP, compresses it, and creates a shareable URL with the offer as a query parameter.
2. **Signaling:** The initiator shares the generated URL with the second peer (retriever).
3. **Retriever:** The retriever opens the shared URL. The application extracts the offer from the URL, generates an answer SDP, compresses it, and updates the shareable URL with the answer as a query parameter.
4. **Response:** The retriever sends the updated URL back to the initiator (e.g. by copying and pasting). The initiator opens the URL, which stores the answer in local storage.
5. **Connection Establishment:** The initiator retrieves the answer from local storage and sets it as the remote description. The WebRTC connection is established, and the peers can start exchanging messages.

## Usage

1. Open `rtc_test.html` in a web browser.
2. Share the generated URL with the other peer.
3. Once the other peer opens the URL, they will generate another URL that they need to share back.
4. After both peers have exchanged URLs, a direct connection will be established, and you can start sending messages.

## Technologies Used

- HTML
- JavaScript
- WebRTC API
- `pako` (for SDP compression)

## Libraries

- [pako](https://cdnjs.com/libraries/pako) - JavaScript compression library used to compress SDP offers and answers.

## STUN Server

- `stun:stun.l.google.com:19302` - Google's public STUN server used for NAT traversal.

## Notes

- This is a basic implementation and may require further enhancements for production use, such as a more robust signaling mechanism or security.
- The peers must have a way to exchange URLs (e.g., chat, whatsapp, email, or any other messaging platform).
- The application relies on browser support for WebRTC and the `pako` library.
