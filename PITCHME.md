---

### How to hide secret data in github

We MUST NOT add secret data to git repository

(But sometimes, we want to share it)

---

### Technology - GPG

Gnu Privacy Guard

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

### List keys in your local keyring


```bash
$ gpg --list-keys y.takahara@gmail.com
pub   rsa2048 2017-06-22 [SC] [expires: 2019-06-22]
      983608495645E4172F2D60EAE693F4D73438BE8E
uid           [ultimate] Yoshihiro Takahara <y.takahara@gmail.com>
sub   rsa2048 2017-06-22 [E] [expires: 2019-06-22]
```

---

### Exchange GPG key - Pattern 1

> Jiro want to import Taro's key to his GPG keyring.

+++

#### 1. Taro exports his public key like this:

```bash
$ gpg --armor --export taro@wakumo.vn
-----BEGIN PGP PUBLIC KEY BLOCK-----

mQENBFlusgYBCADUcwVxK9kBC9Dd14wsIVmDEtMJ+XSsN+pxonStV/Ouo8124oID
bB3v4w6NmlW4+dLZjAVQoVQ/mrrhYUo3cQWUARxycLho6HnuiQLbAnLU7UFO+dT0
egEWy2MmWz5f3vBInT0j84AdepW4xV2ppn/g3mM1mzVmj9H8kfnnq8BSFH1c7oMf
x97B4LdlndG+i+3EGgu+WUrf30VHnGqZykp4jDs6nOWqXNRCjFzLf6P/JNlcoWU9
bdaURD44q4kM19FHR7CZPsTVY8v5HHz0QRr0rQDQMiW0lt8ytgL1r+gCwptp+ZEr
waqWiiKcVmtQgqXPdg5rbMKhw1mnhGtjv+z3ABEBAAG0JFlvc2hpaGlybyBUYWth
aGFyYSA8dHVtZkB3YWt1bW8uY29tPokBVAQTAQgAPhYhBK3UocW7mG+mqqvSo3Qv
6yAGuZ8lBQJZbrIGAhsDBQkDwmcABQsJCAcCBhUICQoLAgQWAgMBAh4BAheAAAoJ
EHQv6yAGuZ8l6HMH/0AhXtNZv8dHDjHO8dOWQBeh9dUrifwU1lBo8POSuXV9Ya79
IjxGHyDMmGpzETIZfM8fvVxfS9lwQp8h+nT47527aVf90/XSNVIOR9IeKnEv1OOk
TaqIKCC0pYUjZAxfpQAgG2VQyfqKeydmeDC7tf2jdAV41Xibe9T70nGovxjXN2ut
SPDiQymo51TYKsGKn6cRazhlZd+i4k1ES9ofpmrMRnK40H27hjm6oGz+QpLsY7SE
HOMyVYabEGi3lZmeCND3qkaJAQdeUdaMFdg+/l6ffUDPB7p+ERWODnka0w66h6/2
grDKqKUSf754kXF9wkYQ34hIzCXl1GjiiQ/gw0e5AQ0EWW6yBgEIAMfPwrMJSu7T
9vCsdSpNMVNCs6w+K92JYspYTkhcEppWxUlGNO0eq7XKsokvPzsmz4mPOE6OITsE
lY+mZt0xq7MLMWKy1EuKNw4W56JqJwE6z3uh0TlilhF8SJSBX2mXDjKHxgi3gtss
RRtEowZ9/GxoNQ00IknQmSZUSPuE8DrlriznlmHTZ+n9xON4IXLTIecLux3y9RGV
b6Volu6yk5UZz7xxb1OE9DL8ouEzxn6R6b5ZAnKr3U0fT3r9jITnwTmfKeEUyFE6
8FA2lnNQrfRsHEf5chya4vJrDdAxfVIIrPUKiadgRAteiHkKG/tjEXbFiFVgbfL2
vkI7Nmk3unsAEQEAAYkBPAQYAQgAJhYhBK3UocW7mG+mqqvSo3Qv6yAGuZ8lBQJZ
brIGAhsMBQkDwmcAAAoJEHQv6yAGuZ8l7L8H/16Iw267F+rWtLgqQFQCs6as4KWQ
a+ihq1Vk75YmHw3yu9hFJ+MU5i4Z3HJ/KMktj+X2nVEoduJgStffiLjIeaNmjPzR
FqrPCDMfTfnU3iasI4b3lqc7u+W5WcxdLnIOFmpOeX/qIer31PeVX/1Js8wpAizz
usjNl8L0TfKET5C3+oP5TPdOtGV711yhmV7UEZY+VEhMPD+obfFZE5IRQSpAoiqt
8BsOHrOb/JlgTEtiC5pkKjZS7o4IB0SwbKR1nalX+H9gIEAVclbj9cMNYHKBNjVZ
WIZlpBv2+0OHMQ43C+YwNljffxEn3chhBDsLP6VGwjW/FUYp1bDzHHsYwp8=
=ZISe
-----END PGP PUBLIC KEY BLOCK-----
```

