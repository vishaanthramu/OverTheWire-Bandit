# 🏴 Bandit Level 2 → Level 3

<!-- 📸 SCREENSHOT: add the Level 2 → Level 3 challenge page screenshot here -->


After logging into Bandit Level 2 as `bandit2`, I read the goal for this level: the password for the next level is stored in a file called **`--spaces in this filename--`** located in the home directory.

## 📋 Step 1 — List the Files

I checked the home directory:

```bash
ls
```

The output showed:

```text
--spaces in this filename--
```

This file name has two problems:

1. It contains **spaces**.
2. It starts with **`--`**.

---

## ❌ Step 2 — Why the Normal Way Fails

If I type:

```bash
cat --spaces in this filename--
```

it does not work, for two reasons:

- **Spaces:** The shell uses spaces to separate arguments. So `cat` receives four separate words: `--spaces`, `in`, `this` and `filename--`.
- **Dashes:** Anything starting with `-` or `--` is treated as an **option** (like `-p` in `ssh -p`). So `cat` thinks `--spaces` is an option it doesn't know and shows an error.

---

## 📖 Step 3 — Read the File Correctly

To fix both problems, I used quotes **and** `./`:

```bash
cat "./--spaces in this filename--"
```

### 🔎 How does this work?

- `" "` → the quotes keep the whole name together as **one** argument, so the spaces don't split it.
- `./` → the name now starts with `.` instead of `-`, so `cat` doesn't treat it as an option.

> 💡 Other ways that also work:
>
> ```bash
> cat -- "--spaces in this filename--"
> cat ./--spaces\ in\ this\ filename--
> ```
>
> - `--` on its own tells a command "no more options after this point, everything else is a file name".
> - `\` (backslash) before a space **escapes** it, so the shell treats the space as part of the name.
>
> Pressing **Tab** after typing `./--sp` also auto-completes the name with the escapes added for me.

The command displayed the contents of the file, which was the password for the next level.

---

## 🔑 Step 4 — Copy the Password for Level 3

After running:

```bash
cat "./--spaces in this filename--"
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit3` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 3

Now that I have the password for the next level, I need to log in as `bandit3`.

The username changes from:

```text
bandit2
```

to:

```text
bandit3
```

The command is:

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the password that I obtained from the file and press **Enter**.

If the password is correct, I am logged into **Bandit Level 3**.

---

## 🔄 Level 2 → Level 3 Process

```text
Already logged in as bandit2
        ↓
ls
        ↓
Find "--spaces in this filename--"
        ↓
Spaces split the name + "--" looks like an option
        ↓
cat "./--spaces in this filename--"
        ↓
Read the next-level password
        ↓
Copy the password
        ↓
SSH as bandit3
        ↓
Enter the password
        ↓
Level 3
```

## 🧠 What I Learned

- The shell splits arguments on spaces.
- Quotes `" "` keep a name with spaces together as one argument.
- A backslash `\` escapes a single character, like a space.
- Arguments starting with `-` or `--` are treated as options.
- `./` in front of a name, or `--` before it, stops it from being read as an option.
- **Tab** completion can type tricky file names for me.

## 🎓 Key Takeaway

The important command I learned in Level 2 → Level 3 was:

```bash
cat "./--spaces in this filename--"
```

Quoting and `./` together let me read a file with both spaces and leading dashes in its name.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 2 to Level 3**.

👉 [Level 3 → Level 4](../Level-04/README.md)
