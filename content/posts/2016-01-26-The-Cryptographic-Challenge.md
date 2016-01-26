## Go Hack Night: The Cryptographic Challenge

Throughout history, cryptography has had dramatic effects on the outcome of wars, monarchies and the lives of individuals. One example of this is the successful cracking of the German Enigma cipher during World War II. This ultimately proved to be instrumental in the Allied forces victory.

In this puzzle you will have the opportunity to try your hand at the ancient art of code-cracking by decrypting a text message that uses two distinct ciphers to render its contents unintelligible.

### The Ciphers

#### The Ceasar Cipher

The earliest and simplest form of ciphers is known as "monoalphabetic substitutions". This is a system of encryption wherein every occurrence of a particular plaintext letter in the alphabet is replaced by a cyphertext letter. This will generate a second alphabet where the 26 letters are in different positions. Juxtaposing the two alphabets will yield a one-to-one mapping of the plaintext letter to its encrypted counterpart.

The [Caesar Cipher](https://en.wikipedia.org/wiki/Caesar_cipher) is an example of such a substitution cipher. It is attributed to Julius Caesar who used it to communicate with his generals. Also known as a shift cipher, it replaces each plaintext letter with a letter that is a fixed number of places down the alphabet. For example, with a shift of three, a B in the plaintext alphabet becomes an E in the ciphertext one.

Here is an example of a full cipher alphabet with a shift parameter of 3:

<pre>Plain alphabet:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher alphabet:   DEFGHIJKLMNOPQRSTUVWXYZABC
</pre>

Placing the two alphabets side by side makes it easy to decrypt a message like:

<pre>FRZDUGV GLH PDQB WLPHV EHIRUH WKHLU GHDWKV; WKH YDOLDQW QHYHU WDVWH RI GHDWK
EXW RQFH.

Z. VKDNHVSHDUH, MXOLXV FDHVDU
</pre>

Which in its plain text form is:

<pre>COWARDS DIE MANY TIMES BEFORE THEIR DEATHS; THE VALIANT NEVER TASTE OF DEATH
BUT ONCE.

W. SHAKESPEARE, JULIUS CAESAR
</pre>

The tricky part of the Caesar cipher is that the shift parameter is often unknown to the code cracker.

#### The Vigenère Cipher

This cipher was long thought to be unbreakable because, unlike the Caesar cipher, there is no simple one-to-one mapping of the plaintext to the cipher alphabet.

The [Vigenère cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher) is applied by utilizing a series of different Caesar ciphers based on the letters of a chosen keyword. The ordinal position of each letter in the keyword is what determines the shift parameter values of the various Caesar ciphers used. The resulting cipher alphabets are then applied in sequence and then repeated to encode the letters in the message.

This is perhaps easier to understand with an example.

If we use the word ABLE as the keyword, we can see that the shift values for each letter will be 0, 1, 11, and 4. Note that the letter A produces no shift since its value is 0.

Let's use the Vigenère Cipher to encrypt the following message with the keyword ABLE:

<pre>ATTACK AT DAWN
</pre>

The following four cipher alphabets come into play:

Shift 0 (Letter A):

<pre>Plain alphabet:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher alphabet:   ABCDEFGHIJKLMNOPQRSTUVWXYZ
</pre>

Shift 1 (Letter B):

<pre>Plain alphabet:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher alphabet:   BCDEFGHIJKLMNOPQRSTUVWXYZA
</pre>

Shift 11 (Letter L):

<pre>Plain alphabet:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher alphabet:   LMNOPQRSTUVWXYZABCDEFGHIJK
</pre>

Shift 4 (Letter E):

<pre>Plain alphabet:    ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher alphabet:   EFGHIJKLMNOPQRSTUVWXYZABCD
</pre>

One trick you can use to facilitate knowing when to apply which cipher alphabet is to repeat the keyword above the encoded message, like so:

<pre>Keyword: ABLEABLEABLE
Message: ATTACKATDAWN
</pre>

Using these four cipher alphabets in circular sequence will produce the following encrypted message:

<pre>AUEECL LX DBHR
</pre>

### On to the challenge!

#### Stage 1. Crack the cipher and decrypt the message

Below you will see a message that has been encrypted with the Vigenère cipher:

<pre>EFMZRNQMWOBEBUIXDDMTRDGAXGJUBKNEIVWATHLHJDZUOAOENVIBROCXCSLZUIFUDCSPHSGMDTQTQAUNVSWTVOAKXUPZVNGATAQJQLRVGSIYROSMWSJUBKGATAITHFNVIIZKEOSMWSJUBKUTHWVIYUQXSHPKBNVHCOBSLRRJJSAZFOLHJFMRVKRPDKBNVSOHDYKUZEFPXHPGAOABDBMBRNVYNCCJBNGIPFBOPUYTGZGRVKRHCWWTFIZLJFMEBUPTCOXVEEPBPHMZUEYHVWAZVCFHUGPOCPVGVOVEFOEMDTXXBDHVTRQYPRRXIZGOASVWTCNGAAYETUMJCRBZGOUSVNTFPBCGY
</pre>

Your job is to decrypt this. The problem is, the keyword has been encrypted with the Caesar cipher! The encrypted keyword is <strong>JICAHUHN</strong>. It is a common English word. Once you have cracked the encryption and discover the keyword, you should be able to write some code to decrypt the main message.

Regarding the format of the message, note that both the keyword, as well as the message will be in uppercase letters. Also, all spaces and punctuation marks have been removed from the message body to make it harder to crack the encryption.

<div class="hint">
	<a href="#" class="hint-reveal">Click to reveal a hint to help you with Stage 1.</a>

	<p><strong>Hint:</strong> One approach to cracking the Caesar cipher is to use <a href="https://en.wikipedia.org/wiki/Brute-force_attack">brute-force</a> to try all possible shift values and then examine the results. Because you know that the keyword is a common English word, you should be able to find the word in the results, either by hand, or programmatically by checking the results against a <a href="https://en.wikipedia.org/wiki/Words_(Unix)">word list</a>. There are a number of ways to implement a Vigenére cipher decrypter. One would be to create a <a href="https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Description">Vigenére table</a> and use it to look up the corresponding unencrypted letter of a given letter in the encrypted message based on the current letter of the keyword.</p>
</div>

#### Stage 2. Identify the source and encrypt the title

Once you have decrypted the message, you should be able to identify its source. The next stage is to write some code that can encrypt a message using the Vigenère cipher and encrypt the title of the source using the same keyword as before.

<div class="hint">
	<a href="" class="hint-reveal">Click to reveal a hint to help you with Stage 2.</a>

	<p><strong>Hint:</strong> The code to encrypt a message should be very similar to the code you used to decrypt one. See if you can modify your decryption code to perform the reverse action.</p>
</div>

#### Stretch Goal: A tougher nut to crack

If you manage to complete both of the tasks above and want a more challenging problem to crack, this is for you. Below is another message encoded with the Vigenère cipher for you to crack:

<pre>SOMZAQLLIWSZKBBOGKLBBQJNNVODSKIPVSSQWUIDLGWTBTALGPVSHPETIDAJUVNULYOHVMJRBVZYALWUIQKRDLBUUQAUAQLFAJPUWDCVIXGDIFEAJIWZIZWBQJIFGPWULMMRDVZUKRKOMXHNAVXXWJAHZZZMSAWIJGPLJQSSPPNGDNNVODSKOTGRWCHPVSAQPOIFOFAUEQHPAWIDWYLYWSJYIAPQWVLLZUWLYLKMFZAQCELJERMOGKLVAUFELVMFJWKYUGKGYZWYWNNVODSKOHZQWJANIZLQKTMMJCAEYGAQEAMEGKAHZQKNWYSXALCTGODYETQELFWAQFAQLVAEAZHLBAOPEAMSJYJKXDGENHUEFMXSMBJMCYIYKRNBTKEYCUQRAAAUBAFCOJWYHSPLZBJMCYIYEGJNQESLWYBNWAWBAQARWWXXACOHKOMKQSIFWBGUWIDCZNMFGRDLEAJJZIMOSSOLQFJCMBQDWQORQXDYJKQZYCJBQFQYJKMEHCYPIXDWXLKMMQAPBBJMZBKQKMXQMOLQKMJQSSPFXDGENHUYWPODPAKSXJWZKAEVCEDWRPMILFATAQDTAZIESPPPAFKUESTQFHKFETSRPOMKVMWULIAJHKWULZAABQJ
</pre>

The problem is, this time you do not know the keyword! The final stage of the challenge is to write some code that can crack the cipher and reveal the message.

<div class="hint">
	<a href="" class="hint-reveal">Click to reveal a hint to help you with the Stretch Goal.</a>

	<p><strong>Hint:</strong> There are a <a href="https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Cryptanalysis">number of techniques</a> that can be used to crack the Vigenère cipher. A good place to start is to see if you can identify the keyword length using <a href="https://en.wikipedia.org/wiki/Vigenère_cipher#Kasiski_examination">Kasiski examination</a>. Once you have an idea of the length of the keyword, you can use either <a href="https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Frequency_analysis">Frequency analysis</a> or <a href="https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Key_elimination">Key elimination</a> to recover the keyword and crack the cipher.</p>
</div>

<em>(This challenge was adapted from the [NWRUG Cryptographic Challenge meetup](http://nwrug.org/quizzes/the-cryptographic-challenge))</em>
