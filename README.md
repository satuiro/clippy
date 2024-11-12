# Clippy

## Cross-Platform Clipboard Sync Project Specification

## Tech Stack

### Linux CLI Application (Rust)

- **Core**: Rust
- **Clipboard Integration**: `x11-clipboard` or `wl-clipboard` crate (for X11/Wayland)
- **P2P Networking**: `libp2p` with the following modules:
  - Noise protocol for encryption
  - Kademlia DHT for peer discovery
  - MDNS for local network discovery
  - WebRTC transport for NAT traversal
- **Serialization**: `serde` + `bincode` for efficient data transfer
- **CLI Interface**: `clap` for command line argument parsing

### Android Application (React Native)

- **Framework**: Expo React Native
- **P2P Integration**:
  - Custom native module for libp2p integration
  - React Native WebRTC for peer connections
- **State Management**: Redux Toolkit
- **Local Storage**: AsyncStorage
- **UI Components**: React Native Paper
- **Clipboard Access**: `expo-clipboard`
- **Background Tasks**: `expo-background-fetch`

### Shared Infrastructure

- **Protocol**: Custom protocol built on libp2p
- **Security**:
  - End-to-end encryption using Noise protocol
  - Public key authentication
  - Perfect forward secrecy
- **Data Format**: Protocol Buffers for message serialization

## Core Features

### 1. Device Pairing

- QR code-based device pairing
- Manual pairing code entry
- Public key exchange during pairing
- Device nickname assignment

### 2. Clipboard Sync

- Real-time clipboard content synchronization
- Support for multiple content types:
  - Plain text
  - Rich text
  - URLs
  - Images (with size limits)
- Selective sync options
- History retention (configurable)

### 3. Network Handling

- Local network discovery (MDNS)
- Internet sync via DHT and WebRTC
- Automatic reconnection
- Bandwidth optimization
- NAT traversal

### 4. Security & Privacy

- End-to-end encryption
- Device verification
- Clipboard history encryption at rest
- Option to exclude sensitive content
- Auto-clear clipboard after timeout

### 5. User Interface

- Android:

  - Material Design UI
  - Quick settings tile integration
  - Share sheet integration
  - Notification for sync status
  - Dark/light theme support

- Linux:
  - CLI commands for all operations
  - System tray integration (optional GUI)
  - Desktop notifications
  - Configuration file support

### 6. Management Features

- Device management
  - Add/remove devices
  - View connected devices
  - Device-specific permissions
- Sync history
  - View sync history
  - Clear history
  - Export history
- Network settings
  - Toggle local/internet sync
  - Bandwidth limits
  - Port configuration

## Project Structure

```
project/
├── core-protocol/          # Shared protocol definitions
│   ├── protos/            # Protocol Buffer definitions
│   └── crypto/            # Shared cryptographic utilities
│
├── linux-client/          # Rust CLI application
│   ├── src/
│   │   ├── cli/          # Command line interface
│   │   ├── clipboard/    # Clipboard integration
│   │   ├── network/      # libp2p networking
│   │   └── storage/      # Local storage
│   └── Cargo.toml
│
└── android-app/          # React Native application
    ├── src/
    │   ├── components/   # React components
    │   ├── screens/      # App screens
    │   ├── store/        # Redux store
    │   └── native/       # Native modules
    └── package.json
```

