---
layout: post
title: "Cryptographic Key Management"
date: 2018-06-04 14:39:29
categories: Encryption
meta: "Lets breakdown types of keys and storage best practises"
---

In my quest for continous learning, two months ago I started studying Cryptography 
a course offered by Standford University on [Coursera](https://coursera.org). My 
objective for taking this subject was to learn how to combine the lessons of 
cryptography as a tool for protecting information and continous decentralized apps 
development. 

It was also my intention to apply the principles of symmetric and asymmetric 
cryptographic operations to provide different security properties to the softwares
I build. The use of cryptographic encryption and authentication framework is fast
becoming a necessity for modern businesses; for example, enterprises are leveraging 
`Public Key Infrastructure` to authenticate users and machines.  S/MIME is proving 
its worth as both an email encryption option and a way to validate email sources 
to counter phishing.

Before detailing how cryptographic frameworks can be used in various business solutions
we need to understand what cryptography is, how it works under the hood and how 
programmers can integrate it into software development. 

## Introduction

Whether you know it or not, as long as you have used any service on the internet 
you have interacted with Cryptographic key management or `encryption` as we will
refer to it for here-on. Encryption is applied to protect electronic communications
and financial transactions, maintain the privacy of sensitive data and it enables
secure authentication and authorization. 

Most, *if not all*, encryption lifecycles on most services start with the generation, 
usage, storage, archiving, and finally the deletion of keys. What are these keys
that we're referencing? A `cryptographic key` is data that specifies the transformation 
of plaintext into ciphertext, and vice versa. Keys are typically designed to be both 
random and reasonably long such that they are difficult to guess. 

### Types of Cryptographic Keys

In general, cryptographic keys are categorized according to their properties and uses. 
The value of any key is equivalent to the value of all the data and/or assets it is 
used to protect. Although there are more than 10 types of keys, today we will be covering
three primary types: 

1. **Symmetric keys** – these are typically used to protect bulk *data-at-rest*. 
   It draws its name from the fact that the same encryption key is used to both 
   encrypt and decrypt the data and is only accessible to authorized users i.e
   anyone with the secret key. 

2. **Asymmetric Keys** – as the name suggests are a pair of keys used for the 
   encryption and decryption of data. Both keys are different but related to 
   each other and are created at the same time. They are referred to as a 
   `public` and a `private` keys:

    * Public Key - this is a key used for data encryption and can be 
      shared publicly.

    * Private Key - this key is used to decrypt the data encrypted
      by the public key. This key must be safeguarded at all times.

    This type of cryptography is commonly known for its usage with asymmetric 
    algorithms like RSA or ECDSA; in these instances, private key storage best 
    practises are employed since anyone with the private key can impersonate 
    the key owner to decrypt private data, gain unauthorized access to systems 
    or generate a fraudulent digital signature that appears authentic.

    <figure>
      <img src="/blog/wp-content/uploads/2018/06/key-management.png" alt="" />
      <figcaption>Illustration: symmetric & asymmetric keys</figcaption>
    </figure>

3. **Hash Keys**  – these are used to safeguard the integrity and authenticity of 
   data and transactions with algorithms like HMAC-SHA256. If you have used Bitcoin,
   other cryptocurriencies or blockchain in general then you are familiar with a hash. 

   Similar to asymmetric encryption, private hash keys should not be disclosed, or 
   lost as mal-intended users of this key can impersonate transaction originators to 
   modify, falsify or create incorrect data/transactions that recipients will believe 
   to be authentic. 

## How Cryptographic Encryption Works

So far in this post we have covered what encryption is and the most common types of keys
used for data protection. Without going into the historic details of encryption we will
now dive deep to understand how modern encryption systems actually work.

### Symmetric Encryption Systems

A historical example of symmetric encryption used by Julius Caesar: the `Caesar cipher`
is a method of shifting the alphabet by three characters. In this case the encryption 
and decryption key is the number 3. The Caesar cipher is a weak form of symmetric 
cryptography since anyone with this knowledge could decipher any message between Ceaser 
and his generals.

Thankfully, encryption has come a long way since the Caesar cipher. Using amazing math 
and the help of computers, symmetric-key algorithms today can be divided into [stream ciphers](https://en.wikipedia.org/wiki/Stream_cipher) and block ciphers. Stream ciphers encrypt bits of a message one at 
a time. In a synchronous stream cipher, a stream of pseudo-random digits is generated 
independently of the plaintext and ciphertext messages, and then combined with the 
plaintext (to encrypt) or the ciphertext (to decrypt). There’s a lot of different symmetric 
algorithms one can choose from including ***Twofish***, ***Serpent***, ***TDES***, and ***IDEA***.

To take it further, lets breakdown how an authorized user can access encrypted data:

  1. A user requests access to encrypted data.
  2. The client `Key Manager` API receives a `Data Encryption Key` retieval request 
     from a database or application.
  3. Here, once the client Key Manager API `certificate` has been verified, the Key 
     Manager must send `its certificate` to the `Key Manager API` for authentication
     and acceptance. 
  4. A `secure TLS connection` is opened between the client KM API & the KM once the 
     certificates have been accepted.
  5. The KM API sends a decrypted `Data Encryption Key` (*that was received over the encrypted TLS session*) 
     to the database or application.
  6. A DEK cached in a `temporary secure memory` lets the database or application `send` 
     `the plaintext` information to the user. 

Symmetric cryptography however doesn’t address several issues for example:

  * How does the sender send the symmetric decryption key to the 
    recipient without someone spying on that conversation too? 

  * What if the sender and recipient are physically far away from 
    each other?

### Asymmetric Encryption Systems

The critical advantage in an asymmetric key system is that users never need to send a 
copy of their keys to each other. The `public key cryptography` allows someone to send 
their public key in an open, insecure channel. This system also prevents third party 
`intermediaries` — *such as the email service providers, Internet service providers, 
and those on their networks* — from seeing the message content. Theses intermediaries 
are restricted to `metadata`. 

In these systems, **users can encrypt and send messages to `owners` of a public key while also using their `private key` to decrpyt messages they receive**. Asymmetric encryption uses different keys for 
encryption and decryption - and that's one of the major benefits of this encryption 
system. We never need to send secret keys or passwords over insecure network channels.

Another one of those benefits of this system is that it boasts a simple encryption-to-decryption-to-encryption
process that happens in quick succession:

  1. It starts once the `Sender's certificate` has been verified. The 
     `recipient` then sends `their certificate` to the sender for 
     `authentication and acceptance`.
  2. Once the sender has received the recipients `public key` they create 
     a `one-session-use` symmetric encryption key and encrypts the `message`.
  3. The `symmetric key` is encrypted with the senders `public key` and 
     sent to the recipient.
  4. The `message` is received as a packet and is `decrypted` by the recipients 
     private key - the recipient then decrypts the message with the `one-session-use` 
     symmetric key. 

Now that we know how each encryption system works I want to cover the very vital topic 
of key storage options & best practises. With an ever-increasing number of keys to protect, 
and an ever-increasing value of data being protected by those keys, how do we address the 
many threats that can result in a key being compromised. 

## Key Management - the Risks & Mitigation

Best practice tells us that a private key should remain secure and, well…private! Should 
anyone get a hold of it, depending on the certificate type, they could create phishing websites 
with the organization’s certificate in the address bar, they could authenticate to corporate 
networks by impersonating the owner, they could sign applications or documents as the owner, and 
even read encrypted emails.

In this section, we’ll discuss the options for private key protection and storage - but before we 
can talk about security we need to know the possible threats to key management. 

### Key Management - the Risks

We know a single compromised key could lead to a massive data breach with consequential reputational 
damage, punitive regulatory fines or loss of investor and customer confidence. Yet, the ever-present 
vulnerabilities in modern computing systems, and with growing sophistication of cyber attacks, it has 
never been more important, nor more challenging, to keep cryptographic keys safe and secure. 

Here are some of the major threats to consider while managing the safe storage of keys:

  * **Usage of Keys** - How keys are used across various databases or applications
    can impact how safe the keys remain. For instance, `Improper re-use of keys` in 
    certain circumstances can make it easier for an attacker to crack the key.

    Without the proper `rotation of keys` i.e. if a key is over-used then it makes 
    the key more vulnerable especially when using older symmetric algorithms;

  * **Inappropriate & Inadequate Protection** - This is simple, keys should never
    be `stored alongside the data` that they protect as any data corruption is likely 
    to compromise the key also.

    Even keys stored only in server memory `should be encrypted` whenever stored 
    and only be made available in unencrypted form within a secure, offline tamper-
    protected environment.

  * **Insecure Movement of Keys** - When sharing symmetric keys on a system, the 
    key should be `split into multiple components` that must then be kept separate 
    until being re-entered into the target system (and then the components are destroyed). 
    Without this extra caution, keys are at risk of being publicised.

  * **Non-Desctruction of Keys** - Keys should be `securely deleted` once they 
    have expired, unless explicitly required for later use (e.g. to decrypt data). 
    This removes the risk of accidental compromise at some future date.

  * **Manual Key Management** - The use of a manual key management processes,
    using `paper` or `inappropriate` tools such as spreadsheets and accompanied 
    by manual key ceremonies, can easily result in human errors that often go 
    unnoticed and may leave keys highly vulnerable.

There are other physical environment security threats that need to be considered a threat 
and factored in the security plan this include ***physical access controls***, ***fire*** 
***safety***, ***utilities failure***,
***mobile device management*** and even ***structural integrity***.

### Securing Encryption Key Managers

Now that we have hightlighted ways to the secure the physical environment in which the key 
manager is housed we will naturally turn to securing the key manager itself with a hardware 
security module. Some of this hardware modules are:

  * **Cryptographic Tokens** - With cryptographic hardware, the key is generated on 
    the hardware itself and is not exportable. This means the private key never leaves 
    the device, making it much more difficult for someone to compromise. 

  * **Hardware Security Module** - This is typically a server with different levels 
    of security protection or “hardening” of the module with tamper evident/resistant 
    screws and locks along with the highest sensitivity to “tamper detection/response 
    circuitry that wipes out all sensitive data.

  * **Virtual Instances** - In many cases, a virtual key manager can be downloaded
    from a vendor in a matter of minutes and deployed in a virtual environment. The 
    downside, of course, is that by it’s nature of being virtual with no set physical 
    components, a virtual key manager’s software can only be FIPS 140-2 compliant, 
    but not validated. 

The key storage options discussed above are somewhat traditional methods that have been 
used for years. However, as more devices come online they need to authenticate and communicate 
securely. We will continue turning to PKI-based solutions, which in turn bring about new 
considerations, requirements and technologies for protecting private keys.

## Need for Algorithmic Key Encryption 

So now that we understand the risks and mitigations that come with encryption key 
management, why is algorithmic key encryption important? Well encryption has been 
around for millenniums but in 2000 when `Advanced Encryption Standard` (AES) algorithm 
was formally adopted as the standard encryption algorithm it introduced a `single key use` 
as a part of the encryption process.

The key can be 128 bits (16 bytes), 192 bits (24 bytes), or 256 bits (32 bytes) in 
length. Given that the fastest computer would take billions of years to run through 
every permutation of a 256-bit key, AES is considered an extremely secure encryption 
standard. Regardless, its advised to maintain a robust encryption key management 
strategy even after deploying an encryption. 

<figure>
  <img src="/blog/wp-content/uploads/2018/06/aes-encryption.png" alt="" />
  <figcaption>Source: Wikipedia</figcaption>
</figure>

## Conclusion

Private key storage `shouldn’t be a dark art`. Any key management system that
utilizes HSM to generate keys will not only help protect your keys, it will also boost 
efficiency, reduce reliance on highly-skilled personnel, and simplify achieving, 
maintaining and demonstrating compliance with a multitude of standards and regulations 
such as GDPR.


