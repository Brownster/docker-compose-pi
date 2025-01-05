# Docker Compose for Media Services

This repository provides a comprehensive Docker Compose configuration to deploy a suite of media-related applications. The stack includes services for managing movies, TV shows, music, audiobooks, and podcasts, along with utilities for downloading, transcoding, and streaming.

## Services Included

### VPN
- **Image:** `${VPN_IMAGE}`
- **Purpose:** Securely route all traffic through a VPN.
- **Key Features:** Supports Private Internet Access (PIA), environment file configuration.

### Jackett
- **Image:** `${JACKETT_IMAGE}`
- **Purpose:** Indexer proxy for torrent and Usenet.
- **Volumes:**
  - `${DOCKER_DIR}/${JACKETT_CONTAINER}:/config`
  - `${DOWNLOADS}:/downloads`

### Sonarr
- **Image:** `${SONARR_IMAGE}`
- **Purpose:** TV series management and automation.
- **Volumes:**
  - `${DOCKER_DIR}/${SONARR_CONTAINER}:/config`
  - `${STORAGE_MOUNT}/${TVSHOWS_FOLDER}:/tv`
  - `${DOWNLOADS}/incomplete:/downloads/incomplete`
  - `${DOWNLOADS}/complete:/downloads/complete`

### Radarr
- **Image:** `${RADARR_IMAGE}`
- **Purpose:** Movie management and automation.
- **Volumes:**
  - `${DOCKER_DIR}/${RADARR_CONTAINER}:/config`
  - `${STORAGE_MOUNT}/${MOVIES_FOLDER}:/movies`
  - `${DOWNLOADS}/incomplete:/downloads/incomplete`
  - `${DOWNLOADS}/complete:/downloads/complete`

### Lidarr
- **Image:** `${LIDARR_IMAGE}`
- **Purpose:** Music management and automation.
- **Volumes:**
  - `${DOCKER_DIR}/${LIDARR_CONTAINER}:/config`
  - `${STORAGE_MOUNT}/${MUSIC_FOLDER}:/music`
  - `${DOWNLOADS}/incomplete:/downloads/incomplete`
  - `${DOWNLOADS}/complete:/downloads/complete`

### Airsonic
- **Image:** `${AIRSONIC_IMAGE}`
- **Purpose:** Music streaming server.
- **Volumes:**
  - `${DOCKER_DIR}/${AIRSONIC_CONTAINER}:/config`
  - `${STORAGE_MOUNT}/${MUSIC_FOLDER}:/music`
  - `${STORAGE_MOUNT}/${PODCAST_FOLDER}:/podcasts`
  - `${STORAGE_MOUNT}/${PLAYLIST_FOLDER}:/playlists`

### Audiobookshelf
- **Image:** `ghcr.io/advplyr/audiobookshelf`
- **Purpose:** Audiobook and podcast management and streaming.
- **Volumes:**
  - `${STORAGE_MOUNT}/audiobooks:/audiobooks`
  - `${STORAGE_MOUNT}/${PODCAST_FOLDER}:/podcasts`
  - `${DOCKER_DIR}/audiobookshelf:/config`
  - `${DOCKER_DIR}/audiobookshelf/metadata:/metadata`

### Transmission
- **Image:** `${TRANSMISSION_IMAGE}`
- **Purpose:** Torrent client.
- **Volumes:**
  - `${DOCKER_DIR}/${TRANSMISSION_CONTAINER}:/config`
  - `${DOWNLOADS}:/downloads`

### NZBGet
- **Image:** `${NZBGET_IMAGE}`
- **Purpose:** Usenet downloader.
- **Volumes:**
  - `${DOCKER_DIR}/${NZBGET_CONTAINER}:/config`
  - `${DOWNLOADS}/incomplete:/incomplete`
  - `${DOWNLOADS}/complete:/complete`

### Jellyfin
- **Image:** `${JELLYFIN_IMAGE}`
- **Purpose:** Media server for movies, TV, and music.
- **Volumes:**
  - `${DOCKER_DIR}/${JELLYFIN_CONTAINER}:/config`
  - `${STORAGE_MOUNT}:/media`

### Watchtower
- **Image:** `${WATCHTOWER_IMAGE}`
- **Purpose:** Automatic container updates.
- **Volumes:**
  - `/var/run/docker.sock:/var/run/docker.sock`

### RDTClient
- **Image:** `rogerfar/rdtclient`
- **Purpose:** RealDebrid torrent downloader.
- **Volumes:**
  - `${DOCKER_DIR}/rdtclient:/data/db`
  - `${DOWNLOADS}:/data/downloads`

### Get IPlayer
- **Image:** `${GET_IPLAYER_IMAGE}`
- **Purpose:** Download BBC iPlayer content.
- **Volumes:**
  - `${DOCKER_DIR}/${GET_IPLAYER}/config:/config`
  - `${DOWNLOADS}/complete:/downloads`

## Prerequisites
1. **Docker** and **Docker Compose** must be installed on your system.
2. Update the `.env` file with appropriate paths and environment variables.

## Environment Variables
- `PUID` and `PGID`: User and group IDs for file permissions.
- `TIMEZONE`: System timezone (e.g., `Europe/London`).
- Paths for media storage, downloads, and configurations.

## Usage
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```
2. Update the `.env` file with your specific configurations.
3. Start the stack:
   ```bash
   docker-compose up -d
   ```
4. Access the services via their respective ports defined in the `.env` file.

## Folder Structure
Ensure the following folder structure is maintained:
- `/mnt/storage/Movies` for movies
- `/mnt/storage/TVShows` for TV shows
- `/mnt/storage/Music` for music
- `/mnt/storage/Audiobooks` for audiobooks
- `/mnt/storage/Podcasts` for podcasts
- `/mnt/storage/Playlists` for playlists
- `/mnt/storage/downloads/incomplete` for incomplete downloads
- `/mnt/storage/downloads/complete` for completed downloads

## Support
For issues or enhancements, please create an issue in the repository.

