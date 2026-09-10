# 🏴 Bandit Level 10 → Level 11

<!-- 📸 SCREENSHOT: add the Level 10 → Level 11 challenge page screenshot here -->


After logging into Bandit Level 10 as `bandit10`, I read the goal for this level: the password for the next level is stored in the file `data.txt`, which contains **base64 encoded data**.

## 📋 Step 1 — Look at the File

```bash
ls
cat data.txt
```

The file contained just one line of random-looking letters and numbers, ending with `=`:

```text
VGhlIHBhc3N3b3JkIGlz...=
```

This is what **base64** encoded text usually looks like.

---

## 🔎 Step 2 — What is Base64?

**Base64** is a way of **encoding** data using only 64 safe characters:

- `A–Z`
- `a–z`
- `0–9`
- `+` and `/`

`=` is used as **padding** at the end.

It is often used to send data (like images or attachments) through systems that only handle text.

⚠️ Base64 is **encoding, not encryption**. There is no key or password needed. Anyone can decode it.

---

## 🔓 Step 3 — Decode the File

```bash
base64 -d data.txt
```

### 🔎 What is `base64 -d`?

- `base64` → the command to encode or decode base64 data.
- `-d` → **decode**, converting the base64 back to the original text.
- `data.txt` → the file to decode.

The output was:

```text
The password is <password>
```

---

## 🔑 Step 4 — Copy the Password for Level 11

After running:

```bash
base64 -d data.txt
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit11` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 11

Now that I have the password for the next level, I need to log in as `bandit11`.

The username changes from:

```text
bandit10
```

to:

```text
bandit11
```

The command is:

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the decoded password and press **Enter**.

If the password is correct, I am logged into **Bandit Level 11**.

---

## 🔄 Level 10 → Level 11 Process

```text
Already logged in as bandit10
        ↓
cat data.txt
        ↓
Looks like base64 (letters, numbers, ends with =)
        ↓
base64 -d data.txt
        ↓
"The password is ..."
        ↓
Copy the password
        ↓
SSH as bandit11
        ↓
Enter the password
        ↓
Level 11
```

## 🧠 What I Learned

- Base64 turns data into text using 64 characters (`A–Z`, `a–z`, `0–9`, `+`, `/`).
- `=` at the end is a common sign that text is base64.
- `base64 -d` decodes base64 back into the original data.
- Encoding is **not** the same as encryption. Base64 can be decoded by anyone.

## 🎓 Key Takeaway

The important command I learned in Level 10 → Level 11 was:

```bash
base64 -d data.txt
```

Base64 hides nothing. It only changes how the data looks.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 10 to Level 11**.

👉 [Level 11 → Level 12](../Level-12/README.md)
