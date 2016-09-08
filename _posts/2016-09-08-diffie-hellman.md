---
title: 40 years of secret key exchange
addons:
  highlightjs: yes
  mathjax: yes
  style_goodies: yes
category: class
tags: cryptography, discrete logarithm, Diffie-Hellman, elliptic curves, isogenies
---

<div style="display:none">
$$
\def\ZZ{\mathbb{Z}}
\def\FF{\mathbb{F}}
\def\Enc{\mathrm{Enc}}
\def\Dec{\mathrm{Dec}}
\def\Sig{\mathrm{Sig}}
\def\Ver{\mathrm{Ver}}
$$
</div>

<style>
hr {
border: none;
height: 2em;
margin: 0;
}
#content .box {
background-color: #fafafa;
border-radius: 10px;
box-shadow: 2px 2px 5px 2px #eee;
overflow: hidden;
margin: 2ex auto;
}
#content .box > * {
margin-left: 1ex;
margin-right: 1ex;
}
#content .box > h4:first-child {
margin: 0 0 0.5ex 0;
padding: 0.1ex 1ex;
background-color: #eee;
}
</style>

# 40 years of secret key exchange

by [Luca De Feo](http://defeo.lu/){:target="_blank"}

[Rentrée des Masters Jacques Hadamard](http://www.fondation-hadamard.fr/fr/formations/rentree-des-masters-et-accueil-des-etudiants){:target="_blank"}

September 8-9, 2016. Paris Saclay.

---
---

## The beginnings of public key cryptography

---

Cryptography, helping lovers since 2000 BC

> O Romeo, Romeo! wherefore art thou Romeo?
> Deny thy father and refuse thy name;
> Or, if thou wilt not, be but sworn my love,
> And I'll no longer be a Capulet. 
{:.cite style="white-space:pre-line"}

**Confidentiality:** Has Tybalt seen the message?

**Authenticity:** Is the message really from Juliet?

**Integrity:** Is the message exactly what Juliet meant to send?

...**and:** Secret sharing, homomorphic encryption, multiparty
computation, plausible deniability, anonimity, proofs of knowledge,
proofs of work, ...

---

### Secret key (symmetric) cryptography

Romeo and Juliet have met in the Capulet's orchard.  Upon falling in
love, they have agreed on a *secret key* **S**.

>It was the nightingale, and not the lark,
>That pierced the fearful hollow of thine ear;
> 
>                        **↓ S**
> 
>Lw#zdv#wkh#qljkwlqjdoh#dqg#qrw#wkh#odun#
>Wkdw#slhufhg#wkh#ihduixo#kroorz#ri#wklqh#hdu
> 
>                        **↓ S**<sup>-1</sup>
> 
>It was the nightingale and not the lark
>That pierced the fearful hollow of thine ear
{:.box style="white-space:pre-line"}

- Known since the ancient times;
- Widely used during war times, played a key role in WWII;
- The *cryptanalytic* efforts of WWII gave birth to the modern computer
  (ever heard of **Enigma**, **Alan Turing**, **Bletchley Park**,
  **Colossus**, ...)
  
  ![](https://upload.wikimedia.org/wikipedia/en/5/5e/The_Imitation_Game_poster.jpg)
  {:.centered}
  
- With a little care, secret key cryptography achieves
  **confidentiality**, **authenticity** and **integrity**.

---

### The birth of public key (asymmetric) cryptography

The modern day Romeo and Juliet have only met on Tinder. They want to
share their most intimate secrets in a **confidential** way, but the
Internet is fraught with pirates, hackers, governments, and tech-savvy
Italian moms wanting to spy on their messages.

**Can Romeo and Juliet establish a *common secret* by chatting on a
  public channel without having ever met before in person?**

---

#### 1976: *New directions in cryptography*

Our modern day Romeo and Juliet: **W. Diffie** and **M. Hellman**

![](https://upload.wikimedia.org/wikipedia/commons/8/88/Diffie_and_Hellman.jpg)
{:.centered}

> We stand today on the brink of a revolution in cryptography.  The
> development of cheap digital hardware has freed it from the design
> limitations of mechanical computing and brought the cost of high
> grade cryptographic devices down to where they can be used in such
> commercial applications as remote cash dispensers and computer
> terminals.  **In turn, such applications create a need for new types
> of cryptographic systems which minimize the necessity of secure key
> distribution channels** and supply the equivalent of a written
> signature.  At the same time, theoretical developments in
> information theory and computer science show promise of providing
> provably secure cryptosystems, changing this ancient art into a
> science.
{:.cite}

---

### The Diffie-Hellman key exchange protocol (abstract version)

Let $$G$$ be a finite cyclic group, noted multiplicatively, generated
by an element $$g∈G$$.

- $$G$$ is abelian,
- Let $$N$$ be the order of $$G$$,


|**Romeo** || **Juliet**
| Picks $$0<a<N$$ at random; || Picks $$0<b<N$$ at random;
| Computes $$A = g^a$$; || Computes $$B = g^b$$;
|| $$—A→$$
|| $$←B—$$
| Computes $$S = B^a = g^{ba}$$ || Computes $$S = A^b = g^{ab}$$
{:.box}

---

Ok, $$S$$ is a common *something*. **But is it a secret?**

**Lady Capulet** is spying on Romeo and Juliet's conversation:

- She knows $$G$$, $$N$$ and $$g$$;
- She sees $$A$$ and $$B$$.

How can she recover $$S$$?

Let's see an [example with $$G=\ZZ/N\ZZ$$]().

---

### *Hard* problems

Let $$G$$ be a cyclic group of order $$N$$.

> #### Discrete logarithm
> Let $$g,A∈G$$, the *discrete logarithm* $$\log_g A$$ is the unique
> integer $$0≤a<N$$ such that $$g^a=A$$.
{:.box}

Discrete logarithm problem (DLP)
: Given $$g,A∈G$$, find $$\log_g A$$.

Computational Diffie-Hellman problem (CDH)
: Given $$g,A,B∈G$$, find $$S$$ such that $$S = A^{\log_g B} =
B^{\log_g A} = g^{(\log_g A)(\log_g B)}$$.

> #### Security reductions
>
> Obviously: **CDH → DLP** (if you can solve DLP, you can solve CDH);
>
> Conjectured: **DLP → CDH**.
{:.box}

---

### Computational security

We cannot hope *discrete logarithm* to be unsolvable for any group. But
we can hope it to take **VERY LOOONG** to solve.

> #### Cost of secret generation
>
> *Square-and-multiply* exponentiation algorithm:
>
> $$a ↦ g^a = (\underbrace{g^{⎣a/2⎦}}_{\text{recursive call}})^2 · g^{a\bmod 2}$$
>
> - $$⎡\log_2 N⎤$$ recursive calls;
> - one or two group operations at each call.
>
> **Total cost:** $$O(\log N)$$ *group operations*.
{:.box}

We say that DLP (or CDH) is *hard* in $$G$$ if no algorithm solves it
in polynomial time in $$\log N$$.

- DLP is clearly **not hard** in $$(\ZZ/N\ZZ, +)$$.
- DLP is at worse exponential in $$\log N$$ (hint: test all exponents
  $$<N$$).
- Advanced algorithms (Baby step-giant step, Pollard
  rho) solve DLP in $$O(\sqrt{N})$$.
- By the Chinese remainder theorem, this can be reduced to
  $$O(\sqrt{p})$$, where $$p$$ is the **largest prime factor** of
  $$N$$ (Pohlig-Hellman).

And if you know a little about complexity theory:

- DLP is in NP.
- If P = NP, then DLP is **not hard** for any group.
- Since we do not know whether P = NP, we do not know any group with
  hard DLP.

... But we can still **conjecture** that DLP is hard for some
groups...

---

### The classical Diffie-Helman protocol

Let $$q$$ be a prime, the *modular integers* $$\ZZ/q\ZZ$$ form a
finite field, also written $$\FF_q$$.

Denote by $$\FF_q^*$$ the *multiplicative group of units* of
$$\FF_q$$.

That is all elements of $$\FF_q$$, except $$0$$, with group operation
given by multiplication.

- $$\FF_q^*$$ is cyclic of order $$q-1$$;
- A generator of $$\FF_q^*$$ can be computed easily using
  Lagrange's theorem.

If $$q-1$$ has a **large prime factor**, the DLP in $$\FF_q^*$$
**seems to be hard**!

[An example]().

---

### Capulet in the middle

It is easy to prove that if CDH is hard, then the Diffie-Hellman key
exchange is **secure against passive adversaries**.

However, if Lady Capulet can intercept messages on Tinder and
manipulate them...

---

|**Romeo** || **Lady Capulet** || **Juliet**
| Picks $$0<a<N$$ at random; || Picks $$0<c<N$$ at random; || Picks $$0<b<N$$ at random;
| Computes $$A = g^a$$; || Computes $$C = g^c$$; || Computes $$B = g^b$$;
|| $$—A→$$ || $$—C→$$
|| $$←C—$$|| $$←B—$$
| Computes $$S = C^a = g^{ca}$$ || Computes $$S = A^c = g^{ac}$$
||| Computes $$S' = B^c = g^{bc}$$ || Computes $$S' = C^b = g^{cb}$$
|| $$⇐S⇒$$|| $$⇐S'⇒$$
{:.box}

---

### Public key encryption

Instead of an *ephemeral key*, Juliet has a *long term* **secret key**
anyone can use to send her private message.

> #### Public key encryption system
>
> Key pair
> : A pair $$(K_p, K_s)$$ (*public key*, *secret key*),
> : $$K_p$$ is publicly known (published on Juliet's Tinder profile).
>
> Encryption algorithm $$\Enc(K_p, m)$$
> : Inputs: public key $$K_p$$ and a *message* $$m$$;
> : Output: a *cyphertext* $$c$$.
>
> Decryption algorithm $$\Dec(K_s, m)$$
> : Inputs: secret key $$K_s$$ and a *cyphertext* $$c=\Enc(K_p, m)$$;
> : Output: the *message* $$m$$.
{:.box}

**Security properties:**

- Only the owner of $$K_s$$ can decrypt cyphertexts encrypted with
  $$K_p$$.
- It is easy to derive a key exchange protocol from a PK encryption one.
- The other direction is harder.

**First ever encryption protocol:** RSA (Rivest, Shamir, Adleman 1977)

- Based on hardness of integer factorization;
- Already known to GCHQ by 1973.


---

### From Diffie-Hellman to PK encryption: the El Gamal protocol (1985)

##### Parameters

- Finite field $$\FF_q$$;
- Generator $$g∈\FF_q$$;

##### Keys

- **Secret key:** random $$0<a<q-1$$;
- **Public key:** $$K_p = g^a$$;


> #### Encryption
>
> **Input:** Public key $$K_p$$, a message $$m∈\FF_q$$;
>
> 1. Pick random $$0≤b<q-1$$;
> 2. Compute $$c_1 = g^b$$;
> 3. Compute $$s = (K_p)^b$$ (*shared secret*);
> 4. Compute $$c_2 = m·s$$;
>
> **Output:** The cyphertext $$(c_1, c_2)$$.
{:.box}

> #### Decryption
>
> **Input:** Secret key $$a$$, a cyphertext $$(c_1,c_2)∈\FF_q × \FF_q$$;
>
> 1. Compute $$s = c_1^a$$ (*shared secret*);
> 2. Compute $$m = c_2 · s^{-1}$$;
>
> **Output:** The message $$m$$.
{:.box}

CDH hard ⇒ El Gamal is secure

---

### Signatures

But how does Juliet know that the message is really from Romeo?

> #### Public key signature system
>
> Key pair
> : A pair $$(K_p, K_s)$$ (*public key*, *secret key*),
> : $$K_p$$ is publicly known (published on Romeo's Tinder profile).
>
> Signature algorithm $$\Sig(K_s, m)$$
> : Inputs: secret key $$K_s$$ and a *message* $$m$$;
> : Output: a *signature* $$s$$.
>
> Verification algorithm $$\Ver(K_p, m, s)$$
> : Inputs: public key $$K_p$$, a *message* $$m$$, a *signature* $$s$$;
> : Output: OK if $$s = \Sig(K_s, m)$$, FAIL otherwise.
{:.box}

**Security property:**

- Only the owner of $$K_s$$ can sign messages for $$K_p$$.
- Security proofs for signature protocols are usually much more
  complicated than for encryption protocols. We will not discuss them.

**Signatures are hard:**

- No automatic way to obtain a signature algorithm from PK encryption;
- RSA signature, introduced together with RSA;
- Signatures from Diffie-Hellman: Schnorr signature (1988), DSA (1991).


---

### Schnorr signatures

##### Parameters

- Finite field $$\FF_q$$;
- Generator $$g∈\FF_q$$;
- A *hash function* $$H: \{0,1\}^* → \FF_q$$;

##### Keys

- **Secret key:** random $$0<a<q-1$$;
- **Public key:** $$K_p = g^a$$;

> #### Signature
>
> **Input:** Secret key $$a$$, a message $$m∈\{0,1\}^*$$;
>
> 1. Pick random $$0≤b<q-1$$;
> 2. Compute $$r = g^b$$;
> 3. Compute $$e = H(m \| r)$$;
> 4. Compute $$s = b - a·e$$;
>
> **Output:** The signature $$(s, e)$$.
{:.box}

> #### Verification
>
> **Input:** Public key $$K_p$$, a message $$m$$, a signature $$(s, e)$$;
>
> 1. Compute $$r = (K_p)^e · g^s$$;
> 2. Compute $$e' = H(M \| r)$$;
>
> **Output:** OK if $$e = e'$$, FAIL otherwise.
{:.box}

---

### Final remarks

- A weaker form of signatures gives *authentication protocols*. These
  can be combined with key exchange protocols to obtain a key exchange
  secure in presence of **active adversaries**.

- All along we have assumed that we trust Tinder to correctly present
  Romeo and Juliet's public keys. But what if Lady Capulet manipulates
  Tinder? Distributing public keys in a safe manner requires a trust
  infrastructure (Public Key Infrastructure (PKI), web of trust,
  ...). This is a complex subject, out of the scope of this course.

---
---

## Modern day key exchange

### Sub-exponential algorithms

### Elliptic curves

### Side channel analysis

### Montgomery ladder

### x-only laws

### Fault attacks, twist security, ed25519?

---
---

## Key exchange in a post-quantum world

---
---

## References
