# Shell Tricks

## Bash shortcuts

* Ctrl + a: Home
* Ctrl + e: End
* Ctrl + k: Cut to $
* Ctrl + u: Cut to ^
* Ctrl + w: Cut next word
* Alt + d:  Cut previous word
* Ctrl + y: Paste Bash clipboard
* Alt + u: Change word to uppercase
* Alt + u: Change word to lowercase
* Alt + t: Swap current word with previous
* Ctrl + r: Reverse search
* Ctrl + s: Freeze command line
* Ctrl + q: Unfreeze command line
* Ctrl + \: Kill -3 SIGQUIT

## Vi mode in bash

Append `set -o vi` to your `~.bashrc`

## Brace expansions

Useful for copying or moving files with long paths.

```bash
mkdir -p /tmp/first/second/thirs
mv /tmp/first/second/{thirs,third}
```

Or generating files

```bash
cd /tmp/
mkdir -p {1..4}
touch {1..4}/testfile
```

## String operators

## write or append text file

```bash
cat <<_EOF_ > file.txt
one

two
_EOF_

cat <<_EOF_ >> file.txt
one

two
_EOF_
```

## Sort file by column

```bash
cat <<_EOF_ >> file.txt
a 5
k 2
l 9
f 2
g 15
_EOF_
sort -nk 2 file.txt
```

## Size of all directories

```bash
du -shc ./* | sort -h
```

## Get your public IP address

```bash
dig +short myip.opendns.com @resolver1.opendns.com
```

## Read file without comments

```bash
grep -Ev -e "^[[:space:]]*#" -e "^$" /etc/ssh/sshd_config
```

## Trailing whitespaces

Find trailing whitespaces

```bash
grep -nEv "[[:space:]]+$" file
```

Remove trailing whitespaces

```bash
sed -ri 's/[[:space:]]+$//g' file
```

## xargs

Run commands first, second and third in parallel

```bash
echo "first second third" | xargs -d " " -I {} -P 3 {}
```

Get information about all openstack networks

```bash
openstack image list | tail -n+4 | head -n-1 | awk '{print $2}' | xargs -I {} -P5 openstack image show {} | grep size
```

## sed

Can be used in Vi editor eg. `:%s/expr/newexpr/`

### Comment file with sed

```bash
sed -i 's/^/#\ /g' file
```

### Append to every line

```bash
sed -i '$ a text' file
```

### Append after expression

```bash
sed -i '/expr/a text' file
```

### Substitute

```bash
sed -i 's/expr/newexpr/g' file
```

### Double quote keys in json file

```bash
sed 's/\(\<[a-zA-Z]*\)\(:\)/"\1":/g' file
```

## Useful utilities

### ccat

Colorful `cat` https://github.com/jingweno/ccat

```bash
alias cat='ccat'
cat file
```

### ccze

Log colorizer https://github.com/cornet/ccze

```bash
tail -f /var/log/mail.log | ccze
cat file | ccze -A | less -R
```
