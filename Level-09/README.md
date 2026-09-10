# 🏴 Bandit Level 8 → Level 9

<!-- 📸 SCREENSHOT: add the Level 8 → Level 9 challenge page screenshot here -->


After logging into Bandit Level 8 as `bandit8`, I read the goal for this level: the password for the next level is stored in the file `data.txt` and is **the only line of text that occurs only once**.

## 📋 Step 1 — Look at the File

```bash
ls
```

The output showed:

```text
data.txt
```

When I looked at the contents with `cat data.txt`, I saw many random-looking strings, and the same lines were repeated many times. I needed to find the one line that is **not** repeated.

---

## 🔎 Step 2 — Understand `sort` and `uniq`

### What is `sort`?

`sort` arranges the lines of a file in alphabetical order.

After sorting, all identical lines end up **next to each other**.

### What is `uniq`?

`uniq` works on lines that are next to each other:

- `uniq` → removes duplicate lines that are next to each other.
- `uniq -u` → shows **only the lines that appear once** (the unique ones).
- `uniq -c` → shows how many times each line appears.

⚠️ `uniq` only compares lines that are **next to each other**. That's why the file has to be sorted first. Running `uniq -u data.txt` on its own gives the wrong answer.

---

## 🔗 Step 3 — Combine Them with a Pipe

```bash
sort data.txt | uniq -u
```

### 🔎 What is `|` (pipe)?

The `|` symbol is called a **pipe**.

It takes the output of the command on the left and gives it as input to the command on the right.

In this command:

- `sort data.txt` → sorts all the lines so duplicates are grouped together.
- `|` → passes the sorted lines to the next command.
- `uniq -u` → prints only the line that appears exactly once.

The output was a single line, which was the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 9

After running:

```bash
sort data.txt | uniq -u
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit9` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 9

Now that I have the password for the next level, I need to log in as `bandit9`.

The username changes from:

```text
bandit8
```

to:

```text
bandit9
```

The command is:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from `sort` and `uniq` and press **Enter**.

If the password is correct, I am logged into **Bandit Level 9**.

---

## 🔄 Level 8 → Level 9 Process

```text
Already logged in as bandit8
        ↓
ls
        ↓
Find data.txt (lots of repeated lines)
        ↓
sort data.txt
        ↓
Duplicate lines are now next to each other
        ↓
| uniq -u
        ↓
Only the line that appears once is left
        ↓
Copy the password
        ↓
SSH as bandit9
        ↓
Enter the password
        ↓
Level 9
```

## 🧠 What I Learned

- `sort` puts lines in order so duplicates are grouped together.
- `uniq` only compares lines that are next to each other.
- `uniq -u` prints lines that occur only once.
- `uniq -c` counts how many times each line appears.
- The pipe `|` sends the output of one command into another command.

## 🎓 Key Takeaway

The important command I learned in Level 8 → Level 9 was:

```bash
sort data.txt | uniq -u
```

Pipes let me chain small commands together to solve a bigger problem.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 8 to Level 9**.

👉 [Level 9 → Level 10](../Level-10/README.md)
