# 🏴 Bandit Level 9 → Level 10

<!-- 📸 SCREENSHOT: add the Level 9 → Level 10 challenge page screenshot here -->


After logging into Bandit Level 9 as `bandit9`, I read the goal for this level: the password for the next level is stored in the file `data.txt` in one of the few **human-readable strings**, preceded by several **`=`** characters.

## 📋 Step 1 — Check the File

```bash
ls
```

The output showed:

```text
data.txt
```

Before opening it, I checked what type of file it is:

```bash
file data.txt
```

The output said:

```text
data.txt: data
```

`data` means it is mostly **binary** (non-text) data. Running `cat` on it would fill the terminal with strange symbols.

---

## ❌ Step 2 — Why `grep` Alone Doesn't Help

My first idea was to search for `=` like in the previous levels:

```bash
grep "==" data.txt
```

But because the file is binary, `grep` only said:

```text
grep: data.txt: binary file matches
```

It found a match but didn't show the text.

---

## 🔤 Step 3 — Pull Out the Readable Text with `strings`

```bash
strings data.txt
```

### 🔎 What is `strings`?

`strings` looks through a binary file and prints only the **human-readable text** inside it (sequences of printable characters).

This removed all the binary junk, but there were still a lot of random-looking lines.

---

## 🔍 Step 4 — Filter for Lines with `=`

I combined `strings` with `grep` using a pipe:

```bash
strings data.txt | grep "=="
```

In this command:

- `strings data.txt` → extracts the readable text from the binary file.
- `|` → passes that text to the next command.
- `grep "=="` → keeps only the lines that contain `==`.

The output showed a few lines, roughly like this:

```text
========== the
========== password
========== is
========== <password>
```

Read together, the lines say **"the password is ..."**, and the last line has the password for the next level.

---

## 🔑 Step 5 — Copy the Password for Level 10

After running:

```bash
strings data.txt | grep "=="
```

the terminal displayed the password for the next level on the last line.

I copied the password from the terminal.

This password is used to authenticate as the `bandit10` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 6 — Connect to Bandit Level 10

Now that I have the password for the next level, I need to log in as `bandit10`.

The username changes from:

```text
bandit9
```

to:

```text
bandit10
```

The command is:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I found after the `=` signs and press **Enter**.

If the password is correct, I am logged into **Bandit Level 10**.

---

## 🔄 Level 9 → Level 10 Process

```text
Already logged in as bandit9
        ↓
ls
        ↓
file data.txt  → binary data
        ↓
grep "==" data.txt  → "binary file matches"
        ↓
strings data.txt | grep "=="
        ↓
Lines read "the password is ..."
        ↓
Copy the password
        ↓
SSH as bandit10
        ↓
Enter the password
        ↓
Level 10
```

## 🧠 What I Learned

- `file` shows whether a file is text or binary.
- `grep` on a binary file only says "binary file matches" instead of showing the line.
- `strings` pulls the human-readable text out of a binary file.
- `strings` and `grep` together make it easy to search inside binary files.

## 🎓 Key Takeaway

The important command I learned in Level 9 → Level 10 was:

```bash
strings data.txt | grep "=="
```

`strings` is useful for finding hidden text inside binary files.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 9 to Level 10**.

👉 [Level 10 → Level 11](../Level-11/README.md)
