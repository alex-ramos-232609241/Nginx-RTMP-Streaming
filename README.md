# NGINX-RTMP Streaming Server with HLS and Digital Channels

## Overview
This project configures a scalable and lightweight **RTMP Streaming Server** based on **NGINX** with support for **HTTP Live Streaming (HLS)**. In addition to video streaming, this setup is versatile enough to support the delivery of **digital channels** for various media purposes, including live broadcasts, pre-recorded video loops, and adaptive streaming resolutions. 

Designed to leverage **containerized technologies** (Docker), the system ensures reliability, modularity, and cross-environment deployment. This is a practical solution for streaming platforms or companies looking to deliver high-quality video and digital content with modern, efficient infrastructure.

---

## Key Features

### **1. Flexible Streaming Protocols**
- **RTMP Support**:
  - Ideal for live streaming from encoders such as OBS Studio.
- **HLS Support**:
  - Outputs HLS-compliant video for multi-platform delivery (browsers, mobile apps, etc.).

### **2. Adaptive Streaming for Quality Optimization**
- **Multiple Resolutions**: Configurations include 1080p and 720p variants, ensuring compatibility across bandwidths.
- **HLS Fragmentation**: Adjusts delivery for smoother playback by segmenting videos into small chunks.

### **3. Infrastructure Advantages for U.S. Projects**
- **Containerized Setup**: Uses **Docker Compose**, enabling seamless deployment and scalability.
- **Cloud Compatibility**: Suitable for hybrid or fully cloud environments (AWS, GCP, Azure). Networks can integrate with CDN providers.
- **Automated Media Processing**: Uses **FFmpeg** for on-the-fly transcoding and looping media.
- **Modular Architecture**: Loosely coupled services ensure individual components can scale independently.

### **4. Beyond Video Streaming**
While focused on delivering video streams, this project supports streaming any type of digital channel (e.g., audio-only streams, slideshows, pre-recorded advertisements) by configuring sources and transcoding appropriately.

---

## Project Architecture

```plaintext
Docker Network: streaming
  |
  |-- nginx-rtmp:
  |     - RTMP endpoint for live video ingestion.
  |     - HLS output served on HTTP (port 8080).
  |
  |-- ffmpeg:
        - Transcoding media and looping input files.
```

### Docker Services
#### **1. nginx-rtmp**
- **Image**: [tiangolo/nginx-rtmp](https://hub.docker.com/r/tiangolo/nginx-rtmp)
- **Ports**:
  - `1935`: RTMP ingestion.
  - `8080`: HTTP-based HLS output.
- **Mounted Volumes**: Custom `nginx.conf` for RTMP and HLS configurations.
- **Role**: Acts as the primary server for live video ingestion and HLS stream generation.

#### **2. ffmpeg**
- **Image**: [jrottenberg/ffmpeg](https://hub.docker.com/r/jrottenberg/ffmpeg)
- **Responsibilities**:
  - Handles transcoding and packaging of input files.
  - Generates streams in **FLV** format for ingestion.
- **Customization**: Can loop pre-recorded videos or serve other media types (e.g., music files or slides).

---

## Usage
### **Setup Requirements**
1. **Docker** and **Docker Compose** installed on the server.
2. A configured Docker network named `streaming`. Create it if it doesn’t exist:
   ```bash
   docker network create streaming
   ```
3. Place your input videos or media assets in `/home/<user>/nginx-rtmp-dc/video`.

### **Deployment**
1. Clone the repository:
   ```bash
   git clone https://github.com/alex-ramos-232609241/Nginx-RTMP-Streaming.git
   ```

2. Modify the `nginx.conf` or adjust paths as needed.

3. Start the services:
   ```bash
   docker-compose up -d
   ```

4. Ingest your stream via RTMP at:
   ```
   rtmp://<server-ip>:1935/live/test
   ```

5. View the HLS stream at:
   ```
   http://<server-ip>:8080/hls/1080p/index.m3u8
   ```

---

## Example Use Cases
1. **Corporate Digital Signage**:
   - Display looping promotional content or slideshows at multiple resolutions.
2. **Live Event Broadcasts**:
   - Stream live conferences, gaming events, or other live content to multiple devices.
3. **Hybrid Digital Channels**:
   - Combine audio, video, and interactive elements for educational purposes or IPTV setups.

---

## Customization
- **Adaptive Bitrate Streaming**: Add more variants to the configuration for different resolutions.
- **Alternative Input Sources**: Configure **FFmpeg** to process custom live inputs such as webcams or external video devices.
- **Scalability**: Integrate this project with CDN providers for global delivery.

---

## Contributions
Contributions are welcome! Feel free to open issues or submit pull requests to help improve this project.

---

## License
This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgments
- **Tiangolo** for the NGINX-RTMP Docker Image.
- **Jrottenberg** for the FFmpeg Docker Image.

---

## Contact
For questions or support, contact [uni.ramos.telecomun@gmail.com] or open an issue on the repository.
