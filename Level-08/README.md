# 🏴 Bandit Level 7 → Level 8

<!-- 📸 SCREENSHOT: add the Level 7 → Level 8 challenge page screenshot here -->


After logging into Bandit Level 7 as `bandit7`, I read the goal for this level: the password for the next level is stored in the file `data.txt` **next to the word `millionth`**.

## 📋 Step 1 — List the Files

```bash
ls
```

The output showed:

```text
data.txt
```

---

## 👀 Step 2 — Look at the File Size

I first tried to open it:

```bash
cat data.txt
```

The file is **huge**. Thousands of lines scrolled past, each one a word followed by a random string. Finding one word by scrolling was not practical.

> 💡 `wc -l data.txt` counts the lines in a file. It showed that `data.txt` has thousands of lines.

---

## 🔍 Step 3 — Search for the Word `millionth`

I used `grep` to find only the line containing `millionth`:

```bash
grep millionth data.txt
```

### 🔎 What is `grep`?

`grep` searches a file for a word or pattern and prints **only the lines that match**.

In this command:

- `grep` → the search command.
- `millionth` → the word I am looking for.
- `data.txt` → the file to search in.

The output was just one line:

```text
millionth       <password>
```

The string next to `millionth` is the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 8

After running:

```bash
grep millionth data.txt
```

the terminal displayed the password for the next level, right next to the word `millionth`.

I copied the password from the terminal.

This password is used to authenticate as the `bandit8` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 8

Now that I have the password for the next level, I need to log in as `bandit8`.

The username changes from:

```text
bandit7
```

to:

```text
bandit8
```

The command is:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I found next to `millionth` and press **Enter**.

If the password is correct, I am logged into **Bandit Level 8**.

---

## 🔄 Level 7 → Level 8 Process

```text
Already logged in as bandit7
        ↓
ls
        ↓
Find data.txt
        ↓
cat data.txt  (way too many lines)
        ↓
grep millionth data.txt
        ↓
Password is next to "millionth"
        ↓
Copy the password
        ↓
SSH as bandit8
        ↓
Enter the password
        ↓
Level 8
```

## 🧠 What I Learned

- `grep` searches for text inside files and prints only the matching lines.
- `grep` is much faster than scrolling through a large file.
- `wc -l` counts how many lines a file has.
- When a file is too big to read, search it instead.

## 🎓 Key Takeaway

The important command I learned in Level 7 → Level 8 was:

```bash
grep millionth data.txt
```

`grep` is one of the most useful Linux commands for finding information in big files and logs.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 7 to Level 8**.

👉 [Level 8 → Level 9](../Level-09/README.md)
