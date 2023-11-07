# Map Data Format Specification

## Overview

Outlines the map data format for mekkio. The format is designed to be detailed for client-side rendering and efficient for server-side game logic processing.

## Map Data Definitions

### Tile Types

- **Tile**: The fundamental unit of the map's layout.
  - `id`: A unique identifier for the tile type.
  - `type`: A string identifier for the type, e.g., "stone".
  - `properties`: A collection of properties and behaviors associated with the tile.

### Tile Properties

- **Sprite**: The path to the tile image in the tileset.
- **Collidable**: A boolean indicating if the tile is an obstacle.
- **Friction**: A float representing the friction coefficient of the tile.
- **EmitsLight**: A boolean indicating if the tile emits light.

### Layers

- Organize the map into multiple layers, such as background, foreground, and collision layers.

### Objects

- Define interactive or significant objects within the map, like items and NPCs.

### Regions

- Segment the map into larger chunks for dynamic loading and memory management.

## Client-Side Map Format

```json
{
  "tileSize": "The size of each tile in pixels",
  "tileTypes": {
    "Type identifier": {
      "sprite": "Path to the sprite image",
      "collidable": "Boolean for collision detection",
      "friction": "Friction coefficient for physics calculations",
      "emitsLight": "Boolean for light emission"
    },
    // ... additional tile types ...
  },
  "layers": [
    {
      "name": "Layer name, e.g., 'Background'",
      "tiles": "2D array representing the map layout with type identifiers"
    },
    // ... additional layers ...
  ],
  "objects": [
    {
      "type": "Object type, e.g., 'health_pack'",
      "position": {
        "x": "X-coordinate of the object",
        "y": "Y-coordinate of the object"
      }
    },
    // ... additional objects ...
  ],
  "regions": [
    {
      "id": "Region identifier",
      "startX": "Starting X-coordinate of the region",
      "startY": "Starting Y-coordinate of the region",
      "width": "Width of the region in tiles",
      "height": "Height of the region in tiles"
    },
    // ... additional regions ...
  ]
}
```
### Server-Side Map Format

The server-side format is a simplified version focusing on game logic such as collision detection and event processing.
- Collision Layer: Represented as a grid where each cell is either passable or an obstacle.
- Objects: Listed with their types and coordinates for quick reference during gameplay.
  
```
Region 1:
CCCCC
C...C
C...C
CCCCC

Objects:
<Item> at (2,1)
```
