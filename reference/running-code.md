# Running Code in VS Code

This guide covers how to run C++, Java, and Go programs in Visual Studio Code.

---

## Recommended: Code Runner Extension

[Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) is the recommended way to run code in this course. It provides a consistent experience across all three languages.

### Why Code Runner?

| Feature | Code Runner | Built-in Methods |
|---------|-------------|------------------|
| User input (`cin`, `Scanner`, etc.) | ✅ Works (with setting below) | ⚠️ May not work |
| Consistent across languages | ✅ Same shortcut for all | ❌ Different per language |
| Output location | Terminal | Varies (Debug Console, Terminal) |

### Setup (Required)

1. **Install the extension:** Search for "Code Runner" in the Extensions panel and install it

2. **Enable "Run in Terminal"** — this setting is required for user input to work:
   - Open VS Code Settings (`Ctrl+,` or `Cmd+,`)
   - Search for `code-runner.runInTerminal`
   - Check the box for **"Code-runner: Run In Terminal"**

   Or add this to your `settings.json`:
   ```json
   "code-runner.runInTerminal": true
   ```

> **Why is this required?** By default, Code Runner outputs to VS Code's Output panel, which is **read-only**. Programs that need user input (like `cin` in C++ or `Scanner` in Java) will hang waiting for input that can never be entered. The "Run in Terminal" setting sends output to the Integrated Terminal, which accepts input.

### How to Run Code

- **Keyboard:** `Ctrl+Alt+N` (Windows) or `Ctrl+Option+N` (Mac)
- **Button:** Click the ▶ play button in the top right corner
- **Menu:** Right-click in the editor → "Run Code"

Output and input appear in the **Terminal** panel at the bottom.

### Note

Code Runner uses the same compilers you installed during setup (g++, javac, go). It's just a convenient way to run them — it doesn't replace the dev environment setup.

---

## Alternative: Manual Terminal Commands

If you prefer not to use Code Runner, you can always run code manually in the Integrated Terminal. This approach always supports user input.

Open the Terminal panel (`Ctrl+`` ` or `Cmd+`` `) and use these commands:

### C++

```bash
# Compile and run (two steps)
g++ myfile.cpp -o myfile
./myfile          # Mac/Linux
myfile.exe        # Windows

# Or compile and run in one line
g++ myfile.cpp -o myfile && ./myfile
```

### Java

```bash
# Compile and run (two steps)
javac MyFile.java
java MyFile

# Or compile and run in one line
javac MyFile.java && java MyFile
```

### Go

```bash
go run myfile.go
```

---

## Alternative: Built-in Run Methods

VS Code has built-in ways to run code, but they have limitations with user input. These methods are documented here for reference, but Code Runner is recommended.

### C++: Run Menu

1. Open a `.cpp` file
2. Go to **Run > Run Without Debugging** (`Ctrl+F5` / `Cmd+F5`)
3. First time: Select your compiler (g++, clang++, or cl.exe)
4. Output appears in **Debug Console** — user input may not work

### Java: Run Link

1. Open a `.java` file with a `main` method
2. Click **"Run"** that appears above `main`
3. Output appears in **Terminal** — user input works here

### Go: Run Link

1. Open a `.go` file with a `main` function
2. Click **"run"** that appears above `main`
3. Output appears in **Debug Console** — user input may not work

---

## Troubleshooting

### Code Runner Issues

**Nothing happens when I run**
- Make sure Code Runner extension is installed
- Check that you have the compiler installed (g++, javac, go)

**Program hangs waiting for input**
- Enable "Run in Terminal" setting (see Setup above)
- This is the most common issue — the Output panel cannot accept input

**Wrong compiler or command**
- Code Runner auto-detects based on file extension
- For C++, it uses `g++` by default; this works on Mac, Linux, and Windows with MinGW

### Compiler Issues

**"g++ not found" / "javac not found" / "go not found"**
- The compiler is not installed or not in your PATH
- Revisit the dev environment setup guide for your platform

**C++: "No compiler found" in Run menu**
- Mac: Run `xcode-select --install` in Terminal
- Windows: Verify MinGW is in your PATH

### Go-Specific Issues

**"go.mod file not found"**
- Run `go mod init myproject` in your folder (the name can be anything)

**Code won't run in mixed-language folders**
- Go's build system doesn't work alongside `.cpp` or `.java` files
- Use `go run myfile.go` in the terminal instead

---

## Files You Can Ignore

VS Code and compilers create various files that are **automatically ignored** by `.gitignore`:

| Files | What They Are |
|-------|---------------|
| `.vscode/` | VS Code configuration (tasks, settings) |
| `*.o`, `*.obj` | Compiled object files |
| `*.exe` | Windows executables |
| `*.dSYM/` | Mac debug symbols |
| `*.pdb`, `*.ilk` | Windows debug files |

You don't need to delete these — they won't be committed to your repository.
