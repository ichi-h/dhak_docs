---
title: "Usage"
date: 2019-02-11T19:27:37+10:00
weight: 3
summary: Basic usage of Dhak.
---

- [Example](#example)
  - [0: Prepare your passphrase](#0-prepare-your-passphrase)
  - [1: Basic usage](#1-basic-usage)
  - [2: Use options](#2-use-options)
  - [3: Use preset](#3-use-preset)
  - [4: Dangerous password generation (deprecated)](#4-dangerous-password-generation-deprecated)
- [Syntax of Dhak](#syntax-of-dhak)
  - [Command](#command)
  - [Title](#title)
  - [Preset](#preset)
  - [Options](#options)

---

## Example

### 0: Prepare your passphrase

Dhak requires your passphrase when you get a password. This is like a master key in a typical password manager.

A passphrase must be 12 character or more, and contain one lower-case, upper-case and number at least.  
If you forget it, you will never be able to get the same password again, so try to use what is hard to forget and hard to guess.

I recommend you to use some passphrase generators, like [Secure Passphrase Generator](https://untroubled.org/pwgen/ppgen.cgi).

Here, I will use the passphrase "Norm's72Swished50Sideshow" as an example.

### 1: Basic usage

Dhak generates passwords from your original passphrase and the name of the service.  
The following command is the basic usage of Dhak.

```shell
dhak Github
Passphrase: # (Enter "Norm's72Swished50Sideshow")
Password was copied to clipboard!
```

Then, the value of the clipboard is "**(OZshheENa\‘y+g!1p2W**".

The default settings of the password generation are:

- Password length: 20
- Symbols: !"#$%&‘()*+,-./:;<=>?@\[\\]^_`{|}~
- Algorithm: 2b
- Cost: 10

For the details of the above, see [Options](#options).

### 2: Use options

You can specify the generation settings in detail by using options.

```shell
dhak Github --len=40 --sym='' --cost=15
Passphrase: # (Enter "Norm's72Swished50Sideshow")
WARNING: The password does not contain any symbols.
Password was copied to clipboard!
```

And the result is "**CZUFWjezYP4q61039tlOYewgazshrhRKCvM2NiL2**". It's so different from before!

### 3: Use preset

Typing that stuff like the above every time makes you very bothered, so you can add a preset to ~/.dhakrc file, like:

```
{
  "presets": {
    "new_preset": {
      "password_length": "40",
      "symbols": "",
      "cost": "15"
    }
  }
}
```

And run the following command.

```shell
dhak Github new_preset
Passphrase: # (Enter "Norm's72Swished50Sideshow")
WARNING: The password does not contain any symbols.
Password was copied to clipboard!
```

Then, you can get the same password "**CZUFWjezYP4q61039tlOYewgazshrhRKCvM2NiL2**" as before.

For details, see [Configuration](/docs/configure) section.

### 4: Dangerous password generation (deprecated)

If you add the "-f" or "--force" option, you can force Dhak to generate an insecure password.

```shell
dhak Github --len=6 --sym='' --force
Passphrase: # (Enter "Norm's72Swished50Sideshow")
WARNING: The password length "6" is short. It should be 12 or more.
Password was copied to clipboard!
```

The password is "**qOZsMh**". Hmm...

You may use this option, for example, when you sign up a service which accepts only very short passwords.  
Conversely, **do not use use it unless you have those reasons.**

## Syntax of Dhak

```
dhak [-h, --help] [-v, --version] <title> (<preset>) [options]
```

### Command

- -h, \--help
  - Display the help.
- -v, \--version
  - Display the version.

### Title

The name of the service.

### Preset

The pre-prepared setting for password generation (you can add a preset in ~/.dhakrc).

### Options

Specify additional functions as needed.

Dhak will use settings of options in preference to settings of presets.  
The following values of the options mean the default values in this app. If you omit a option, Dhak will use them.

- -d, \--display
    - Display the password in the terminal.
- -f, \--force (deprecated)
    - Forcibly generate a password which may be insecure, such as a password whose length is less than 12 or which has only lower-case.
    - <u><b>YOU SHOULD USE THIS OPTION AS LITTLE AS POSSIBLE.</b></u>
- \--len=20
    - Set a password length.
    - If it is less than 12, you cannot generate the password basically.
- \--sym=!"#$%&‘()*+,-./:;<=>?@\[\\]^_`{|}~
    - Set symbols used the password generation.
    - You can use any symbols except lower-case, upper-case and numbers.
    - You will get passwords without symbols if you keep this empty like `--sym=''`.
- \--algo=2b
    - Set an algorithm of BCrypt.
    - You can use "2", "2a", "2y" and "2b ", but <u>you do not have to change it unless something unexpected happens.</u>
- \--cost=10
    - Set a cost of BCrypt. It must be between 4 and 31.
    - The cost is an exponent, and the actual round of stretching is 2^n.
    - The higher the cost, the more secure the password will be generated, but also the higher the computational load.

{{< pager
  prevHref="/installation"
  prevTitle="Installation"
  nextHref="/configure"
  nextTitle="Configuration"
>}}
