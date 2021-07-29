---
title: 'Security'
date: 2019-02-11T19:30:08+10:00
weight: 5
summary: Policy and security measures of Dhak.
---

- [Policy of Dhak](#policy-of-dhak)
- [Password generation works](#password-generation-works)
- [Good points](#good-points)
- [Bad points](#bad-points)
- [Summary](#summary)

---

## Policy of Dhak

I created Dhak under the policy **not to keep confidential information**.

I said that Dhak is a password manager, but its essence is a _function_. This means that if you input the same value, the output will always be the same.  
By doing this, Dhak practically manages passwords by not keeping any confidential information.

## Password generation works

Basically, Dhak generates passwords using **BCrypt**. BCrypt is a kind of hash algorithm and calculates the hash from the target and salt (a random string which is added at hashing).

Because of the way Bcrypt works, the target must be 72 bytes or less. So first, Dhak generates the binary hash with SHA-512 from the received passphrase and title.

![make binary hash](/dhak_docs/images/works_1.jpg)

The size of SHA-512 hash is 128 bytes as a hex string, but as a binary, it becomes 64 bytes.

Next, Dhak takes the integer hash code from the obtained binary hash and makes a salt from it. Then, Dhak generates the string hash from the two values by using BCrypt [[1]](#1).

![make string hash](/dhak_docs/images/works_2.jpg)

Finally, Dhak cuts the hash to a specified length and randomly replaces a character to a symbol [[2]](#2).  
Thus, the password is completed [[3]](#3).

![make password](/dhak_docs/images/works_3.jpg)

## Good points

The biggest benefit of managing passwords functionally is that **there is no possibility to leak information**.  
What Dhak does just calculates a password from getting values, so it does not need password retention or passphrase verification. Since Dhak does not keep confidential information, there is no leakage of information essentially.

Also, another benefit of being a function is that **you do not need to sync multiple devices.**.  
In these days, it is common to have multiple digital devices, such as a computer, a smartphone, and so on. The problem under these situation is how to manage passwords between them. As a solution for it, for example, some are to save passwords by using a cloud service and to sync them, but others are to share them by using an USB flash memory manually.

Dhak itself does not keep information, so it cannot take the above. However, Dhak can share passwords across multiple devices without doing anything special like that. Dhak has the system to return the same password from the same passphrase and title on any device, so it dose not need synchronization in the first place.

## Bad points

Of course, Dhak has some bad points.

The first is that **Dhak is slightly inflexible.**  
For example, you cannot manage your current passwords with Dhak because it is a password calculator. If you switch to Dhak, you will need to update your existing passwords with Dhak's ones.  
Also, it is difficult to change a password once Dhak has generated it. If you want to change your password for some reason, you will need to change the input value, such as adding the version to the title.

And the second, this is the biggest drawback, is that **if the hash value used for the password is cracked, other passwords can be exposed in chains.**  
Hashing is a one-way function, but it is possible to identify the value of the input source using techniques such as rainbow table attacks. Once the passphrase is known by these methods, other passwords can be easily cracked.  
To counter this, Dhak uses BCrypt to generate passwords, which a strong hashing algorithm that is used in a great many situations.  

## Summary

The critical differences between Dhak and a typical password manager are as follows:

- Typical password manager
  - Pros:
    - High flexibility.
  - Cons:
    - Risk of information leakage.
    - In some cases, synchronization between devices is troublesome.
- Dhak
  - Pros:
    - Resistant to information leakage.
    - No need to sync multiple devices.
  - Cons:
    - Possibility of a single password exposing other passwords.
    - Low flexibility.

---

<a name="1"></a>
\[1] Since the hash will yield an irregular string, there is a slight possibility that BCRypt will generate an insecure password (e.g. only numbers, only letters, etc.). In that case, add a random integer value to the target, hash it, and repeat the process until a secure password is generated.

<a name="2"></a>
\[2] If symbols are used, the number of symbols in the password is randomly adjusted from 1 to one-third of the password length. This "one-third" comes from the ratio of the 32 symbols out of the 94 characters that can be entered on a typical keyboard.

<a name="3"></a>
\[3] For the convenience of getting the true hash, it is processed in reverse order.

{{< pager
  prevHref="/configure"
  prevTitle="Configuration"
  nextHref="/installation"
  nextTitle="Installation"
>}}
