---
layout: post
title: Public key encryption with keyword search
---

This is an attempt to convey a method to do encrypted search to non-cryptographers. Please excuse the lack of rigour for which I will compensate at the end of the article.

Assume you have a public key encryption system.

Bob is sending an encrypted message to Alice using Alice's public key

![alice1](/post_images/alice1.jpg)

Alice wants to delegate some checking of messages to Eve.  She wants Eve to check if the encrypted message is her favourite keyword "Nice", but she does not want Eve to know she is looking for "*Nice*".

How can Eve verify that "*8Ev7*" is actually "*Nice*" in encrypted form ? What you need here is an auxiliary string called a **trapdoor** which Eve can use to verify the equality.   

![alice2](/post_images/alice2.jpg)

Encrypting the trapdoor produces the original ciphertext, allowing Eve to verify equality.

![alice3](/post_images/alice3.jpg)

The trapdoor can be produced using a <a href="https://en.wikipedia.org/wiki/Bilinear_map">bilinear map</a> which enables two different ways of producing same ciphertext.

A bilinear map is a function of two variables *f(x, y)* satifying this condition

![eqn1](/post_images/firsteqn.gif)

Let "*x*" be the text to be encrypted.  The encrypted text will be generated by applying f(x, y) where "*y*" is the key combination (g^{ra}) as shown below.

![pic1](/post_images/pic1.jpg)

Next, you have to generate two more items
1. an auxiliary string called the **trapdoor** in the form of original text raised to power of (*Alpha*)
2. a mangled public key, produced from original public key by raising to power of (*1/Alpha*)

as shown in the lower shaded circle

![pic2](/post_images/pic3.jpg)

Now by the property of a bilinear map, the exponentiation by (*Alpha*) and (*1/Alpha*) cancels as shown here

![pic3](/post_images/pic2.jpg)

As a result, we now have two ways of producing the same encrypted text.

A third-party which has the trapdoor "*Vgzv*" can test if the encrypted text ("*8Ev7*") is the string being searched for.

This is intuitively the cryptographic construction given by Boneh, et al in Sec 3.1 of their paper[1] 

![pic4](/post_images/peks_paper.png)


I have played fast and loose here to provide intuition.  Refer to original paper for rigorous explanation.

## How to produce bilinear maps ?  

I am not going into that here. You have to use Weil pairings or Tate pairings over elliptic curves.  

## Diagram of the full construction

There are two more hash functions which come into play in the complete scheme.

![pic4](/post_images/full_scheme.jpg)

## Reference

1. Boneh, et al.  Public Key Encryption with keyword Search.  <a href="https://crypto.stanford.edu/~dabo/pubs/papers/encsearch.pdf"> https://crypto.stanford.edu/~dabo/pubs/papers/encsearch.pdf </a>
2. Alfred Menezies.  An introduction to pairing-based cryptography (2005) <a href="http://www.math.uwaterloo.ca/~ajmeneze/publications/pairings"> http://www.math.uwaterloo.ca/~ajmeneze/publications/pairings  </a>
3. John Bethencourt.  Intro to bilinear maps <a href="https://people.csail.mit.edu/alinush/6.857-spring-2015/papers/bilinear-maps.pdf"> https://people.csail.mit.edu/alinush/6.857-spring-2015/papers/bilinear-maps.pdf</a>
4. Advantages of bilinear map.  <a href="https://crypto.stackexchange.com/questions/12357/advantages-of-bilinear-map4">  https://crypto.stackexchange.com/questions/12357/advantages-of-bilinear-map4"> </a>
