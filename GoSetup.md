go prog lang: 
0 how to unget & uninstall:
 0a. how to "unget" packs/bin after "go get uri_path"
 0b. how to "uninstall" pcaks/bin after "go install pack"
1. what gocache, goenv, gomodcache & gopath are use for
 1a. what is their def. loc. in win, msys2 and linux
2. how to check what is installed in all the paths above
3. how to uninstalled in all the data from paths above
4. how to change their location 
 4a. will simple mv of dir is good or i'll need to uninstall/rebuild/reinstall
 
 Sure! Let's address each of your questions step by step.

---

### **0. How to Unget & Uninstall Packages/Binaries**

#### **0a. Ungetting Packages/Binaries after `go get uri_path`**

In modern versions of Go (1.16 and later), the `go get` command is primarily used for managing dependencies within modules, not for installing binaries. However, in earlier versions, `go get` was used to fetch and install packages and their binaries.

To "unget" or uninstall packages and binaries fetched via `go get`, you need to manually remove them from your system:

- **Delete the Package Source Code:**
  - Navigate to your `GOPATH/src` directory.
  - Locate the package directory corresponding to the `uri_path`.
  - Delete the directory.

- **Delete the Installed Binaries:**
  - Navigate to your `GOPATH/bin` or `GOBIN` directory.
  - Remove the binary files associated with the package.

There is no built-in `go unget` command, so manual deletion is necessary.

#### **0b. Uninstalling Packages/Binaries after `go install pack`**

Similar to `go get`, `go install` compiles and installs binaries into your `GOPATH/bin` or `GOBIN` directory. To uninstall:

- **Delete the Installed Binaries:**
  - Go to your `GOBIN` or `GOPATH/bin`.
  - Remove the binary files corresponding to `pack`.

- **Delete Compiled Package Files:**
  - Navigate to `GOPATH/pkg`.
  - Remove the compiled package files associated with `pack`.

Again, uninstallation involves manual deletion since Go does not provide an uninstall command for packages.

---

### **1. What are `GOCACHE`, `GOENV`, `GOMODCACHE`, and `GOPATH` used for?**

#### **GOCACHE**

- **Purpose**: Stores compiled package files to speed up subsequent compilations. It caches the build outputs to avoid redundant work.
- **Default Location**:
  - **Windows**: `%LocalAppData%\go-build`
  - **MSYS2**: Likely uses the Windows path or `$HOME/.cache/go-build`
  - **Linux**: `$HOME/.cache/go-build`

#### **GOENV**

- **Purpose**: Holds Go environment configuration settings. It's a file that persists settings modified via `go env -w`.
- **Default Location**:
  - **Windows**: `%USERPROFILE%\go\env`
  - **MSYS2**: `$HOME/go/env`
  - **Linux**: `$HOME/.config/go/env`

#### **GOMODCACHE**

- **Purpose**: Stores downloaded Go modules when using Go modules for dependency management.
- **Default Location**:
  - **All Platforms**: By default, it's set to `$GOPATH/pkg/mod`

#### **GOPATH**

- **Purpose**: Specifies the root of your workspace. It contains:
  - `src`: Source files
  - `pkg`: Package objects
  - `bin`: Executables
- **Default Location**:
  - **Windows**: `%USERPROFILE%\go`
  - **MSYS2**: Likely `$HOME/go`
  - **Linux**: `$HOME/go`

---

### **1a. Default Locations in Windows, MSYS2, and Linux**

Here's a consolidated table for clarity:

| Variable    | Windows                         | MSYS2                      | Linux                       |
|-------------|---------------------------------|----------------------------|-----------------------------|
| GOCACHE     | `%LocalAppData%\go-build`       | `$HOME/.cache/go-build`    | `$HOME/.cache/go-build`     |
| GOENV       | `%USERPROFILE%\go\env`          | `$HOME/go/env`             | `$HOME/.config/go/env`      |
| GOMODCACHE  | `%GOPATH%\pkg\mod`              | `$GOPATH/pkg/mod`          | `$GOPATH/pkg/mod`           |
| GOPATH      | `%USERPROFILE%\go`              | `$HOME/go`                 | `$HOME/go`                  |

