# 🐧 Bandit Level 0

> 🎯 **Goal:** Connect to the Bandit server using SSH.

## 🔐 Step 1 — Understanding the Level

Bandit Level 0 is the starting point of the OverTheWire Bandit wargame.

The first task is simply to connect to the remote Bandit server using **SSH**.

The information provided for the connection is:

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit0`
- **Password:** `bandit0`

---

## 💻 Step 2 — Connect Using SSH

I opened my terminal and used the following command:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### 🔎 What is `ssh`?

`ssh` stands for **Secure Shell**.

It lets me log into a remote computer over the network and run commands on it, as if I was sitting in front of it. All the traffic is encrypted.

In this command:

- `ssh` → the program used to connect to the remote server.
- `bandit0` → the username I want to log in as.
- `@` → separates the username from the server address.
- `bandit.labs.overthewire.org` → the address of the Bandit server.
- `-p 2220` → connect on port `2220` instead of the default SSH port `22`.

---

## ✅ Step 3 — Accept the Server Fingerprint

Because this was my first time connecting to this server, SSH showed a message like:

```text
The authenticity of host '[bandit.labs.overthewire.org]:2220' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

I typed:

```text
yes
```

and pressed **Enter**.

This saves the server's fingerprint on my computer, so SSH will recognise the server the next time I connect.

---

## 🔑 Step 4 — Enter the Password

The server then asked for the password.

I typed:

```text
bandit0
```

and pressed **Enter**.

> 💡 While typing a password in the terminal, nothing appears on the screen, not even `*`. This is normal. The password is still being typed.

---

## 🎉 Step 5 — Logged In

After entering the correct password, the Bandit welcome banner appeared and my prompt changed to:

```text
bandit0@bandit:~$
```

This shows that I am now logged into the Bandit server as the `bandit0` user.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your Level 0 login screenshot here -->

---

## 🔄 Level 0 Process

```text
Open terminal
        ↓
ssh bandit0@bandit.labs.overthewire.org -p 2220
        ↓
Type yes to accept the fingerprint
        ↓
Enter the password: bandit0
        ↓
Logged in as bandit0
        ↓
Level 0
```

## 🧠 What I Learned

- `ssh` is used to log into a remote server securely.
- The format is `ssh username@host -p port`.
- `-p` is used when the server does not use the default port `22`.
- The first time I connect to a server, SSH asks me to confirm its fingerprint.
- Passwords are not shown on the screen while typing.

## 🎓 Key Takeaway

The important command I learned in Level 0 was:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

This command is used to connect to every Bandit level. Only the username changes.

## ➡️ Next

Now that I am logged in as `bandit0`, I can start looking for the password for **Bandit Level 1**.

👉 [Level 0 → Level 1](../Level-01/README.md)
