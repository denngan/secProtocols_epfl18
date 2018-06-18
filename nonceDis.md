1. **What is AES?**  
AES (Andvanced encryption algorithm) is a blockcipher encrypting 128 bits with a symmetric key.

2. **What is TLS?**  
TLS (Transport Layer Security Protocol) is a cryptographic protocol that provides communication security over a computer network (typically, the HTTP protocol). It sets up the cryptographic algorithms, validates both parties through digital certificates and generates symmetric key.

3. **What is AES-GCM?**  
Mode of operation offering authendticated Encryption with associated data (AEAD)
* Counter Mode for Stream Encryption
* Advanced Encryption Standart (AES)
* GHASH for authentication

4. **In which version of TLS is AES-GCM used?**  
Version 1.3 and 1.2

5. **What is AEAD?**
authenticated encryption with associated data; That means that some encrypted message can be authenticated and on top data can be added that will be authenticated but not encrypted.

6. **What is a nonce? Where is it used in AES-GCM?**  
Number used once - A nonce is an arbitrary number that can be used just once. In AES-GCM the nonce is used to initialize the Counter mode of operation. The TLS IV is 96 bits long: IV = salt32 || nonce64. 

7. **What is a Galois Field?**  
A Galois Field is a finite field $GF(p^k)$ with order $p^k$. 

8. **What is the best way to generate a nonce?**  
There are two posiibilities: using a counter or using a Linear Feedback Shift Register (LFSR: a shift register whose input bit is a linear function of its previous state). This way the whole number range is covered before a nonce repeats, meaning $2^64$ different nonces.

9. **What is the difference between using a counter and LSFR for nonce generation?**  
The difference is that the LSFR seems random to a third-party (because it depends on the previous state), but a counter always increments by one. The security of both methods is similar though as the LSFR also goes through the whole number range before creating duplicates.

10. **Why should nonces not be created randomly?**  
When we create nonces randomly, collisions are possible. While this improbable for few nonces it becomes very probable with a lot of nonces. For instance, with $2^33$ sent messages the probability of collision is over 86% due to Birthday Paradox. Therefore, a counter offers a bigger number range without risk of nonce reuse.

11. **What does the Birthday Paradox imply?**  
The birthday paradox states that in a set of size N only $O(/sqrt{N})$ samples are needed to find a collision with constant probability. That means that with an increasing size of samples the probability for a collision rises very quickly. 

12. **What is known plaintext attack? How does it work in AES-GCM?**  
A known plaintext attack is an attack where the plaintext that is ecncrypted is known. In AES-GCM we can XOR the ciphertext with the message to get the block the message was encrypted with $CTR_K$

13. **What is a forgery attack?**  
In a forgery attack the attacker is able to authenticate and thus forge messages.

14. **Describe the Forbidden Attack and why it is called that way?**  
The Forbidden Attack is made possible due to nonce reuse in TLS and AES-GCM. As this is against specifications it is called forbidden. The attack allows us two obtain two authentication tags for two different messages that where computed with the same GHASH key. This enables us to XOR the tags and factor the polynomials. L is a root and thus we are able to obtain L and authenticate messages. 

15. **Which functions are used in AES-GCM?**   
AES, XOR and GHASH.

16. **How is the GHASH Key L computed?**  
$L = Enc(0)$ using AES encryption of 128-bit of zeros.

17. **How can an attacker get key L when a nonce is reused?**  
XOR the tags and factor the polynomial, L is one of the roots. The create a second polynomial from another nonce reuse. In this case L will also be a root so the intersection of the two root sets will give us L.

18. **Which algorithm is used for Factorization and in which complexity does it operate?**  
We use Cantor-Zassenhaus algorithm which has a polynomial complexity. 

19. **Why is a static endpoint needed to mount a practical forgery attack? What is a static endpoint?**
A static endpoint is a site which uses only static html. With a static endpoint it is known which message is going to be sent and we can mount a known plaintext attack. This allows us to encrypt any new message we want while the frobidden attack allows us to authenticate it.

20. **Explain the steps of a practical forgery attack with nonce reuse and why a man in the middle is needed.**    
Firstly, we mount man-in-the-middle between the server and the user. That is becasue we need to monitor and change the traffic sometimes. The steps are:
* Collect nonces, wait for duplicate
* Get GHASH key (enable forgery)
* Redirect to static web site
* Known plaintext attack - enable encryption
* Inject Javascript

21. **Under which circumstances is the Forbidden Attack possible?**  
The Forbidden Attack i possible with nonce reuse.

22. **How long is the IV in AES-GCM for TLS and what does it consist of?**
The IV is 96 bits (32 bits of salt and 64 bits of nonce).

23. **Why is salt added to the nonce to create the IV in AES-GCM?**
When we have two clients, we can have some collisions due to the similar key or similar nonces. To avoid this, salt is used.

24. **What is added to the IV before AES-GCM encryption and why?**  
Before AES-GCM encryption, 31 zeros a one are added. These 32 bits are used as a counter.

25. **Why could adding 0^32 to the IV before AES-GCM encryption be dangerous?**
This can lead to a collision with the key L if the IV is all zeros, too, because $L=Enc(0)$.  

26. **What other kind of algorithms could be used for AES-GCM? Explain how they improve security.**  
ChaCha20-Poly1305, AES-OCB for deterministic nonce creation. The advantages here are that the nonce is constructed from the record sequence number. So the nonce does not have to be transmitted with each message. Also MAC-then-Encrypt algorithms are possible as they are still secure when a nonce is reused. That is becasue the MAC is computed first and only then encryption is done.

27. **Would the Forbidden Attack be possible if AES-GCM was generating nonces from the record sequence number?**  
No, because the record sequence number has same properties as a counter.

28. **How secure is AES-GCM?**
It is theoretically secure if there are no developer mistakes and, of course, no nonce is reused.

29. **Is it insecure if a server is forced to resend a new packet in a new session with the same salt or different salt?**  
Collisions are possible with the same salt, same key, same nonce. The message has to be different though.

30. **What benefits arise form using the TLS record sequence number as nonce?**  
It has properties of a counter so it is safe and it does not have to be computed, which prevents mistakes. Also it saves bandwidth as it is kniwn to both parties.

31. **What is the goal of the Forbidden Attack?**  
To retrieve GHASH key L to authenticate and forge packets.

32. **What is the goal of the known plain message attack?**  
Retreiving the $CTR_K(IV)$ value that is used to ancrypt and decrypt.

33. **What are advantages and disadvantages of MAC-then Encrypt?**
With MAC then encrypt the MAC is computed from the plain text and then tag and plaintext are decrypted. That way nonce reuse is not a problem. But the plaintext has to be processed twice.

34. **Is the attack possible in real life?**  
Yes, of course! According to the findings, 184 servers that reused nonces were found (70 devices returned one duplicate and 107 used the same number constantly). 70'000 devices generated random nonces.