---

### **2. How to Check What Is Installed in All the Paths Above**

#### **GOCACHE**

- **View Cache Contents**:
  - Use the command: `go cache -debug`
  - Manually navigate to the cache directory and list files.

#### **GOENV**

- **View Environment Variables**:
  - Run: `go env`
- **View Configured Settings**:
  - Check the `go/env` file at the default location.

#### **GOMODCACHE**

- **List Installed Modules**:
  - Run: `go list -m all` within a module-enabled project.
  - Navigate to `$GOMODCACHE` or `$GOPATH/pkg/mod` and list directories.

#### **GOPATH**

- **List Installed Packages and Binaries**:
  - Packages: Check `$GOPATH/pkg`
  - Binaries: Check `$GOPATH/bin`
  - Source Code: Check `$GOPATH/src`

---

### **3. How to Uninstall All the Data from Paths Above**

#### **GOCACHE**

- **Clear Cache**:
  - Run: `go clean -cache`

#### **GOENV**

- **Reset Environment Settings**:
  - Remove specific settings: `go env -u VARIABLE_NAME`
  - Delete the `go/env` file to reset all configurations.

#### **GOMODCACHE**

- **Clear Module Cache**:
  - Run: `go clean -modcache`

#### **GOPATH**

- **Remove All Data**:
  - **Warning**: This will delete your source code, packages, and binaries.
  - Manually delete the `$GOPATH` directory.

---

### **4. How to Change Their Location**

#### **Changing `GOCACHE`**

- **Set New Location**:
  - Temporarily (current session): `export GOCACHE=/new/path` (Linux/MSYS2) or `set GOCACHE=C:\new\path` (Windows)
  - Permanently:
    - Add the environment variable to your shell profile or system environment variables.

#### **Changing `GOENV`**

- **Set New Location**:
  - Set `GOENV` to the desired file path.
  - Example: `export GOENV=/new/path/go/env`

#### **Changing `GOMODCACHE`**

- **Set New Location**:
  - Temporarily: `export GOMODCACHE=/new/path` or `set GOMODCACHE=C:\new\path`
  - Permanently:
    - Add to your shell profile or system environment variables.

#### **Changing `GOPATH`**

- **Set New Location**:
  - Temporarily: `export GOPATH=/new/path` or `set GOPATH=C:\new\path`
  - Permanently:
    - Add to your shell profile or system environment variables.

---

### **4a. Will Simply Moving the Directory Suffice, or Do I Need to Uninstall/Rebuild/Reinstall?**

- **Simply Moving Directories**:

  - **Cache Directories (`GOCACHE`, `GOMODCACHE`)**:
    - **Not Recommended**: These directories contain cached data with absolute paths.
    - **Action**: It's better to clear the caches using `go clean -cache -modcache` and let Go rebuild them at the new location.

  - **`GOPATH`**:
    - **Possible**: You can move the `GOPATH` directory to a new location.
    - **Steps**:
      1. Move the directory to the new location.
      2. Update the `GOPATH` environment variable to point to the new location.
      3. Rebuild any packages if necessary.

- **Rebuilding/Reinstalling**:

  - **Necessary When**:
    - You have binaries or packages that have hardcoded paths.
    - After moving `GOPATH`, some compiled packages may need to be recompiled.
  - **Action**:
    - Run `go install` or `go build` in your projects to rebuild binaries and packages.

---

**Note**:

- **Environment Variables**:

  - On **Windows**, set environment variables via the System Properties or using `set` in Command Prompt.
  - On **Linux/MSYS2**, use `export` in your shell profile (`~/.bashrc`, `~/.zshrc`).

- **Persistence**:

  - Setting environment variables in a terminal is temporary. To make changes permanent, update your system's environment variables or shell configuration files.

- **Backup**:

  - Before deleting or moving directories, consider backing up important data.

---

If you have further questions or need clarification on any step, feel free to ask!