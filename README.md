# EX-NO-8-IMPLEMENTATION OF DIGITAL SIGNATURE STANDARD

## AIM:
To write a C program to implement the signature scheme named digital signature
standard (Euclidean Algorithm).

## ALGORITHM:

  STEP-1: Alice and Bob are investigating a forgery case of x and y.
  
  STEP-2: X had document signed by him but he says he did not sign that document digitally.
  
  STEP-3: Alice reads the two prime numbers p and a.
  
  STEP-4: He chooses a random co-primes alpha and beta and the x’s original signature x.
  
  STEP-5: With these values, he applies it to the elliptic curve cryptographic equation to obtain y.
  
  STEP-6: Comparing this ‘y’ with actual y’s document, Alice concludes that y is a forgery.

## PROGRAM:
```
#include <stdio.h>


int euclid(int m, int n) {
    if (n == 0) {
        return m;
    } else {
        return euclid(n, m % n);
    }
}


void exteuclid(int a, int b, int *gcd, int *x) {
    int r1 = a, r2 = b;
    int s1 = 1, s2 = 0;
    int t1 = 0, t2 = 1;

    while (r2 > 0) {
        int q = r1 / r2;
        int r = r1 - q * r2;
        r1 = r2;
        r2 = r;

        int s = s1 - q * s2;
        s1 = s2;
        s2 = s;

        int t = t1 - q * t2;
        t1 = t2;
        t2 = t;
    }

    *gcd = r1;
    *x = (t1 < 0) ? (t1 + a) : t1; 
}

int mod_pow(long long base, long long exp, long long mod) {
    long long result = 1;
    while (exp > 0) {
        if (exp % 2 == 1) { 
            result = (result * base) % mod;
        }
        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}

int main() {
    int p = 823;
    int q = 953;
    int n = p * q;
    int Pn = (p - 1) * (q - 1);

   
    int e = 313; 
    int d;
    int gcd;

    exteuclid(Pn, e, &gcd, &d);
    
    if (gcd == 1) {
        printf("Decryption key is: %d\n", d);
    } else {
        printf("Multiplicative inverse for the given encryption key does not exist. Choose a different encryption key.\n");
        return 1; 
    }

   
    int M = 19070;

   
    long long S = mod_pow(M, d, n); 

    long long M1 = mod_pow(S, e, n); 

 
    if (M == M1) {
        printf("As M = M1, accept the message sent by Alice.\n");
    } else {
        printf("As M not equal to M1, do not accept the message sent by Alice.\n");
    }

    return 0;
}
```

## OUTPUT:
![Screenshot 2024-10-16 125236](https://github.com/user-attachments/assets/1d50b2f9-32f8-4376-8e86-c0e3c7942518)

## RESULT:
  Thus the simple Code Optimization techniques had been implemented successfully
