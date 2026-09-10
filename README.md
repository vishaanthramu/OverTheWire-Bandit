# OverTheWire-Bandit
Reflections on my experience of OverTheWire Bandit wargame and Linux security basics.

## 🐧 About

[Bandit](https://overthewire.org/wargames/bandit/) is a beginner wargame by OverTheWire that teaches Linux commands and basic security concepts. Each level hides the password for the next level, and I write down how I found it and what I learned.

> ⚠️ Passwords are not included in these write-ups. Only the method and commands are shown.

## 📚 Levels

| Level | Write-up | Main commands |
|---|---|---|
| Level 0 | [SSH login](Level-00/README.md) | `ssh` |
| Level 0 → 1 | [Reading a file](Level-01/README.md) | `pwd`, `ls`, `cat` |
| Level 1 → 2 | [A file named `-`](Level-02/README.md) | `cat ./-` |
| Level 2 → 3 | [Spaces and dashes in a filename](Level-03/README.md) | quotes, `./`, `--` |
| Level 3 → 4 | [Hidden files](Level-04/README.md) | `cd`, `ls -a` |
| Level 4 → 5 | [Finding the human-readable file](Level-05/README.md) | `file` |
| Level 5 → 6 | [Finding a file by its properties](Level-06/README.md) | `find -size -type` |
| Level 6 → 7 | [Searching the whole server](Level-07/README.md) | `find -user -group`, `2>/dev/null` |
| Level 7 → 8 | [Searching inside a big file](Level-08/README.md) | `grep` |
| Level 8 → 9 | [The line that appears once](Level-09/README.md) | `sort`, `uniq -u`, `\|` |
| Level 9 → 10 | [Text inside a binary file](Level-10/README.md) | `strings`, `grep` |
| Level 10 → 11 | [Base64](Level-11/README.md) | `base64 -d` |
| Level 11 → 12 | [ROT13](Level-12/README.md) | `tr` |
| Level 12 → 13 | [Hexdump and repeated compression](Level-13/README.md) | `xxd -r`, `file`, `gzip`, `bzip2`, `tar` |
| Level 13 → 14 | [Logging in with an SSH key](Level-14/README.md) | `scp`, `chmod`, `ssh -i` |
| Level 14 → 15 | [Sending data to a port](Level-15/README.md) | `nc` |
