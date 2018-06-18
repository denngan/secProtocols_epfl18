1. **What is AES?**
<br> AES (Andvanced encryption algorithm) is a specification for the encryption of electronic data. </br>

2. **What is TLS?**
<br> TLS (Transport Layer Security Protocol) is a cryptographic protocol that provides communications security over a computer network (typically, the HTTP protocol). It sets up the cryptographic algorithms, validates both parties through digital certificates and generates symmetric key. </br>

3. **What is AES-GCM?**
AES-GCM provides authenticated encryption with associated data (AEAD). It uses:
<br> - Galois Counter Mode (GCM); </br>
<br> - an authenticated mode of operation; </br>
<br> - Advanced Encryption Standart (AES). </br>

4. **In which version of TLS is AES-GCM used?**
<br> Version 1.3. </br>

5. **What is AEAD?**
<br> AEAD - authenticated encryption with associated data. </br>


6. **What is a nonce? Where is it used in AES-GCM?**
<br> Nonce is an arbitrary number that can be used just once. In AES-GCM it is used in the formation of IV (initialization vector). IV = salt32 || nonce64. </br>

7. **What is a Galois Field?**
<br> Galois Field is a field that contains a finite number of elements. </br>

8. **What is the best way to generate a nonce?**
<br> There are two posiibilities: using a counter or using a Linear Feedback Shift Register (LFSR: a shift register whose input bit is a linear function of its previous state). </br>


9. **What is the difference between using a counter and LSFR for nonce generation?**



10. **Why should nonces not be created randomly?**
<br> When we create nonces randomly, we could have some collisions. For instance, with 2^33 sent messages the probability of collision is over 86% due to Birthday Paradox. </br>

11. **What does the Birthday Paradox imply?**
<br> The birthday paradox briefly: we have 23 people and we want to estimate that there are two men who have birthday at the same day. The probability of this is more than 50%. To understand it better, let's look at the birthday attack. </br>
<br> A birthday attack is a type of cryptographic attack that exploits the mathematics behind the birthday problem in probability theory. This attack can be used to abuse communication between two or more parties. The attack depends on the higher likelihood of collisions found between random attack attempts and a fixed degree of permutations. With a birthday attack it is possible to find a collision.  </br>

12. **What is known plaintext attack? How does it work in AES-GCM?**
<br> A known plaintext attack is the attack when we know open text and use it to retrieve the key with the aim to decrypt other messages. </br>
<br> When knowing the plaintext M, one can retrieve the IV encrypted in counter mode. CTR(IV) = C + M, when IV is reused, the CTR will decrypt any other ciphertext with unknown messages.</br>

13. **What is a forgery attack?**

3. Describe the Forbidden Attack and why it is called that way?
3. Which functions are used in AES-GCM?
5. How is the GHASh Key L computed?
6. How can an attacker get Key L when a nonce is reused?
8. Which algorithm is used for Factorization and in which complexity does it operate?
8. Why is a static endpoint needed to mount a practical forgery attack? What is a static endpoint?
9. Explain the steps of a practical forgery attack with nocne reuse and why a man in the middle is needed.
4. Under which circumstances is the Forbidden Attack possible?
7. How long is the IV in AES-GCM for TLS and what does it consist of?
8. Why is salt added to the nonce to create the IV in AES-GCM?
9. What is added to the IV before AES-GCM encryption and why.
10. Why could adding 0^32 to the IV before AES-GCM encryption be dangerous?
11. What other kind of algorithms could be used for AES-GCM? Explain how they improve security.
12. Whould the Forbidden Attack be possible if AES-GCM was generating nonces from the record sequence number?
13. How secure is AES-GCM?
14. Is it insecure if a server is forced to resend a new packet in a new session with the same salt or different salt?
15. What benefits arise form using the TLS record sequence number as nonce? 
17. What is the goal of the Forbidden Attack? 
18. What is the goal of the known plain message attack?
19. What are advantages and disadvantages of MAC-then Encrypt?
20. Is the attack possible in real life? 
