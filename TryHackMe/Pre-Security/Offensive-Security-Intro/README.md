# TryHackMe – Offensive Security Intro

## Overview

In this room, I explored the FakeBank web application to practice basic web enumeration and understand how hidden functionality can be discovered. Using DIRB, I identified an unlinked endpoint that exposed a deposit form and completed the lab by interacting with the discovered functionality.

---

## Enumeration

After browsing the available pages, I didn't find any obvious functionality that could be used to complete the task. The next step was to enumerate hidden directories using **DIRB**.

```bash
dirb http://fakebank.thm
```

The scan used the default `common.txt` wordlist and tested **4,609** directory names.

Relevant results:

```text
+ http://fakebank.thm/bank-deposit (CODE:200|SIZE:4663)
+ http://fakebank.thm/images (CODE:301|SIZE:179)
```

The `/bank-deposit` endpoint was the most interesting result because it exposed functionality that wasn't available through the application's normal navigation.

### DIRB Scan

![DIRB Scan](images/dirb-scan.png)

*Figure 1: DIRB identified the hidden `/bank-deposit` endpoint.*

---

## Exploitation

Opening the discovered `/bank-deposit` page revealed a form with the following fields:

* Deposit account number
* Deposit amount

For the lab exercise, I submitted:

* **Account:** `8881`
* **Amount:** `2000`

After submitting the deposit request, I returned to the account page and confirmed that the balance had increased. The application then displayed a success message indicating that the lab objective had been completed.

This demonstrated that sensitive functionality exposed through a hidden endpoint could be discovered using directory enumeration. The exercise reinforces that simply hiding a URL is not an effective security control.

### Deposit Form

![Deposit Form](images/deposit-form.png)

*Figure 2: Hidden deposit page.*

### Updated Balance

![Updated account balance after deposit](images/updated-balance.png)

*Figure 3: Updated account balance.*

### Success Message

![Success Message](images/success-message.png)

*Figure 4: Successful completion of the lab.*

---

## What I Learned


- Directory enumeration can reveal functionality that is not linked from the application's interface.
- Discovering hidden pages is often the first step before attempting further testing.
- Sensitive features should be protected with proper authorization instead of relying on hidden URLs.

---

## Tools Used

* Kali Linux AttackBox
* DIRB v2.22
* Mozilla Firefox

---

## References

* TryHackMe – Offensive Security Intro
* DIRB documentation
