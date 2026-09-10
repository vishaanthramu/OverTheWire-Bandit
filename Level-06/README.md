# 🏴 Bandit Level 5 → Level 6

<!-- 📸 SCREENSHOT: add the Level 5 → Level 6 challenge page screenshot here -->


After logging into Bandit Level 5 as `bandit5`, I read the goal for this level: the password for the next level is stored in a file somewhere under the `inhere` directory and has **all** of the following properties:

- human-readable
- `1033` bytes in size
- not executable

## 📂 Step 1 — Look Inside the `inhere` Directory

```bash
ls inhere
```

The output showed a lot of directories:

```text
maybehere00  maybehere01  maybehere02  ...  maybehere19
```

Each `maybehere` directory has several files inside it, including hidden ones. Checking all of them by hand would take a long time, so I needed a way to **search** for the file.

---

## 🔍 Step 2 — Search Using `find`

I used the `find` command with the properties from the level goal:

```bash
find inhere -type f -size 1033c ! -executable
```

### 🔎 What is `find`?

`find` searches through a directory (and all directories inside it) for files that match certain conditions.

In this command:

- `find` → the search command.
- `inhere` → where to start searching.
- `-type f` → only look for regular **files** (not directories).
- `-size 1033c` → the file must be exactly **1033 bytes**. The `c` means bytes (without it, `find` counts in 512-byte blocks).
- `! -executable` → the file must **not** be executable. `!` means "NOT".

The output showed only one file:

```text
inhere/maybehere07/.file2
```

It is a hidden file (it starts with `.`), so `ls` alone would not have shown it.

> 💡 To double-check that it is human-readable, I can run `file inhere/maybehere07/.file2`. It shows `ASCII text`.

---

## 📖 Step 3 — Read the File

```bash
cat inhere/maybehere07/.file2
```

The command displayed the contents of the file, which was the password for the next level. The file is padded with a lot of blank space, which is why it is 1033 bytes even though the password is short.

---

## 🔑 Step 4 — Copy the Password for Level 6

After running:

```bash
cat inhere/maybehere07/.file2
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit6` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 6

Now that I have the password for the next level, I need to log in as `bandit6`.

The username changes from:

```text
bandit5
```

to:

```text
bandit6
```

The command is:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from `.file2` and press **Enter**.

If the password is correct, I am logged into **Bandit Level 6**.

---

## 🔄 Level 5 → Level 6 Process

```text
Already logged in as bandit5
        ↓
ls inhere
        ↓
Too many directories to check by hand
        ↓
find inhere -type f -size 1033c ! -executable
        ↓
Found inhere/maybehere07/.file2
        ↓
cat inhere/maybehere07/.file2
        ↓
Copy the password
        ↓
SSH as bandit6
        ↓
Enter the password
        ↓
Level 6
```

## 🧠 What I Learned

- `find` searches through directories and all their subdirectories.
- `-type f` limits the search to files.
- `-size 1033c` matches an exact size in bytes (`c` = bytes).
- `! -executable` means "not executable". `!` flips a condition.
- Combining several conditions in `find` narrows the results down to just the file I need.

## 🎓 Key Takeaway

The important command I learned in Level 5 → Level 6 was:

```bash
find inhere -type f -size 1033c ! -executable
```

When I know the properties of a file but not where it is, `find` can locate it for me.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 5 to Level 6**.

👉 [Level 6 → Level 7](../Level-07/README.md)
