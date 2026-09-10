# 🏴 Bandit Level 13 → Level 14

<!-- 📸 SCREENSHOT: add the Level 13 → Level 14 challenge page screenshot here -->


After logging into Bandit Level 13 as `bandit13`, I read the goal for this level: the password for the next level is stored in `/etc/bandit_pass/bandit14` and can **only be read by user `bandit14`**.

This time I don't get a password. Instead, I get a **private SSH key** that can be used to log into the next level.

## 📋 Step 1 — List the Files

```bash
ls
```

In the home directory I found a file called:

```text
sshkey.private
```

(There is also a hint file in the home directory for anyone who gets stuck.)

When I tried to read the password file directly:

```bash
cat /etc/bandit_pass/bandit14
```

I got:

```text
cat: /etc/bandit_pass/bandit14: Permission denied
```

That's expected, since only `bandit14` can read it. So I need to **become** `bandit14` using the key.

---

## 🔎 Step 2 — What is an SSH Private Key?

So far I have logged in with **passwords**. SSH can also log in with a **key pair**:

- **Public key** → stored on the server, in the user's account. It is like a lock.
- **Private key** → kept by the user. It is like the key that opens that lock.

If I have the private key that matches `bandit14`'s public key, the server lets me in as `bandit14` **without a password**.

⚠️ A private key is just as secret as a password. Anyone who has it can log in.

---

## 📥 Step 3 — Copy the Key to My Own Computer

The Bandit server blocks SSH logins to `localhost` from inside itself, so I needed to use the key from my own computer.

I logged out of the Bandit server with `exit`, and then on **my own machine** I ran:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```

### 🔎 What is `scp`?

`scp` stands for **Secure Copy**. It copies files between computers over SSH.

In this command:

- `scp` → the secure copy command.
- `-P 2220` → use port `2220`. ⚠️ `scp` uses a **capital** `-P`, while `ssh` uses a lowercase `-p`.
- `bandit13@bandit.labs.overthewire.org:` → log in as `bandit13` on the Bandit server.
- `sshkey.private` → the file to copy (from `bandit13`'s home directory).
- `.` → save it in my current directory.

It asked for the `bandit13` password, and then copied the file.

---

## 🔒 Step 4 — Fix the Key's Permissions

The first time I tried to use the key, SSH refused it with a warning like:

```text
WARNING: UNPROTECTED PRIVATE KEY FILE!
Permissions 0644 for 'sshkey.private' are too open.
```

SSH won't use a private key that other users on my computer can read. So I changed the permissions:

```bash
chmod 600 sshkey.private
```

### 🔎 What is `chmod`?

`chmod` stands for **change mode**. It changes who can read, write or execute a file.

`600` means:

- `6` → **owner** (me) can read and write.
- `0` → **group** gets no access.
- `0` → **others** get no access.

---

## 🔐 Step 5 — Log In as `bandit14` Using the Key

```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

In this command:

- `-i sshkey.private` → use this **identity** (private key) file to log in.
- `bandit14@...` → log in as the `bandit14` user.
- `-p 2220` → the Bandit SSH port.

This time the server did **not** ask for a password. I was logged in as **`bandit14`** straight away.

---

## 📖 Step 6 — Read the Password for Level 14

Now that I am `bandit14`, I'm allowed to read the password file:

```bash
cat /etc/bandit_pass/bandit14
```

The terminal displayed the password for `bandit14`.

I copied and saved it, because I will **need it in the next level**. From now on I can also log in as `bandit14` with this password instead of the key.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔄 Level 13 → Level 14 Process

```text
Logged in as bandit13
        ↓
ls  →  find sshkey.private
        ↓
cat /etc/bandit_pass/bandit14  →  Permission denied
        ↓
exit
        ↓
scp -P 2220 bandit13@...:sshkey.private .
        ↓
chmod 600 sshkey.private
        ↓
ssh -i sshkey.private bandit14@... -p 2220
        ↓
Logged in as bandit14 (no password needed)
        ↓
cat /etc/bandit_pass/bandit14
        ↓
Save the password
        ↓
Level 14
```

## 🧠 What I Learned

- SSH can log in using a private key instead of a password.
- `ssh -i` chooses which private key file to use.
- `scp` copies files over SSH. It uses `-P` (capital) for the port.
- SSH refuses private keys with permissions that are too open.
- `chmod 600` makes a file readable and writable only by its owner.
- `/etc/bandit_pass/` holds each level's password, and only that level's user can read it.

## 🎓 Key Takeaway

The important commands I learned in Level 13 → Level 14 were:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14
```

Key-based login is how SSH is used in real life, so this was one of the most useful levels so far.

## ➡️ Next

After logging in with the SSH key, I successfully moved from **Bandit Level 13 to Level 14**.

👉 [Level 14 → Level 15](../Level-15/README.md)
