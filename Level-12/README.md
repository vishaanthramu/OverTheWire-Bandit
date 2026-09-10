# 🏴 Bandit Level 11 → Level 12

<!-- 📸 SCREENSHOT: add the Level 11 → Level 12 challenge page screenshot here -->


After logging into Bandit Level 11 as `bandit11`, I read the goal for this level: the password for the next level is stored in the file `data.txt`, where all lowercase (`a–z`) and uppercase (`A–Z`) letters have been **rotated by 13 positions**.

## 📋 Step 1 — Look at the File

```bash
ls
cat data.txt
```

The output looked like this:

```text
Gur cnffjbeq vf <scrambled password>
```

It looks like nonsense, but it has the same shape as the last level's output (`The password is ...`). Each letter has just been shifted.

---

## 🔎 Step 2 — What is ROT13?

Rotating letters by 13 positions is called **ROT13**. It is a simple **substitution cipher**.

Each letter is replaced by the letter 13 places after it in the alphabet:

```text
A B C D E F G H I J K L M
↕ ↕ ↕ ↕ ↕ ↕ ↕ ↕ ↕ ↕ ↕ ↕ ↕
N O P Q R S T U V W X Y Z
```

So `A` becomes `N`, `B` becomes `O`, and so on. After `Z` it wraps back around to `A`.

Because the English alphabet has 26 letters, rotating by 13 **twice** gets you back to the original. So the same command is used to encode **and** decode ROT13.

For example:

```text
Gur cnffjbeq vf  →  The password is
```

---

## 🔓 Step 3 — Decode with `tr`

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### 🔎 What is `tr`?

`tr` stands for **translate**. It replaces characters from one set with characters from another set.

In this command:

- `cat data.txt` → prints the scrambled text.
- `|` → sends it to `tr`.
- `'A-Za-z'` → the original letters: all uppercase, then all lowercase.
- `'N-ZA-Mn-za-m'` → what each letter is replaced with:
  - `A–M` become `N–Z`, and `N–Z` become `A–M`
  - `a–m` become `n–z`, and `n–z` become `a–m`

Numbers and other symbols are not in the list, so they stay the same.

The output was:

```text
The password is <password>
```

---

## 🔑 Step 4 — Copy the Password for Level 12

After running:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

the terminal displayed the password for the next level.

I copied the password from the terminal.

This password is used to authenticate as the `bandit12` user.

> ⚠️ The password is not included here because this is a public GitHub write-up.

---

## 🖥️ Terminal Screenshot

<!-- 📸 SCREENSHOT: add your terminal screenshot here (blur the password!) -->


---

## 🔐 Step 5 — Connect to Bandit Level 12

Now that I have the password for the next level, I need to log in as `bandit12`.

The username changes from:

```text
bandit11
```

to:

```text
bandit12
```

The command is:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

The server then asks for the password.

I paste the decoded password and press **Enter**.

If the password is correct, I am logged into **Bandit Level 12**.

---

## 🔄 Level 11 → Level 12 Process

```text
Already logged in as bandit11
        ↓
cat data.txt
        ↓
"Gur cnffjbeq vf ..." → letters are rotated
        ↓
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
        ↓
"The password is ..."
        ↓
Copy the password
        ↓
SSH as bandit12
        ↓
Enter the password
        ↓
Level 12
```

## 🧠 What I Learned

- ROT13 shifts every letter 13 places in the alphabet.
- Applying ROT13 twice gives back the original text.
- `tr` replaces one set of characters with another.
- Ranges like `A-Z` and `a-z` make it easy to list letters in `tr`.
- ROT13 is not real security. It only hides text from a quick glance.

## 🎓 Key Takeaway

The important command I learned in Level 11 → Level 12 was:

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

`tr` can decode simple letter-substitution ciphers like ROT13 in one line.

## ➡️ Next

After obtaining the password, I successfully moved from **Bandit Level 11 to Level 12**.

👉 [Level 12 → Level 13](../Level-13/README.md)
