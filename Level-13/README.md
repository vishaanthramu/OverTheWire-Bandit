# 🏴 Bandit Level 12 → Level 13

<!-- 📸 SCREENSHOT: add the Level 12 → Level 13 challenge page screenshot here -->


After logging into Bandit Level 12 as `bandit12`, I read the goal for this level: the password for the next level is stored in the file `data.txt`, which is a **hexdump** of a file that has been **repeatedly compressed**.

The level also suggested working inside a temporary directory under `/tmp`.

This was the longest level so far, because the file had to be unpacked many times.

## 📂 Step 1 — Create a Temporary Working Directory

I can't create files in my home directory on the Bandit server, so I made a private temporary directory:

```bash
mktemp -d
```

### 🔎 What is `mktemp -d`?

`mktemp` creates a temporary file with a random name. With `-d` it creates a temporary **directory** instead.

The output was something like:

```text
/tmp/tmp.XXXXXXXXXX
```

(The `XXXXXXXXXX` part is random, so other players can't guess it.)

Then I copied `data.txt` into it and moved there:

```bash
cp data.txt /tmp/tmp.XXXXXXXXXX
cd /tmp/tmp.XXXXXXXXXX
```

- `cp` → **copy** a file from one place to another.
- `cd` → move into the new directory.

---

## 🔢 Step 2 — Turn the Hexdump Back into a File

When I opened `data.txt`, it looked like this:

```text
00000000: 1f8b 0808 ...  ................
00000010: ...
```

This is a **hexdump**: the bytes of a file written out as hexadecimal numbers. I needed to convert it back into the real file:

```bash
xxd -r data.txt > data
```

### 🔎 What is `xxd -r`?

- `xxd` → creates a hexdump from a file.
- `-r` → **reverse**, turning a hexdump back into the original binary file.
- `> data` → save the result into a new file called `data`.

---

## 🔍 Step 3 — Use `file` to Find Out What Each Layer Is

From here on, I repeated the same loop:

```text
file  →  rename with the right extension  →  decompress  →  file again ...
```

### 🔎 Why `file` every time?

The file was compressed several times using **different** tools. The file name doesn't tell me which one was used, but `file` does by reading the file's contents.

| `file` says... | Tool to use | Command |
|---|---|---|
| `gzip compressed data` | gzip | `mv x x.gz` then `gzip -d x.gz` |
| `bzip2 compressed data` | bzip2 | `mv x x.bz2` then `bzip2 -d x.bz2` |
| `POSIX tar archive` | tar | `tar -xf x` |
| `ASCII text` | — | `cat x` 🎉 |

- `mv` → **move / rename** a file. `gzip` and `bzip2` expect the right extension (`.gz`, `.bz2`), so I renamed the file before decompressing.
- `gzip -d` → decompress a `.gz` file.
- `bzip2 -d` → decompress a `.bz2` file.
- `tar -xf` → **extract** (`-x`) the files from a tar archive **file** (`-f`).

---

## 📦 Step 4 — Peel Off Every Layer

In my case, the layers went like this (always check with `file` first, the order is what matters):

```bash
file data                 # gzip compressed data
mv data data2.gz
gzip -d data2.gz

file data2                # bzip2 compressed data
mv data2 data3.bz2
bzip2 -d data3.bz2

file data3                # gzip compressed data
mv data3 data4.gz
gzip -d data4.gz

file data4                # POSIX tar archive
tar -xf data4             # extracts data5.bin

file data5.bin            # POSIX tar archive
tar -xf data5.bin         # extracts data6.bin

file data6.bin            # bzip2 compressed data
mv data6.bin data7.bz2
bzip2 -d data7.bz2

file data7                # POSIX tar archive
tar -xf data7             # extracts data8.bin

file data8.bin            # gzip compressed data
mv data8.bin data9.gz
gzip -d data9.gz

file data9                # ASCII text  🎉
```

After all the layers were removed, `file` finally said **ASCII text**.

---

## 📖 Step 5 — Read the Final File

```bash
cat data9
```

The output was:

```text
The password is <password>
```

---

## 🔑 Step 6 — Copy the Password for Level 13

After running:

```bash
cat data9
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit13` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 7 — Connect to Bandit Level 13

Now that I have the password for the next level, I need to log in as `bandit13`.

The username changes from:

```text
bandit12
```

to:

```text
bandit13
```

The command is:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password from the final file and press **Enter**.

If the password is correct, I am logged into **Bandit Level 13**.

---

## 🔄 Level 12 → Level 13 Process

```text
Already logged in as bandit12
        ↓
mktemp -d  →  cp data.txt  →  cd into it
        ↓
xxd -r data.txt > data
        ↓
file → gzip   → gzip -d
        ↓
file → bzip2  → bzip2 -d
        ↓
file → gzip   → gzip -d
        ↓
file → tar    → tar -xf
        ↓
file → tar    → tar -xf
        ↓
file → bzip2  → bzip2 -d
        ↓
file → tar    → tar -xf
        ↓
file → gzip   → gzip -d
        ↓
file → ASCII text → cat
        ↓
Copy the password
        ↓
SSH as bandit13
        ↓
Level 13
```

## 🧠 What I Learned

- `mktemp -d` creates a private temporary directory with a random name.
- `cp` copies files and `mv` renames or moves them.
- A hexdump shows a file's bytes as hex, and `xxd -r` converts it back.
- `file` identifies the real type of a file, whatever its name is.
- `gzip -d`, `bzip2 -d` and `tar -xf` unpack the three common Linux archive formats.
- When a task repeats, I follow the same loop: check → act → check again.

## 🎓 Key Takeaway

The important commands I learned in Level 12 → Level 13 were:

```bash
mktemp -d
xxd -r data.txt > data
file data
gzip -d file.gz
bzip2 -d file.bz2
tar -xf file
```

The most important one is `file`. It told me what to do next at every step.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 12 to Level 13**.

👉 [Level 13 → Level 14](../Level-14/README.md)
