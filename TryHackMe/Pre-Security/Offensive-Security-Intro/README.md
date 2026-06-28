# TryHackMe – Offensive Security Intro

## Overview

This room introduces the basics of offensive security through a vulnerable web application called **FakeBank**. The objective was to enumerate the application, discover hidden functionality, and understand how exposed endpoints can lead to unintended actions.

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

**Evidence**

* Screenshot: DIRB scan showing discovered endpoints.

---

## Exploitation

Opening the discovered `/bank-deposit` page revealed a form with the following fields:

* Deposit account number
* Deposit amount

For the lab exercise, I submitted:

* **Account:** `8881`
* **Amount:** `2000`

After submitting the request and returning to the account page, the application reflected the updated balance and displayed a success message indicating that the operation had completed successfully.

This demonstrated that functionality intended to be hidden was still reachable once the endpoint had been discovered through enumeration.

**Evidence**

* Screenshot: Deposit form
* Screenshot: Updated account balance
* Screenshot: Success message

---

## What I Learned

* Enumeration is an essential first step during web application testing because hidden endpoints are often not linked from the user interface.
* Automated tools like DIRB can quickly identify directories that expand the application's attack surface.
* Sensitive functionality should never rely on obscurity. If an endpoint exists, it should be protected with appropriate server-side security controls regardless of whether users can navigate to it directly.

---

## Tools Used

* Kali Linux AttackBox
* DIRB v2.22
* Mozilla Firefox

---

## References

* TryHackMe – Offensive Security Intro
* DIRB documentation