#### 2. Copy and Paste to Jiro (via Email, Skype, Slack)

+++

#### 3. Jiro imports this GPG public key:

save to file `taro.pub` then:

```bash
$ gpg --import taro.pub
```

---

### Exchange GPG key - Pattern 2

#### 1. Taro send to public keyserver (pgp.mit.edu)


```bash
$ gpg  --send-keys --keyserver pgp.mit.edu {KEY-ID}
```

like this:

```bash
$ gpg  --send-keys --keyserver pgp.mit.edu 983608495645E4172F2D60EAE693F4D73438BE8E
```

And notify {KEY-ID} to Jiro.

+++

#### 2. Jiro import Taro's key from keyserver


```bash
$ gpg --keyserver pgp.mit.edu --recv-keys {KEY-ID}
```

like this:

```bash
$ gpg --keyserver pgp.mit.edu --recv-keys 983608495645E4172F2D60EAE693F4D73438BE8E
```

+++


> *Warning*
> Don't trust just only email!
> Anyone can upload keys to keyserver as someone.
> Verify KEY-ID carefully.

---

### How to hide secret data in github

+++

### Solution - git-crypt

> https://www.agwa.name/projects/git-crypt/

+++

---

### Workflow - Get and Modify

1. clone  (as usual)
2. unlock <- add
3. edit file (as usual)
4. stage&commit (as usual)
5. push   (as usual)

+++

### Workflow - Add file

Get and Modify

1. clone  (as usual)
2. edit .gitattribute <---
3. stage  (as usual)
3. commit (as usual)
4. push   (as usual)

+++

### Install git-crypt

```bash
brew install git-crypt
```

+++

### Quick start (Initial setup)

```bash
cd {your git repo}
git-crypt init
```

+++

### Add public key

```bash
git-crypt add-gpg-user {{ KEY ID }}
```

like this:

```
git-crypt add-gpg-user ADD4A1C5BB986FA6AAABD2A3742FEB2006B99F25
```

+++

### git-crypt: GPG error: Failed to encrypt

```bash
$ git-crypt add-gpg-user D381FF9E23DAC5B974ADFB40EAB10F4444444B14
gpg: 86ADD9AF9241B449: There is no assurance this key belongs to the named user
gpg: [stdin]: encryption failed: Unusable public key
git-crypt: GPG error: Failed to encrypt
```


```
$ gpg --list-keys D381FF9E23DAC5B974ADFB40EAB10F4444444B14
pub  rsa2048/EAB10F4444444B14
     created: 2017-07-21  expires: 2019-07-21  usage: SC
     trust: unknown       validity: unknown
sub  rsa2048/86ADD9AF9241B449
     created: 2017-07-21  expires: 2019-07-21  usage: E
[ unknown] (1). Vo Dong Nhut <nhutvd@wakumo.vn>
```

### How to trust

```bash
$ gpg --edit-key <KEY_ID>
```

then:


```
gpg> trust
  1 = I don't know or won't say
  2 = I do NOT trust
  3 = I trust marginally
  4 = I trust fully
  5 = I trust ultimately
  m = back to the main menu

Your decision? 4
Do you really want to set this key to ultimate trust? (y/N) y
```

```
$ gpg --list-keys D381FF9E23DAC5B974ADFB40EAB10F4444444B14
pub   rsa2048 2017-07-21 [SC] [expires: 2019-07-21]
      D381FF9E23DAC5B974ADFB40EAB10F4444444B14
uid           [ultimate] Vo Dong Nhut <nhutvd@wakumo.vn>
sub   rsa2048 2017-07-21 [E] [expires: 2019-07-21]
```

https://stackoverflow.com/questions/33361068/gnupg-there-is-no-assurance-this-key-belongs-to-the-named-user


+++

### Clone and Unlock

```bash
$ git clone { git url }
$ git crypt unlock
```

+++

### How to add secret file


Create .gitattributes file

```bash:.gitattributes
secret.txt filter=git-crypt diff=git-crypt
```

We can use wild card like this:

```bash:.gitattributes
secret.txt filter=git-crypt diff=git-crypt
*.key filter=git-crypt diff=git-crypt
```

+++

Then stage & commit

```bash
git add secret.txt
git commit
```

> *Warning*
> EDIT `.gitattributes` BEFORE stage (git add) secretfiles to git.

+++

```bash
git push origin master
```

All Remote files are encrypted.

---

#### Do you have any questions?
