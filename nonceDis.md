1. What is AES?
2. What is TLS?
3. What is AES-GCM?
3. In which version of TLS is AES-GCM used. 
4. What is AEAD?
5. What is a nonce? Where is it used in AES-GCM?
5. What is the best way to generate a nonce?
6. What is the difference between using a counter and LSFR for nonce generation?
8. Why should nonces not be created randomly?
9. What does the Birthday Paradox imply.
10. What is known plaintext attack? How does it work in AES-GCM?
2. What is a forgery attack? 
3. Describe the Forbidden Attack and why it is called that way?
3. Which functions are used in AES-GCM?
5. How is the GHASh Key L computed?
6. How can an attacker get Key L when a nonce is reused?
8. Which algorithm is used for Factorization and in which complexity does it operate?
8. Why is a static endpoint needed to mount a practical forgery attack? What is a static endpoint?
9. Explain the steps of a practical forgery attack with nocne reuse.
4. Under which circumstances is the Forbidden Attack possible?
7. How long is the IV in AES-GCM for TLS and what does it consist of?
8. Why is salt added to the nonce to create the IV in AES-GCM?
9. What is added to the IV before AES-GCM encryption and why.
10. Why could adding 0^32 to the IV before AES-GCM encryption be dangerous?
11. What other kind of algorithms could be used for AES-GCM? Explain how they improve security.
12. Whould the Forbidden Attack be possible if AES-GCM was generating nonces from the record sequence number?
13. How secure is AES-GCM?
14. Is it unsecure if a server is forced to resend a new packet in a new session with the same salt?
15. What benefits arise form using the TLS record sequence number as nonce? 
