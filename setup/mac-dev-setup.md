# Mac Development Environment Setup

This guide will help you set up your development environment on macOS.

---

## Required Software

You will install the following:
1. **Visual Studio Code** (IDE for all languages)
2. **Xcode Command Line Tools** (C/C++ Compiler)
3. **Java Development Kit (OpenJDK)**
4. **Go Programming Language**
5. **Git** (included with Xcode tools)
6. **VS Code Extensions**

---

## Step 1: Install VS Code

1. Download VS Code from: https://code.visualstudio.com/
2. Open the downloaded `.zip` file
3. Drag "Visual Studio Code.app" to Applications folder
4. Open VS Code from Applications

---

## Step 2: Install Xcode Command Line Tools (C/C++ Compiler)

1. Open **Terminal** (Applications → Utilities → Terminal)
2. Run this command:
   ```bash
   xcode-select --install
   ```
3. A dialog will appear asking to install developer tools
4. Click "Install"
5. Accept the license agreement
6. Wait for installation to complete (5-10 minutes)

> **Already installed?** If you see "Command line tools are already installed" — you're all set, skip to Step 3.

---

## Step 3: Install OpenJDK (Java)

> **Prefer Homebrew?** See the [Optional: Homebrew Setup](#optional-homebrew-setup) section at the end of this guide.

1. Download Microsoft Build of OpenJDK 25 from:
   https://learn.microsoft.com/en-us/java/openjdk/download
   - Choose: **JDK 25 (LTS) - macOS .pkg**
2. Open the downloaded `.pkg` file
3. Follow installation wizard
4. Installer automatically configures Java

---

## Step 4: Install Go

> **Prefer Homebrew?** See the [Optional: Homebrew Setup](#optional-homebrew-setup) section at the end of this guide.

1. Download Go from: https://go.dev/dl/
   - Choose: **macOS installer (.pkg)**
2. Open the downloaded `.pkg` file
3. Follow installation wizard (use default options)
4. Installer automatically adds Go to PATH

---

## Step 5: Verify Git Installation

Mac includes Git with Xcode Command Line Tools. Verify by running:

```bash
git --version
```

If Git is not installed, the easiest way is to complete Step 2 (Xcode Command Line Tools), which includes Git.

---

## Step 6: Install VS Code Extensions

1. Open VS Code
2. Click Extensions icon (left sidebar) or press `Cmd+Shift+X`
3. Install these extensions (search by name, or click links to verify):
   - [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) (by Microsoft)
   - [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) (by Microsoft)
   - [Go](https://marketplace.visualstudio.com/items?itemName=golang.go) (by Go Team at Google)

**Verify extensions are installed:**

First, enable the `code` command (one-time setup):
- Open Command Palette: `Cmd+Shift+P`
- Type "Shell Command: Install 'code' command in PATH" and press Enter

Then in VS Code terminal (View menu → Terminal), run:
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

Open **Terminal** and run these commands:

```bash
gcc --version
```
Should show: `Apple clang version 15.x.x` or similar

```bash
javac -version
```
Should show: `javac 21.x.x` or similar

```bash
go version
```
Should show: `go version go1.x.x darwin/amd64` or `darwin/arm64`

```bash
git --version
```
Should show: `git version 2.x.x` or similar

---

## Troubleshooting

### "xcode-select: command not found"
- Solution: Update macOS to latest version first

### "javac: command not found"
- Solution: Close and reopen terminal
- If still fails: Verify Java installation in System Settings → Java

### VS Code can't find compiler
- Solution: Reload VS Code (`Cmd+Shift+P` → "Developer: Reload Window")

---

## Next Steps

After completing this setup, see [GitHub Classroom Reference](../reference/github-classroom-reference.md) to learn the assignment workflow.

---

# Optional: Homebrew Setup

For students who prefer a command-line workflow, [Homebrew](https://brew.sh) is the standard Mac package manager. It simplifies installing and updating development tools.

## Install Homebrew

Open Terminal and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the prompts. After installation, follow any instructions shown to add Homebrew to your PATH.

## Install Dev Tools with Homebrew

Once Homebrew is installed, you can install the development tools with simple commands:

```bash
brew install openjdk@25
brew install go
brew install git  # optional - Xcode tools already includes git
```

For Java, create the system symlink so VS Code can find it:

```bash
sudo ln -sfn /opt/homebrew/opt/openjdk@25/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-25.jdk
```

**Note:** The C/C++ compiler still comes from Xcode Command Line Tools (`xcode-select --install`). Homebrew's gcc is available but not required for this course.

## Updating Tools

To update all Homebrew-installed tools:

```bash
brew update && brew upgrade
```

## Why Use Homebrew?

- Single commands to install tools
- Easy updates across all tools
- Common in professional development environments
- Useful beyond this course for other development needs
