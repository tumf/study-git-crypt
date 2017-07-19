---

### How to hide secret data in github


---

たとえそれがプライベートなリポジトリであっても。
gpg


---

### Technology - GPG

gnu privacy guard

+++

### install GPG

```bash
brew install gpg
```

+++

### Create your key

```bash
gpg --generate-key
```

+++

### list keys

```
$ gpg --list-keys
/Users/tumf/.gnupg/pubring.gpg
------------------------------
pub   rsa4096 2014-10-28 [SC]
      409B6B1796C275462A1703113804BB82D39DC0E3
uid           [ unknown] Michal Papis (RVM signing) <mpapis@gmail.com>
uid           [ unknown] Michal Papis <michal.papis@toptal.com>
uid           [ unknown] [jpeg image of size 5015]
sub   rsa4096 2014-10-28 [S] [expires: 2019-03-09]
sub   rsa2048 2015-11-02 [E]

pub   rsa2048 2017-06-22 [SC] [expires: 2019-06-22]
      983608495645E4172F2D60EAE693F4D73438BE8E
uid           [ultimate] Yoshihiro Takahara <y.takahara@gmail.com>
sub   rsa2048 2017-06-22 [E] [expires: 2019-06-22]
```

+++

### add key

gpg --armor --export your_email@address.com

gpg --search-keys y.takahara@gmail.com

```bash
$ gpg --import name_of_pub_key_file
```
+++

### How to send my public key to friend

1. Use text
2. Key server

gpg  --send-keys --keyserver pgp.mit.edu 983608495645E4172F2D60EAE693F4D73438BE8E
> *Warning* Don't trust email

---

### git-crypt

https://www.agwa.name/projects/git-crypt/

---

### Workflow

1. clone
2. unlock <-
3. commit
4. push

---

### Install git-crypt

```bash
brew install git-crypt
```

+++

### Quick start

```bash
cd {your git repo}
git-crypt init
```

### Add public key

```
git-crypt add-gpg-user USER_ID
```

> git-crypt add-gpg-user ADD4A1C5BB986FA6AAABD2A3742FEB2006B99F25

### Clone and Unlock

```bash
$ git clone { git url }
$ git-crypt unlock
```

### How to add secret file


Create .gitattributes file

```.gitattributes
secret.txt filter=git-crypt diff=git-crypt
```



Then add to git

```bash
git add secret.txt
```

> *Warning* Setup `.gitattributes` BEFORE stage secretfiles to git.

+++
