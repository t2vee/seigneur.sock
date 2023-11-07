>  
> This readme is only pesudo at the moment. Do not expect this current state to be the final implementation  
>  

# Seigneur Communication Protocol Specification

## Overview

Describes the custom binary communication protocol designed for efficient data transfer between the mekkio client and seigneur over secure websockets.  
The protocol is tailored to minimize packet size and parsing time.

## Protocol Structure

Each packet in the protocol has a structured format, beginning with a game tick and followed by a packet type identifier and the corresponding payload.

### Packet Anatomy

- **Game Tick (4 bytes):** A 32-bit integer representing the current game state's tick count.
- **Packet Type (1 byte):** A unique identifier for the type of packet being sent.
- **Payload (variable):** The data associated with the packet type, detailed below.

## Packet Types

| Packet Type | Hex Value | Description                   |
|-------------|-----------|-------------------------------|
| Move        | `0x01`    | Details player movement       |
| Player Join | `0x02`    | Indicates a player joining    |
| Player Leave| `0x03`    | Indicates a player leaving    |
| Sanity Check| `0x04`    | Performs a lobby/room check   |
| Weapon Action| `0x05`   | Details weapon actions taken  |

## Detailed Packet Structures

### Move Packet (0x01)

- **Player ID (4 bytes):** Unique identifier for the player.
- **X Coordinate (2 bytes):** The X-axis position of the player.
- **Y Coordinate (2 bytes):** The Y-axis position of the player.
- **Velocity (2 bytes):** The current velocity of the player.

### Player Join Packet (0x02)

- **Player ID (4 bytes):** Unique identifier for the player.
- **Player Name Length (1 byte):** The length of the player's name.
- **Player Name (variable):** The player's name, variable length.

### Player Leave Packet (0x03)

- **Player ID (4 bytes):** Unique identifier for the player.

### Sanity Check Packet (0x04)

- **Lobby/Room ID (4 bytes):** Identifier for the current lobby or room.
- **Player ID (4 bytes):** Unique identifier for the player.
- **Authentication Token Length (1 byte):** Length of the auth token.
- **Authentication Token (variable):** The token used for player authentication.

### Weapon Action Packet (0x05)

- **Player ID (4 bytes):** Unique identifier for the player.
- **Action Type (1 byte):** Type of weapon action (e.g., shoot, damage, ability).
- **Action Data (variable):** Details of the action, varying by type.

## Security Considerations

While the protocol is designed for efficiency, it's crucial to also consider the security aspect of the data being transmitted. Encryption or obfuscation can be employed to protect the data from being intercepted and understood by unauthorized parties.

### Main Encryption Methods

- **AES (Advanced Encryption Standard):** Utilize AES in GCM mode for a balance of speed and security, with the benefit of authentication.

### Possible Implementation

- Libraries such as `pycryptodome` for python.
- Packet batching and stateful encryption to minimize overhead.
