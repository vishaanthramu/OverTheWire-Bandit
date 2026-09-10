# 🏴 Bandit Level 14 → Level 15

<!-- 📸 SCREENSHOT: add the Level 14 → Level 15 challenge page screenshot here -->


After logging into Bandit Level 14 as `bandit14`, I read the goal for this level: the password for the next level can be retrieved by **submitting the password of the current level to port `30000` on `localhost`**.

## 🔑 Step 1 — Get the Current Level's Password

I need the `bandit14` password to submit. I already got it at the end of the last level, but I can read it again because I am logged in as `bandit14`:

```bash
cat /etc/bandit_pass/bandit14
```

---

## 🔎 Step 2 — Understand `localhost` and Ports

### What is `localhost`?

`localhost` means **this same computer**. When I use `localhost` on the Bandit server, I am talking to the Bandit server itself (its address is `127.0.0.1`).

### What is a port?

A **port** is a numbered "door" on a computer that a program listens on. For example:

- SSH on Bandit listens on port `2220`.
- For this level, a special program is listening on port **`30000`**.

That program checks whatever I send it. If it's the correct `bandit14` password, it replies with the next password.

---

## 🌐 Step 3 — Send the Password with `nc`

I sent the password to port `30000` using `nc`:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

### 🔎 What is `nc`?

`nc` stands for **netcat**. It opens a network connection and lets me send and receive raw text through it.

In this command:

- `cat /etc/bandit_pass/bandit14` → prints the current password.
- `|` → sends that password into `nc`.
- `nc` → opens a connection.
- `localhost` → connect to this same machine.
- `30000` → the port to connect to.

> 💡 I could also run just `nc localhost 30000`, then paste the password and press **Enter**. The pipe does the same thing in one line.

The output was:

```text
Correct!
<password>
```

---

## 🔑 Step 4 — Copy the Password for Level 15

After running:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

the server replied with `Correct!` and the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit15` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 15

Now that I have the password for the next level, I need to log in as `bandit15`.

The username changes from:

```text
bandit14
```

to:

```text
bandit15
```

The command is:

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that port `30000` gave me and press **Enter**.

If the password is correct, I am logged into **Bandit Level 15**.

---

## 🔄 Level 14 → Level 15 Process

```text
Logged in as bandit14
        ↓
cat /etc/bandit_pass/bandit14
        ↓
Get the current password
        ↓
cat /etc/bandit_pass/bandit14 | nc localhost 30000
        ↓
Server replies "Correct!" + next password
        ↓
Copy the password
        ↓
SSH as bandit15
        ↓
Enter the password
        ↓
Level 15
```

## 🧠 What I Learned

- `localhost` (`127.0.0.1`) means the machine I am currently on.
- A port is a numbered endpoint where a program listens for connections.
- `nc` (netcat) connects to a port and sends or receives text.
- Piping into `nc` is a quick way to send data to a network service.
- Programs don't only read files. They can also talk over the network.

## 🎓 Key Takeaway

The important command I learned in Level 14 → Level 15 was:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

This was my first level that used networking, and `nc` is the basic tool for it.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 14 to Level 15**.

Next up is **Level 15 → Level 16**, where the password has to be sent over an **encrypted SSL/TLS** connection instead of plain `nc`. 🔐
