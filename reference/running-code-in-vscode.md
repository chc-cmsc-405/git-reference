# Running Code in VS Code

This guide covers how to run C++, Java, and Go programs in Visual Studio Code.

---

## C++

### Using the Run Menu

1. Open a `.cpp` file in VS Code
2. Go to **Run > Run Without Debugging** (or press `Ctrl+F5` / `Cmd+F5`)
3. **First time only:** A menu appears asking you to select a compiler:

   | You See | Choose If |
   |---------|-----------|
   | **clang++** | You're on Mac |
   | **g++** | You're on Mac or Windows with MinGW |
   | **cl.exe** | You're on Windows with Visual Studio |

   > **Mac users:** `clang++` and `g++` are the same compiler on Mac. Pick either one.
   >
   > **Windows users:** If you installed MinGW per the setup guide, pick `g++`. If you see `cl.exe`, that's Visual Studio's compiler — it works but may have minor differences.

4. VS Code compiles and runs your program
5. Output appears in the **Debug Console** panel at the bottom

### What VS Code Creates

After your first run, VS Code creates a `.vscode/` folder with configuration files. **This is normal** — the folder is already in `.gitignore` so it won't be committed to your repository.

### Troubleshooting

**"No compiler found"**
- Make sure you completed the dev environment setup
- Mac: Run `xcode-select --install` in Terminal
- Windows: Verify MinGW is in your PATH

**Program runs but window closes immediately**
- This happens when there's no input waiting
- Add `cin.get();` at the end of main() to pause, or run from Terminal instead

---

## Java

### Using the Run Button

1. Open a `.java` file containing a `main` method
2. Look for **"Run"** text that appears above the `main` method:

   ```java
   public class Hello {
       public static void main(String[] args) {  // ← "Run | Debug" appears here
           System.out.println("Hello!");
       }
   }
   ```

3. Click **Run**
4. Output appears in the **Terminal** panel

> **Note:** The Run/Debug links are provided by the Java Extension Pack. If you don't see them, make sure the extension is installed.

### Troubleshooting

**"Run" link doesn't appear**
- Make sure the Java Extension Pack is installed
- Wait a moment — Java extension takes time to initialize on first open
- Check that your file has a valid `public static void main(String[] args)` method

**"javac: command not found"**
- Java JDK is not installed or not in PATH
- Revisit the dev environment setup guide

---

## Go

### Using the Run Link

1. Open a `.go` file containing a `main` function
2. Look for **"run"** text that appears above the `main` function:

   ```go
   package main

   func main() {  // ← "run | debug" appears here
       fmt.Println("Hello!")
   }
   ```

3. Click **run**
4. Output appears in the **Debug Console** panel

### First-Time Setup

When you first open a Go file, VS Code may prompt you to install Go tools. **Click "Install All"** — these tools provide IntelliSense, debugging, and other features.

If you see errors about missing modules, run this in the terminal:

```bash
go mod init fundamentals
```

> **Note:** The name after `go mod init` can be anything (`fundamentals`, `hello`, `myproject`). It won't affect your code for this course.

This creates a `go.mod` file that Go needs for managing dependencies.

### Important: Mixed-Language Folders

Go's build system doesn't work in folders containing other language source files (like `.cpp` or `.java`). If you're in a mixed-language folder (like the Industry Fundamentals assignment), use the terminal instead:

```bash
go run hello.go
```

Future Go assignments will have their own folders where the VS Code "run" link works normally.

### Troubleshooting

**"run" link doesn't appear**
- Make sure the Go extension is installed
- Install Go tools when prompted (or run `Go: Install/Update Tools` from Command Palette)

**"go: command not found"**

- Go is not installed or not in PATH
- Revisit the dev environment setup guide

**"go.mod file not found" or "cannot determine module path"**
- Run `go mod init fundamentals` in your project folder (the name can be anything)

---

## Quick Reference

| Language | Run Method | Shortcut |
|----------|------------|----------|
| C++ | Run > Run Without Debugging | `Ctrl+F5` / `Cmd+F5` |
| Java | Click "Run" above main() | — |
| Go | Click "run" above main() | — |

---

## Code Runner Extension (Optional)

[Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) is an optional extension that provides a simpler way to run code. It works for all three languages and always outputs to the Terminal.

### Why Use Code Runner?

| Built-in Run | Code Runner |
|--------------|-------------|
| C++ and Go output to Debug Console | Always outputs to Terminal |
| Different methods per language | Same shortcut for all languages |
| May have issues with user input | User input works reliably |

### How to Use

1. Install the Code Runner extension
2. Open any source file
3. Press `Ctrl+Alt+N` (Windows) or `Ctrl+Option+N` (Mac)
4. Output appears in Terminal

You can also click the ▶ play button in the top right corner.

### Note

Code Runner uses the same compilers you installed during setup (g++, javac, go). It's just a different way to run them — it doesn't replace the dev environment setup.

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
