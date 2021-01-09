---
layout: post
title: Public key encryption with keyword search
---

This is an attempt to convey the concept of encrypted search to non-cryptographers. Please excuse the lack of rigour for which I will compensate at the end of the article.

Assume you have a public key encryption system.

Let’s say you wanted a third-party to verify whether an encrypted text matches a search string, without 
1. decrypting the encrypted text or 
2. encrypting the search string

Let’s say encryption("Nice") = $Ev7

How can a third-party verify that "$Ev7" is actually "Nice" in encrypted form ?

What you need here is an auxiliary string called a "trapdoor" which the third-party can use to verify the equality

This problem is solved using a bilinear map, which enables two different ways of producing same encrypted text

A bilinear map is a function of two variables f(x, y) satifying this condition

```
f(x^a, y^b) = f(x, y)^ab
```

<img src="https://render.githubusercontent.com/render/math?math=f(x^{a}, y^{y}) = f(x, y)^{ab} ">

Lets say you have
1. public key = y
2. private key = PVT

Let x be the text

The encrypted text is generated using f(x, y).

 so f("Nice", y]) = $Ev7

Now you have to generate an extra string called the trapdoor "PVT.x"

   PVT * "Nice" = "Vgzv"  (multiply by PVT)

   y/PVT = z (divide by PVT)

Now by the property of a bilinear map, the PVT multiplication and division cancels out giving

f(PVT.x, y/PVT) = f(x, y)

So you have two ways of producing the same encrypted text

   f("Vgzv", z) = f("Nice", x)

Give this string "Vgzv" along with the public key modification (y/PVT) to the third-party

   f("Vgzv", z) = f("Nice", x) = "$Ev7"

This is essentially the first cryptographic construction produced by Boneh and Franklin in their paper

Alright, I have played fast and loose here to provide intuition, lets define it with more rigour

![resources](https://docs.google.com/presentation/d/e/2PACX-1vTx1a9NTz2ilHR2jFEJzZiPMbe3OrChqxyeOcajtey4Lt654_tTPjDIGeNKFUxLPz1jE_hrAIjTQPKg/pub?start=true&loop=true&delayms=1000)

