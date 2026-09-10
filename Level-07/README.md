# 🏴 Bandit Level 6 → Level 7

<!-- 📸 SCREENSHOT: add the Level 6 → Level 7 challenge page screenshot here -->


After logging into Bandit Level 6 as `bandit6`, I read the goal for this level: the password for the next level is stored **somewhere on the server** and has all of the following properties:

- owned by user `bandit7`
- owned by group `bandit6`
- `33` bytes in size

This time the file is not in the home directory. It could be anywhere on the whole system.

## 🔍 Step 1 — Search the Whole Server with `find`

I used `find` again, but this time I started the search from `/`, the **root** of the file system:

```bash
find / -user bandit7 -group bandit6 -size 33c
```

In this command:

- `/` → start searching from the very top of the file system, so every directory is checked.
- `-user bandit7` → the file must be owned by the user `bandit7`.
- `-group bandit6` → the file must belong to the group `bandit6`.
- `-size 33c` → the file must be exactly **33 bytes**.

### ❌ The Problem: Too Many Errors

The output was flooded with lines like:

```text
find: '/root': Permission denied
find: '/proc/...': Permission denied
...
```

As `bandit6`, I am not allowed to look inside many system directories, so `find` prints an error for each one. The real result was buried somewhere in all that noise.

---

## 🧹 Step 2 — Hide the Error Messages

I ran the same command again, but sent all the error messages away:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### 🔎 What does `2>/dev/null` do?

Every Linux command has two main outputs:

- **stdout** (number `1`) → normal output.
- **stderr** (number `2`) → error messages.

In `2>/dev/null`:

- `2` → stderr, the error messages.
- `>` → redirect (send) the output somewhere else.
- `/dev/null` → a special "black hole" file. Anything written to it disappears.

So the errors are thrown away and only the real results are shown.

This time the output was just one line:

```text
/var/lib/dpkg/info/bandit7.password
```

---

## 📖 Step 3 — Read the File

```bash
cat /var/lib/dpkg/info/bandit7.password
```

The command displayed the contents of the file, which was the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 7

After running:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit7` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 7

Now that I have the password for the next level, I need to log in as `bandit7`.

The username changes from:

```text
bandit6
```

to:

```text
bandit7
```

The command is:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from `bandit7.password` and press **Enter**.

If the password is correct, I am logged into **Bandit Level 7**.

---

## 🔄 Level 6 → Level 7 Process

```text
Already logged in as bandit6
        ↓
find / -user bandit7 -group bandit6 -size 33c
        ↓
Too many "Permission denied" errors
        ↓
Add 2>/dev/null to hide errors
        ↓
Found /var/lib/dpkg/info/bandit7.password
        ↓
cat /var/lib/dpkg/info/bandit7.password
        ↓
Copy the password
        ↓
SSH as bandit7
        ↓
Enter the password
        ↓
Level 7
```

## 🧠 What I Learned

- `/` is the root directory, the top of the whole Linux file system.
- `find` can search by owner (`-user`) and group (`-group`).
- Every file in Linux has an owner user and an owner group.
- Commands have two outputs: stdout (`1`) for results and stderr (`2`) for errors.
- `2>/dev/null` hides error messages so only useful output is shown.

## 🎓 Key Takeaway

The important command I learned in Level 6 → Level 7 was:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

`2>/dev/null` is very useful whenever a command shows lots of "Permission denied" errors.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 6 to Level 7**.

👉 [Level 7 → Level 8](../Level-08/README.md)
