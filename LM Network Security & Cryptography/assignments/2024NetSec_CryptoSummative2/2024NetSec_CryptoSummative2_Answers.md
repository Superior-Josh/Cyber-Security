## 2024NetSec_CryptoSummative1_Answers

**Jiayang Xu**

### Question 1

1. If  $\sigma_1^e = H(m)	r \bmod n$, output accept, else reject.

2. There are some attacks show that BadSign is not secure:

   * Assuming that $m$, $\sigma=(\sigma_{1},r)$ and $\sigma_{1}=H(m)^dr^d\bmod n$ are known:
   
     * such that $r'=r^e$, then $\sigma_{1}'=H(m)^dr\bmod n$
   
     * return $\sigma'=(H(m)^dr\bmod n,r^e)$
     * verification: $\sigma_1'^e=H(m)r^e=H(m)r'\bmod n$, accept.
   
   * For any $m$:
   
     * such that $r=H(m)^{e-1}$, then $\sigma_1=H(m)\bmod n$
     * return $\sigma=(H(m)\bmod n,H(m)^{e-1})$
     * verification: $\sigma_1^e=H(m)^e=H(m)H(m)^{e-1}=H(m)r\bmod n$, accept.
   
   * For any $m$:
   
     * such that $r=H(m)^{-1}$, then $\sigma_1=1$
     * return $\sigma=(1,H(m)^{-1})$
  * verification: $\sigma_1^e=1=H(m)H(m)^{-1}=H(m)r\bmod n$, accept.

### Question 2

It is known that:

$s_1 = g^r \bmod p \bmod q$
	$s_2 = g^r \bmod p \bmod q$
	$t_1 = r^{-1}(H(M_1) + x \cdot s_1) \bmod q$
	$t_2 = r^{-1}(H(M_2) + x \cdot s_2) \bmod q$

Due to the low collision of SHA-256 and $q$ is a large prime, we can assume that $H(M_1) \ne H(M_2) \bmod q$, then $t_1 \ne t_2$:

$r=\frac{H(M_1)-H(M_2)}{t_1-t_2}\bmod q$

$x=\frac{t_1r-H(M_2)}{s} \mod q$

So an adversary could recover the secret signing key from the signatures and the messages.

### Question 3

1. *Confidentiality*:
   
   * This protocol **does not fully guarantee confidentiality**. Although RC4 is a stream cipher, its security relies on the uniqueness and randomness of the key. In RC4, if the key (IV || key) is reused multiple times, an attacker may be able to deduce the plaintext from the pattern of the keystream. In this protocol, the IV is public, and the key is short (a 4-letter word), making it vulnerable to brute-force attacks, which could reveal the ciphertext.
   
   * Attack method: the attacker can perform a brute-force attack using the known IV and limited key space to deduce the keystream, thereby recovering the plaintext.
   
   *Data Integrity*:
   
   * This protocol **does not provide data integrity** guarantees. Encryption alone does not ensure integrity, as the attacker can modify the ciphertext without detection.
   
   * Attack method: the attacker can flip bits in the ciphertext, and Bob will decrypt the modified plaintext without realizing the data has been tampered with.
   
   *Authentication*:
   
   * This protocol also **does not provide authentication**. Since there is no mechanism in the protocol to verify the sender's identity, an attacker can forge a message and send it to Bob, who will be unable to verify whether the message came from Alice.
   
   * Attack method: the attacker can generate a legitimate ciphertext and send it to Bob, who will be unable to determine if the message truly came from Alice.

2. The plaintext PIN is **1847**, and the shared secret *key* is **hous**.

### Question 4

1. 

2. 
3. 

### Question 5