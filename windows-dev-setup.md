# Windows Development Environment Setup

This guide will help you set up your development environment on Windows.

---

## Required Software

You will install the following:
1. **Visual Studio Code** (IDE for all languages)
2. **MinGW-w64** (C/C++ Compiler)
3. **Java Development Kit (OpenJDK)**
4. **Go Programming Language**
5. **Git** (for version control and GitHub)
6. **VS Code Extensions**

---

## Step 1: Install VS Code

1. Download VS Code from: https://code.visualstudio.com/
2. Run the installer
3. **Important:** Check "Add to PATH" during installation
4. Complete installation

---

## Step 2: Install MinGW-w64 (C/C++ Compiler)

**Why MinGW-w64?** Provides GCC compiler consistent with Mac/Linux environments.

1. Download from: https://winlibs.com/
   - Scroll to **Release versions** → **UCRT runtime**
   - Find the latest **GCC x.x.x (with POSIX threads)** entry
   - Click **Win64 (without LLVM/Clang/LLD/LLDB): Zip archive**

2. Extract the ZIP file:
   - Right-click the downloaded ZIP → "Extract All..."
   - Extract to: `C:\` (this creates `C:\mingw64`)
   - After extraction, verify you have `C:\mingw64\bin`, `C:\mingw64\lib`, etc.

3. **Add MinGW to Windows PATH:**
   - Open Start Menu, search "Environment Variables"
   - Click "Edit the system environment variables"
   - Click "Environment Variables" button
   - Under "System variables", find and select "Path"
   - Click "Edit"
   - Click "New"
   - Add: `C:\mingw64\bin`
   - Click "OK" on all windows

---

## Step 3: Install OpenJDK (Java)

1. Download Microsoft Build of OpenJDK 25 from:
   https://learn.microsoft.com/en-us/java/openjdk/download
   - Under **OpenJDK 25**, find **Windows x64**
   - Download the **.exe** installer
2. Run the installer
3. Follow installation wizard (use default options)
4. Installer automatically adds Java to PATH

---

## Step 4: Install Go

1. Download Go from: https://go.dev/dl/
   - Choose: **Windows installer (MSI)**
2. Run the installer
3. Follow installation wizard (use default options)
4. Installer automatically adds Go to PATH

---

## Step 5: Install Git

1. Download Git for Windows from: https://git-scm.com/download/win
2. Run the installer
3. **Important selections during installation:**
   - Default editor: Select **Visual Studio Code** (avoid Vim — it's hard to exit!)
   - Initial branch name: Select **Override** and enter **main** (matches GitHub)
   - "Git from the command line and also from 3rd-party software"
   - "Use bundled OpenSSH"
   - "Use the native Windows Secure Channel library"
   - "Checkout Windows-style, commit Unix-style line endings"
   - Use MinTTY terminal
   - Default pull behavior: Fast-forward or merge
   - Git Credential Manager: Yes
4. Complete installation

**Note:** This also installs Git Bash, which provides a Unix-like terminal on Windows. We'll use Git Bash in VS Code for consistent commands across platforms.

---

## Step 6: Install VS Code Extensions

1. Open VS Code
2. Click Extensions icon (left sidebar) or press `Ctrl+Shift+X`
3. Install these extensions (search by name, or click links to verify):
   - [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) (by Microsoft)
   - [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) (by Microsoft)
   - [Go](https://marketplace.visualstudio.com/items?itemName=golang.go) (by Go Team at Google)

**Verify extensions are installed:**

Open the VS Code integrated terminal (View menu → Terminal, or press Ctrl and the backtick key) and run:
```bash
code --list-extensions
```

Your output should include these extensions (other extensions may also be listed, which is fine):
```
golang.go
ms-vscode.cpptools
redhat.java
vscjava.vscode-gradle
vscjava.vscode-java-debug
vscjava.vscode-java-dependency
vscjava.vscode-java-pack
vscjava.vscode-java-test
vscjava.vscode-maven
```

> **Note:** The Java Extension Pack automatically installs the additional `redhat.java` and `vscjava.*` extensions.

---

## Step 7: Verify Installation

Open **Git Bash** (search for it in Start Menu) and run these commands:

```bash
gcc --version
```
Should show: `gcc.exe (GCC) 15.x.x` or similar

```bash
javac -version
```
Should show: `javac 25.x.x` or similar

```bash
go version
```
Should show: `go version go1.x.x windows/amd64` or similar

```bash
git --version
```
Should show: `git version 2.x.x` or similar

**If any command fails:** Close Git Bash completely and reopen (PATH changes require restart).

---

## Troubleshooting

### "gcc is not recognized"
- Solution: Restart Command Prompt/Terminal completely
- If still fails: Verify PATH includes `C:\mingw64\bin`

### "javac is not recognized"
- Solution: Close and reopen terminal
- If still fails: Verify Java installation in system settings

### VS Code can't find compiler
- Solution: Reload VS Code (`Ctrl+Shift+P` → "Developer: Reload Window")

### Git Bash not available in VS Code
- Solution: Open VS Code settings (File → Preferences → Settings)
- Search: "terminal integrated default profile windows"
- Select "Git Bash" from dropdown

---

## Next Steps

After completing this setup, see [GitHub Classroom Setup](github-classroom-setup.md) to configure your GitHub account and learn the assignment workflow.
