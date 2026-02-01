📦 Go Minecraft Inventory Logic Engine
A high-performance, state-driven inventory system written in Go. This project focuses on clean memory management and pointer-based state manipulation to handle complex item interactions like stack merging, swapping, and splitting.

🧩 The Logic
The core architecture is built on a 1D-to-2D mapping system. While the player interacts with a visual grid, the underlying engine manages the data as a linear slice. This significantly simplifies saving player data and optimizes memory access. The system uses a Hand Buffer pattern, where the item currently held by the cursor is treated as a temporary cell. This allows for seamless "drag-and-drop" logic where items are swapped or merged between the grid and the cursor state with zero-allocation efficiency.

🛠️ Key Technical Features
Pointer-Safe Interaction: Uses direct pointers to inventory slots, ensuring that state updates (like incrementing a stack) are reflected instantly across the engine without expensive data copying.

Intelligent Stack Arithmetic: Features built-in logic for Minecraft-style interactions. Left-clicking handles full stack swaps and merges, while right-clicking performs integer division to split stacks perfectly in half.

Engine Agnostic Core: Although demonstrated using the Ebiten library, the movement logic and hit-detection rely on Go’s standard library (image.Rectangle), making the core state machine portable to any Go game framework.

Spatial Hitbox Detection: Instead of heavy physics objects, this engine uses lightweight AABB (Axis-Aligned Bounding Box) logic to map mouse coordinates to specific inventory indices in real-time.

📂 Structure & Usage
The system is organized into two primary components: the Cell, which holds the unique Item ID and quantity, and the Inventory, which acts as the controller. By decoupling the drawing logic from the update logic, the system maintains a clean "Source of Truth," preventing common bugs like item duplication or "ghost" items during rapid clicks.

```
type Cell struct {
    ItemId int      // 0 = Empty
    Amount uint     // Current stack count
    Hitbox image.Rectangle
}
```

🏃 Getting Started
Prerequisites
Go 1.18+

Ebiten v2 dependencies (standard for your OS)

Installation
Clone the repository:

git clone
`https://github.com/yourusername/go-inventory-system.git`

Run the project:
`go run main.go`

Thank You!!!
