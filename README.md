# MiniXecutor v1

A lightweight custom Roblox executor environment built in Lua, featuring extended APIs, local system bridging, and drawing utilities.

---

## ⚠️ Disclaimer

This project is intended for **educational and research purposes only**.

* Do **not** use in environments where it violates terms of service.
* The project includes **local system access**, including file operations and clipboard interaction.
* Use only in controlled environments and at your own risk.

---

## 🚀 Features

### 🧠 Executor-like Environment

* Custom global environment (`getgenv`)
* Synapse/KRNL-like API replication
* Closure detection (`iscclosure`, `islclosure`, `isourclosure`)
* Thread identity detection

---

### 🌐 HTTP System

* Custom `request` implementation using `HttpService`
* Built-in `httpget` with caching
* JSON encoding/decoding

---

### 🔗 Lua ↔ Python Bridge

* Local Flask server (`localhost:8000`)
* Communication via JSON + Base64
* Enables extended capabilities beyond Roblox sandbox

---

### 📁 File System API

Access local files through bridge:

* `writefile(path, content)`
* `readfile(path)`
* `makefolder(path)`
* `listfiles(path)`
* `delfile(path)`
* `delfolder(path)`
* `isfile(path)`
* `isfolder(path)`

📂 Files are stored in:

```
~/Downloads/MoreUNC/workspace/
```

---

### 📋 Clipboard Access

* `setclipboard(text)`

---

### 🎮 Input Simulation

Simulate user input:

#### Keyboard

* `keypress(keycode)`
* `keyrelease(keycode)`

#### Mouse

* `mouse1click()`, `mouse2click()`
* `mousemoveabs(x, y)`
* `mousemoverel(x, y)`

---

### 🎨 Drawing API

Create UI overlays (ESP-style rendering):

```lua
local line = Drawing.new("Line")
line.From = Vector2.new(0, 0)
line.To = Vector2.new(100, 100)
```

Supported types:

* `Line`
* `Square`
* `Circle`
* `Text`

---

### 🔐 Cryptography Utilities

* Base64 encode/decode
* Hashing via external library

```lua
crypt.base64_encode("hello")
crypt.hash("text", "sha256")
```

---

### 🧬 Sandbox System

* Wraps `game`, `workspace`, and `script`
* Prevents direct unsafe access
* Custom environment injection

---

### 🔍 Debug Utilities

* Enhanced `debug.getinfo`
* Script introspection
* `decompile` support (external API)

---

### 🧩 Instance Utilities

* `getinstances()`
* `getnilinstances()`
* `getscripts()`
* `getscripthash()`

---

## 🛠️ Requirements

* Python 3 installed and accessible via CLI
* Required Python packages:

  ```bash
  pip install flask psutil pyperclip itsdangerous
  ```

---

## ⚙️ How It Works

1. Lua script initializes environment
2. Python server is written and executed locally
3. Bridge connects via HTTP (`localhost:8000`)
4. Lua communicates with Python for:

   * File system access
   * Clipboard
   * Asset handling

---

## 📡 Bridge Endpoints

### `/files`

Handles:

* create
* read
* delete
* list
* check

### `/functions`

Handles:

* `getcustomasset`
* `setclipboard`

---

## 🔒 Security Notes

* The bridge has **full access to local files in workspace directory**
* Clipboard access is unrestricted
* HTTP communication is local but unencrypted
* No authentication is implemented

⚠️ Do not expose port `8000` externally.

---

## 🧪 Example Usage

```lua
writefile("test.txt", "Hello from Lua!")
print(readfile("test.txt"))

setclipboard("Copied from MoreUNC")

local txt = Drawing.new("Text")
txt.Text = "Hello"
txt.Position = Vector2.new(100, 100)
```

---

## 📌 Known Limitations

* No WebSocket support (polling used instead)
* Depends on local Python environment
* Limited sandbox security
* Some APIs rely on external services

---

## 📜 License

This project is provided as-is for educational purposes. No warranty is given.

---

## 👤 Author

Me

---
