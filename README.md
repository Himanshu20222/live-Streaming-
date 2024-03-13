# live-Streaming-
live streaming same WIFI network
Here's a breakdown of the two code snippets, including their purpose and interaction:

**Server Code (`pi.py`)**

**Purpose:**
* Establishes a server that captures video from a USB camera and streams the video frames to a connected client.

**Key Actions:**

1. **Socket Setup:** Creates a socket, binds it to the host's IP address and a specific port (9999 in this example).
2. **Listens for Connections:** Listens for incoming connections and accepts a client connection.
3. **Camera Initialization:** Attempts to open a USB camera using the `open_camera` function.
4. **Frame Streaming (If camera opens successfully):**
   * Reads frames from the camera.
   * Serializes each frame using `pickle.dumps`.
   * Packs the frame size with `struct.pack` to indicate the size of the incoming data.
   * Sends the frame size followed by the serialized frame data to the client.
5. **Display Window (Optional):** Shows the video feed locally with `cv2.imshow`.
6. **Error Handling:** Handles potential camera opening errors, broken client connections, and frame read errors.

**Client Code**

**Purpose:**
* Connects to the video streaming server and displays the received video frames.

**Key Actions:**

1. **Socket Connection:** Establishes a socket connection to the server's IP address and port.
2. **Frame Reception:** Enters a loop to continuously receive video frames:
   * Receives the packed frame size using `struct.unpack` to determine the amount of data to expect.
   * Receives the serialized frame data in chunks.
   * Unpickles the frame data using `pickle.loads`.
3. **Display Window:** Displays the received video frame with `cv2.imshow`.

**Interaction**

1. **Server Execution:** You would run the server code (`pi.py`) on your Raspberry Pi (or another computer) that has a camera connected.
2. **Client Execution:** You would then run the client code on the device where you want to view the video stream. **Make sure to replace `server_ip` with the actual IP address of the Raspberry Pi running the server.**
3. **Connection:** The client establishes a connection to the server.
4. **Streaming:** The server captures video frames, serializes them, and transmits them over the socket connection.  The client receives, deserializes, and displays the frames, creating the video stream.


