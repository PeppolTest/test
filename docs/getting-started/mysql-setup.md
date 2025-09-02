# MySQL Setup

This guide explains how to install MySQL on macOS and how to start up a MySQL instance.  
It is tailored for Apple Silicon (M1/M2) but works similarly on Intel-based Macs.

---

## 1. Install Homebrew

[Homebrew](https://brew.sh/) is a package manager for macOS and Linux. We’ll use it to install MySQL.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
after the installation, add Homebrew to your `PATH`:

```bash
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
You can then check if Homebrew is installed correctly:
```bash
brew help
```

---

## 2. Install MySQL via Homebrew
[MySQL instalation tutorial](https://sqlpad.io/tutorial/mysql-install-mac/)

Run:
```bash
brew install mysql
```
Which does the following things:

1. MySQL is installed in the Brew directory, e.g.: `/opt/homebrew/Cellar/mysql/8.0.33_3/bin/mysql`
2. By default, MySQL __does not set a root password__.

To then secure it:
```bash
mysql_secure_installation
```

After the installation, there are two ways to run MySQL:

### Option A: run as background service (recommended)

* This starts MySQL automatically and restarts it after reboot:
```bash
brew services start mysql
```

* To stop it:
```bash
brew services stop mysql
```

* To restart it:
```bash
brew services restart mysql
```

### Option B: run manually (foreground mode)

If you don’t need MySQL running in the background:
```bash
/opt/homebrew/opt/mysql/bin/mysqld_safe --datadir=/opt/homebrew/var/mysql

```
This keeps MySQL running only until you close the terminal.




!!! Keypoints
    * MySQL has been installed at `/opt/homebrew/Cellar/mysql/<version>`.  
    (You normally don’t use this path directly — Homebrew symlinks binaries into `/opt/homebrew/bin`.)  
    * **`brew cleanup`**: Homebrew automatically removes old MySQL versions to save space. If you want to keep older versions, set:  
    ```bash
    export HOMEBREW_NO_INSTALL_CLEANUP=1
    ```
    * **Hints (`HOMEBREW_NO_ENV_HINTS`)**:  
    Homebrew sometimes shows extra help messages.  
    If you want to hide them, set:  
    ```bash
    export HOMEBREW_NO_ENV_HINTS=1
    ```

---





















---

### Code Blocks in Content Tabs

=== "Python"

    ```py
    def main():
        print("Hello world!")

    if __name__ == "__main__":
        main()
    ```

=== "JavaScript"

    ```js
    function main() {
        console.log("Hello world!");
    }

    main();
    ```

---

```js title="code-examples.md" linenums="1" hl_lines="2-4"
// Function to concatenate two strings
function concatenateStrings(str1, str2) {
  return str1 + str2;
}

// Example usage
const result = concatenateStrings("Hello, ", "World!");
console.log("The concatenated string is:", result);
```
