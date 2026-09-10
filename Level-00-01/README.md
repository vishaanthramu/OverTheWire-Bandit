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
