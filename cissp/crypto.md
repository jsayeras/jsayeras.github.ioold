
Finite fields are a core element of modern cryptography. A finite field or a Galois field is a field that contains a finite number of elements. The number of elements of a finite field is called **order** or **size**. In a field of order p<sup>k</sup> (where *p* is a prime and *k* is a positive integer), adding *p* copies of any element always results in zero; that is known as the **characteristic** of the field.  

Given that the number of elements is finite, when we add or multiply on a finite field we will have to devide by the characteristic of the field and take the remaining part. In other words, use the *mod* operation. As an example on 𝔽<sub>7</sub> = {0,1,2,3,4,5,6}, if we were to add 6 and 3, the result would be 2. This is calcualted (6 + 3) % 7 = 2. Similarly the multiplication on a finite field would be (6 x 3) % 7 = 4.

On a finite field, the multiplicative inverse can be calculated using the extended Euclidean algorithm. The classic Euclidean algorithm finds the greatest common divisor *d* given two natural numbers *a* and *b*. The extended version of the Euclidean alogirthm allows us to find what is known as the Bezout identity where *ax + by = d*. It has to be noted that when the greatest common divisor is **different than one, there is no multiplicative inverse**. So if we were to calculate the inverse of 3 in 𝔽<sub>7</sub>, we would have 3<sup>-1</sup> = x mod 7

```Python
# Python code for the extended Euclidean algorithm
def extended_gcd(a, b):
    if a == 0:
        return b, 0, 1
    else:
        gcd, x, y = extended_gcd(b % a, a)
        return gcd, y - (b // a) * x, x

# Modular inverse only exists if gcd > 1
def modinv(a, m):
    gcd, x, y = extended_gcd(a, m)
    if gcd != 1:
        raise Exception('modular inverse does not exist')
    else:
        return x % m
```

The result of calculating *modinv(3, 7)* is 5. According to the Bezout identity we have that *ax + by = d*. In this case, the greatest common divisor *'d'* between 3 and 7 is 1. The result of the extended Eucledean alogirhtm is gcd=1, x=1 and y=-2. Therefore we have that 1 = 1×7 +(-2×3).

We can calculate all the modular inverse of this finite field by running the following code:
```python
for i in range(7):
    try:
        print(i, modinv(i, 7))
    except:
        print(i, "has no multiplicative inverse")
```
And we would get the following result:
|i|i<sup>-1</sup>|
|-|-------|
|0 |has no multiplicative inverse|
|1 |1|
|2 |4|
|3 |5|
|4 |2|
|5 |3|
|6 |6|

Another way to check whether the inverse module is correct, is to compute the i × i<sup>-1</sup> mod p = 1 mod p. So for example 3×5 mod 7 = 1 mod 7. Remember that we are in 𝔽<sub>7</sub>

A finite field 𝔽<sub>q</sub> with characteristic *p*, can be created using a prime *p*, and a positive integer *m* by calculating q = p<sup>m</sup>. In cryptography binary fields are very imporant. An example of a binary field could use be the field 𝔽<sub>8</sub> or 𝔽<sub>2<sup>3<sup/></sub>. Fields with prime numbers *p* where *p* is big enough are also used.

