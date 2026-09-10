# 🏴 Bandit Level 1 → Level 2

<!-- 📸 SCREENSHOT: add the Level 1 → Level 2 challenge page screenshot here -->


After logging into Bandit Level 1 as `bandit1`, I read the goal for this level: the password for the next level is stored in a file called **`-`** located in the home directory.

## 📋 Step 1 — List the Files

I started by checking what files are in the home directory:

```bash
ls
```

The output showed:

```text
-
```

So the file I need is literally named `-` (a single dash).

---

## ❌ Step 2 — Try Reading It Normally

My first try was the same command I used in the last level:

```bash
cat -
```

Nothing was printed. The terminal just sat there waiting.

### 🔎 Why doesn't `cat -` work?

In Linux, many commands treat `-` as a special name that means **standard input (stdin)**, which is basically "read from the keyboard".

So instead of opening the file named `-`, `cat` was waiting for me to type something.

To get out of it, I pressed **Ctrl + C**.

---

## 📖 Step 3 — Read the File Using `./-`

To tell `cat` that `-` is a file and not stdin, I gave it a path to the file:

```bash
cat ./-
```

### 🔎 What does `./` mean?

- `.` → the current directory.
- `/` → separates directories and file names in a path.
- `./-` → "the file named `-` inside the current directory".

Because the argument now starts with `./`, `cat` treats it as a normal file path instead of the special `-`.

> 💡 Using the full path works too: `cat /home/bandit1/-`

The command displayed the contents of the file, which was the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 2

After running:

```bash
cat ./-
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit2` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 2

Now that I have the password for the next level, I need to log in as `bandit2`.

The username changes from:

```text
bandit1
```

to:

```text
bandit2
```

The command is:

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from the `-` file and press **Enter**.

If the password is correct, I am logged into **Bandit Level 2**.

---

## 🔄 Level 1 → Level 2 Process

```text
Already logged in as bandit1
        ↓
ls
        ↓
Find a file named -
        ↓
cat -  (doesn't work, waits for keyboard input)
        ↓
Ctrl + C
        ↓
cat ./-
        ↓
Read the next-level password
        ↓
Copy the password
        ↓
SSH as bandit2
        ↓
Enter the password
        ↓
Level 2
```

## 🧠 What I Learned

- `-` has a special meaning for many commands: it means standard input.
- `cat -` waits for keyboard input instead of reading a file.
- **Ctrl + C** stops a command that is running or stuck.
- Adding `./` in front of a file name makes the command treat it as a file path.
- Tricky file names can be handled by using a relative (`./`) or full (`/home/...`) path.

## 🎓 Key Takeaway

The important command I learned in Level 1 → Level 2 was:

```bash
cat ./-
```

This let me read a file whose name would normally be treated as a special symbol.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 1 to Level 2**.

👉 [Level 2 → Level 3](../Level-03/README.md)
