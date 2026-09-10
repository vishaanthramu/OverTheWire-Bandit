# 🏴 Bandit Level 4 → Level 5

<!-- 📸 SCREENSHOT: add the Level 4 → Level 5 challenge page screenshot here -->


After logging into Bandit Level 4 as `bandit4`, I read the goal for this level: the password for the next level is stored in the **only human-readable file** in the `inhere` directory.

## 📂 Step 1 — Look Inside the `inhere` Directory

```bash
cd inhere
ls
```

The output showed:

```text
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

There are 10 files, and they all start with `-`, just like the file in Level 1 → Level 2.

Opening each file one by one with `cat` would work, but most of them contain random binary data that can mess up the terminal.

> 💡 If the terminal starts showing strange characters after `cat`-ing a binary file, the `reset` command fixes it.

---

## 🔍 Step 2 — Check the File Types

Instead of guessing, I used the `file` command on all of them at once:

```bash
file ./*
```

### 🔎 What is `file`?

`file` looks at the contents of a file and tells me **what type of data** it contains, such as text, an image, a compressed archive or random binary data.

In this command:

- `file` → identifies the file type.
- `./` → the current directory. It also stops `-file00` etc. from being read as options.
- `*` → a **wildcard** that matches every file name.

The output looked like this:

```text
./-file00: data
./-file01: data
./-file02: data
...
./-file07: ASCII text
...
./-file09: data
```

Most files are just `data` (binary), but one file is **`ASCII text`**, which means it is human-readable.

In my case, it was `-file07`.

---

## 📖 Step 3 — Read the Human-Readable File

```bash
cat ./-file07
```

The command displayed the contents of the file, which was the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 5

After running:

```bash
cat ./-file07
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit5` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 5

Now that I have the password for the next level, I need to log in as `bandit5`.

The username changes from:

```text
bandit4
```

to:

```text
bandit5
```

The command is:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from `-file07` and press **Enter**.

If the password is correct, I am logged into **Bandit Level 5**.

---

## 🔄 Level 4 → Level 5 Process

```text
Already logged in as bandit4
        ↓
cd inhere
        ↓
ls
        ↓
10 files: -file00 to -file09
        ↓
file ./*
        ↓
Find the one that is "ASCII text"
        ↓
cat ./-file07
        ↓
Copy the password
        ↓
SSH as bandit5
        ↓
Enter the password
        ↓
Level 5
```

## 🧠 What I Learned

- `file` tells me what kind of data is inside a file.
- `ASCII text` means the file is human-readable. `data` usually means binary.
- `*` is a wildcard that matches all file names.
- `./*` safely passes files starting with `-` to a command.
- `reset` fixes a terminal that got messed up by binary output.

## 🎓 Key Takeaway

The important commands I learned in Level 4 → Level 5 were:

```bash
file ./*
cat ./-file07
```

`file` saves time by showing which file is worth reading, instead of opening every file one by one.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 4 to Level 5**.

👉 [Level 5 → Level 6](../Level-06/README.md)
