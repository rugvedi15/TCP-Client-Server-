
# Distributed File System

## Project Overview
This project implements a **Distributed File System** using socket programming. It allows multiple clients to upload and retrieve files of different types (`.c`, `.pdf`, and `.txt`) by interacting with a centralized server (`Smain`). The file types are managed and stored on different servers (`Spdf` for `.pdf` files and `Stext` for `.txt` files), though this is abstracted away from the clients.

## Features
- **Multiple Client Support:** The system handles multiple client connections simultaneously.
- **Distributed File Storage:**
  - `.c` files are stored locally in **Smain**.
  - `.pdf` files are transferred and stored in **Spdf**.
  - `.txt` files are transferred and stored in **Stext**.
- **Transparent File Management:** Clients interact only with **Smain**, and are unaware of file transfers to the other servers.
- **Socket-based Communication:** All servers and clients communicate using sockets.
- **Robust Error Handling:** Error messages are displayed for invalid inputs, file paths, and commands.

## System Components
### Smain (Main Server)
- Handles all client communications.
- Manages `.c` files locally and delegates `.pdf` and `.txt` files to the respective servers.
- Forks child processes to manage each client session concurrently via the `prcclient()` function.

### Spdf (PDF Server)
- Receives and manages `.pdf` files sent from **Smain**.

### Stext (Text Server)
- Receives and manages `.txt` files sent from **Smain**.

### Client (client24s)
- Clients connect to **Smain** to upload, download, delete files, or display a list of files in directories.
- Clients are unaware of **Spdf** and **Stext** servers, only interacting with **Smain**.

## Commands Supported by the Client
1. **`ufile filename destination_path`**
   - Uploads a file to the destination path on **Smain**.
   - `.c` files are stored on **Smain**; `.txt` and `.pdf` files are transferred to **Stext** and **Spdf**, respectively.
   
2. **`dfile filename`**
   - Downloads a file from **Smain**. If the file is `.txt` or `.pdf`, it retrieves the file from **Stext** or **Spdf**.
   
3. **`rmfile filename`**
   - Deletes a file from **Smain**. If the file is `.txt` or `.pdf`, it deletes the file from **Stext** or **Spdf** as appropriate.

4. **`dtar filetype`**
   - Creates a tar file of all files of the specified type (`.c`, `.txt`, `.pdf`) and downloads it.

5. **`display pathname`**
   - Displays a consolidated list of `.c`, `.txt`, and `.pdf` files in the specified directory path.

## File Structure
The project consists of the following source code files:
- **Smain.c**: Implements the logic for handling client requests and distributing files.
- **Spdf.c**: Manages `.pdf` file storage and communication with **Smain**.
- **Stext.c**: Manages `.txt` file storage and communication with **Smain**.
- **client24s.c**: Implements the client-side logic to send commands and handle responses from **Smain**.

## Error Handling
The system handles errors such as:
- Invalid file paths or commands.
- Missing directories (creates new ones if they don't exist).
- Unsupported file types.

