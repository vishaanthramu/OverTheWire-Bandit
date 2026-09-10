# 🏴 Bandit Level 3 → Level 4

<!-- 📸 SCREENSHOT: add the Level 3 → Level 4 challenge page screenshot here -->


After logging into Bandit Level 3 as `bandit3`, I read the goal for this level: the password for the next level is stored in a **hidden file** in the `inhere` directory.

## 📋 Step 1 — List the Files

I checked the home directory:

```bash
ls
```

The output showed:

```text
inhere
```

`inhere` is a directory, so the password must be inside it.

---

## 📂 Step 2 — Move into the `inhere` Directory

```bash
cd inhere
```

### 🔎 What is `cd`?

`cd` stands for **change directory**.

It moves me from the current directory into another one.

- `cd inhere` → go into the `inhere` directory.
- `cd ..` → go back up one directory.
- `cd ~` or just `cd` → go back to my home directory.

Then I listed the files inside:

```bash
ls
```

This time **nothing** was shown. The directory looked empty, but the goal says the file is hidden.

---

## 👀 Step 3 — Show Hidden Files

In Linux, any file whose name starts with a dot `.` is **hidden**. Plain `ls` doesn't show it.

To see hidden files, I used:

```bash
ls -a
```

### 🔎 What does `-a` do?

`-a` stands for **all**. It tells `ls` to show every file, including hidden ones.

The output showed:

```text
.  ..  ...Hiding-From-You
```

- `.` → the current directory itself.
- `..` → the parent directory.
- `...Hiding-From-You` → the hidden file I was looking for.

> 💡 `ls -la` shows the same files as a long list with permissions, owner and size.

---

## 📖 Step 4 — Read the Hidden File

```bash
cat ...Hiding-From-You
```

The command displayed the contents of the file, which was the password for the next level.

---

## 🔑 Step 5 — Copy the Password for Level 4

After running:

```bash
cat ...Hiding-From-You
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit4` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 6 — Connect to Bandit Level 4

Now that I have the password for the next level, I need to log in as `bandit4`.

The username changes from:

```text
bandit3
```

to:

```text
bandit4
```

The command is:

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from the hidden file and press **Enter**.

If the password is correct, I am logged into **Bandit Level 4**.

---

## 🔄 Level 3 → Level 4 Process

```text
Already logged in as bandit3
        ↓
ls
        ↓
Find the inhere directory
        ↓
cd inhere
        ↓
ls  (shows nothing)
        ↓
ls -a
        ↓
Find ...Hiding-From-You
        ↓
cat ...Hiding-From-You
        ↓
Copy the password
        ↓
SSH as bandit4
        ↓
Enter the password
        ↓
Level 4
```

## 🧠 What I Learned

- `cd` is used to move between directories.
- Files starting with `.` are hidden in Linux.
- `ls` does not show hidden files, but `ls -a` does.
- `.` means the current directory and `..` means the parent directory.
- An "empty" directory might still contain hidden files.

## 🎓 Key Takeaway

The important commands I learned in Level 3 → Level 4 were:

```bash
cd inhere
ls -a
cat ...Hiding-From-You
```

`ls -a` is the command to remember whenever a directory looks empty.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 3 to Level 4**.

👉 [Level 4 → Level 5](../Level-05/README.md)
