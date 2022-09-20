# Bitcoin Wallet Recovery via ECDSA Short Signatures

<p>We all know that the disclosure of the secret key in the ECDSA signature can lead to the complete recovery of the Bitcoin Wallet.&nbsp;In our earlier articles, we looked at&nbsp;<a href="https://cryptodeeptech.ru/lattice-attack/" target="_blank" rel="noreferrer noopener">weaknesses and vulnerabilities</a>&nbsp;in blockchain transactions, but there are also ECDSA short signatures that also lead to the full recovery of a Bitcoin Wallet.</p>




<h3>Why are these ECDSA signatures called short?</h3>



<blockquote class="wp-block-quote"><p>You can get the answer to this question from the topic under discussion:&nbsp;<a href="https://bitcoin.stackexchange.com/questions/38513/the-shortest-ecdsa-signature" target="_blank" rel="noreferrer noopener"><strong>«The shortest ECDSA signature» [The shortest ECDSA signature]</strong></a></p></blockquote>



<p>In our last article:&nbsp;<a href="https://cryptodeeptech.ru/reduce-private-key/" target="_blank" rel="noreferrer noopener"><em>«Reducing the private key through scalar multiplication using the ECPy + Google Colab library»</em></a>&nbsp;we created a&nbsp;<em>Python</em>&nbsp;script:&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/main/08ReducePrivateKey/maxwell.py" target="_blank" rel="noreferrer noopener">maxwell.py</a>&nbsp;which generated a rather interesting public key for us</p>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/69a7a0b324ac3b1f3e0dc27f0f4130bf.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<pre class="wp-block-code"><code>(0x3b78ce563f89a0ed9414f5aa28ad0d96d6795f9c63 , 0xc0c686408d517dfd67c2367651380d00d126e4229631fd03f8ff35eef1a61e3c)</code></pre>



<blockquote class="wp-block-quote"><p>As we know the value of the signature,&nbsp;<code>"R"</code>this is the public key from the private key<code>(Nonce)</code></p></blockquote>



<p>Take a look at Blockchain transaction:&nbsp;<a href="https://btc.exan.tech/tx/11e6b169701a9047f3ddbb9bc4d4ab1a148c430ba4a5929764e97e76031f4ee3" target="_blank" rel="noreferrer noopener"><strong>11e6b169701a9047f3ddbb9bc4d4ab1a148c430ba4a5929764e97e76031f4ee3</strong></a></p>



<h3>RawTX:</h3>



<pre class="wp-block-code"><code>0100000001afddd5c9f05bd937b24a761606581c0cddd6696e05a25871279f75b7f6cf891f250000005f3c303902153b78ce563f89a0ed9414f5aa28ad0d96d6795f9c6302200a963d693c008f0f8016cfc7861c7f5d8c4e11e11725f8be747bb77d8755f1b8012103151033d660dc0ef657f379065cab49932ce4fb626d92e50d4194e026328af853ffffffff010000000000000000016a00000000
</code></pre>



<blockquote class="wp-block-quote"><p>The size of this transaction is only:<code>156 байт</code></p></blockquote>



<h3>How can I restore a Bitcoin Wallet through ECDSA short signatures?</h3>



<p>In the cryptanalysis of the Bitcoin blockchain, we use our own&nbsp;<em>Bas</em>&nbsp;h script:<code>btcrecover.sh</code></p>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/299fa2616cbdb8e6df9304862f441ba2.gif" alt="bitcoin wallet recovery process" title="bitcoin wallet recovery process"><figcaption>bitcoin wallet recovery process</figcaption></figure>



<h3>Bash script: btcrecover.sh</h3>

<pre class="wp-block-code"><code>wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
<pre class="wp-block-code"><code>sudo python2 get-pip.py
<pre class="wp-block-code"><code>pip2 install -r requirements.txt
chmod +x btcrecover.sh


 ./btcrecover.sh 12yysAMhagEm67QCX85p3WQnTUrqcvYVuk


 ./btcrecover.sh 15HvLBX9auG2bJdLCTxSvjvWvdgsW7BvAT
</code></pre>



<h3>Results:</h3>



<p><code>| privkey : addr |</code></p>



<p><a href="https://cryptodeeptech.ru/bitaddress.html" target="_blank" rel="noreferrer noopener">Let’s open bitaddress</a>&nbsp;and&nbsp;&nbsp;&nbsp;check:</p>



<pre class="wp-block-code"><code>ac8d0abda1d32aaabff56cb72bc39a998a98779632d7fee83ff452a86a849bc1:12yysAMhagEm67QCX85p3WQnTUrqcvYVuk
b6c1238de89e9defea3ea0712e08726e338928ac657c3409ebb93d9a0873797f:15HvLBX9auG2bJdLCTxSvjvWvdgsW7BvAT</code></pre>



<h2>Let’s move on to the experimental part and analyze in more detail all the scripts for restoring a Bitcoin Wallet</h2>



<p>Open&nbsp;&nbsp;<a href="https://github.com/demining/TerminalGoogleColab" target="_blank" rel="noreferrer noopener"><strong>[TerminalGoogleColab]</strong></a>&nbsp;.</p>



<p><a href="https://github.com/demining/CryptoDeepTools/tree/main/09BitcoinWalletRecovery" target="_blank" rel="noreferrer noopener"><strong>Let’s use the «09BitcoinWalletRecovery»</strong></a>&nbsp;repository&nbsp;.</p>



<pre class="wp-block-code"><code>git clone https://github.com/demining/CryptoDeepTools.git

cd CryptoDeepTools/09BitcoinWalletRecovery/

ls</code></pre>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/4e37b8f6cefc8f8d0553f541a5eb8b98.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<h3>Install all the necessary modules:</h3>



<pre class="wp-block-code"><code>bitcoin
ecdsa
utils
base58</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>pip2 install -r requirements.txt</code></pre>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/d5f25e5b1b966ff43a48aaf0955ecfcd.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<blockquote class="wp-block-quote"><p>Using the&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/main/09BitcoinWalletRecovery/breakECDSA.py" target="_blank" rel="noreferrer noopener">breakECDSA.py</a>&nbsp;script, we get from the&nbsp;<code>RawTX</code>signature [R, S, Z]</p></blockquote>



<pre class="wp-block-code"><code>python2 breakECDSA.py 0100000001afddd5c9f05bd937b24a761606581c0cddd6696e05a25871279f75b7f6cf891f250000005f3c303902153b78ce563f89a0ed9414f5aa28ad0d96d6795f9c6302200a963d693c008f0f8016cfc7861c7f5d8c4e11e11725f8be747bb77d8755f1b8012103151033d660dc0ef657f379065cab49932ce4fb626d92e50d4194e026328af853ffffffff010000000000000000016a00000000 &gt; signatures.txt
</code></pre>



<h3>The result will be saved to a file: signatures.txt</h3>



<p>Let’s open the file:<code>PublicKeys.txt</code></p>



<pre class="wp-block-code"><code>cat signatures.txt</code></pre>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/cd32b99e37cc600ddd3c35965e2a0288.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<pre class="wp-block-code"><code>R = 0x00000000000000000000003b78ce563f89a0ed9414f5aa28ad0d96d6795f9c63
S = 0x0a963d693c008f0f8016cfc7861c7f5d8c4e11e11725f8be747bb77d8755f1b8
Z = 0x521a65420faa5386d91b8afcfab68defa02283240b25aeee958b20b36ddcb6de</code></pre>



<p>As we know from our last&nbsp;<a href="https://habr.com/ru/post/682220/">article</a>&nbsp;, we know&nbsp;<em><u>the secret key</u></em>&nbsp;to generating&nbsp;<em>the signature</em>&nbsp;<code>R</code></p>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/9dfb1763d978473245abb6cab03e0e48.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<blockquote class="wp-block-quote"><p>In our case, the&nbsp;<em><u>secret key</u></em>&nbsp;<code>(Nonce)</code>&nbsp;is:</p></blockquote>



<pre class="wp-block-code"><code>0x7fffffffffffffffffffffffffffffff5d576e7357a4501ddfe92f46681b20a0 --&gt; 0x3b78ce563f89a0ed9414f5aa28ad0d96d6795f9c63, 0x3f3979bf72ae8202983dc989aec7f2ff2ed91bdd69ce02fc0700ca100e59ddf3
</code></pre>



<h3>Signatures:</h3>



<pre class="wp-block-code"><code>K = 0x7fffffffffffffffffffffffffffffff5d576e7357a4501ddfe92f46681b20a0
R = 0x00000000000000000000003b78ce563f89a0ed9414f5aa28ad0d96d6795f9c63
S = 0x0a963d693c008f0f8016cfc7861c7f5d8c4e11e11725f8be747bb77d8755f1b8
Z = 0x521a65420faa5386d91b8afcfab68defa02283240b25aeee958b20b36ddcb6de</code></pre>



<blockquote class="wp-block-quote"><p>Now that we know the value of&nbsp;<code>[K, R, S, Z</code>] we can get the private key using the formula and restore the Bitcoin Wallet.</p></blockquote>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/2dba14ab5cb76228181c68a9403038a7.svg" alt="Privkey = ((((S * K) - Z) * ​​modinv(R,N)) % N)"></figure>



<p>To get the private key, let’s use the&nbsp;<em>Python</em>&nbsp;script:&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/main/09BitcoinWalletRecovery/calculate.py" target="_blank" rel="noreferrer noopener">calculate.py</a></p>



<pre class="wp-block-code"><code>def h(n):
    return hex(n).replace("0x","")

def extended_gcd(aa, bb):
    lastremainder, remainder = abs(aa), abs(bb)
    x, lastx, y, lasty = 0, 1, 1, 0
    while remainder:
        lastremainder, (quotient, remainder) = remainder, divmod(lastremainder, remainder)
        x, lastx = lastx - quotient*x, x
        y, lasty = lasty - quotient*y, y
    return lastremainder, lastx * (-1 if aa &lt; 0 else 1), lasty * (-1 if bb &lt; 0 else 1)

def modinv(a, m):
    g, x, y = extended_gcd(a, m)
    if g != 1:
        raise ValueError
    return x % m
    
N = 0xfffffffffffffffffffffffffffffffebaaedce6af48a03bbfd25e8cd0364141


K = 0x7fffffffffffffffffffffffffffffff5d576e7357a4501ddfe92f46681b20a0
R = 0x00000000000000000000003b78ce563f89a0ed9414f5aa28ad0d96d6795f9c63
S = 0x0a963d693c008f0f8016cfc7861c7f5d8c4e11e11725f8be747bb77d8755f1b8
Z = 0x521a65420faa5386d91b8afcfab68defa02283240b25aeee958b20b36ddcb6de


print (h((((S * K) - Z) * modinv(R,N)) % N))</code></pre>



<h3>Let’s run the Python script: calculate.py</h3>



<pre class="wp-block-code"><code>python3 calculate.py</code></pre>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/502645324ec5666803f791ea3cc3a109.png" alt="PrivKey=b6c1238de89e9defea3ea0712e08726e338928ac657c3409ebb93d9a0873797f" title="PrivKey=b6c1238de89e9defea3ea0712e08726e338928ac657c3409ebb93d9a0873797f"><figcaption>PrivKey=b6c1238de89e9defea3ea0712e08726e338928ac657c3409ebb93d9a0873797f</figcaption></figure>



<p><a href="https://cryptodeeptech.ru/bitaddress.html" target="_blank" rel="noreferrer noopener">Let’s open bitaddress</a>&nbsp;and&nbsp;&nbsp;&nbsp;check:</p>



<pre class="wp-block-code"><code>ADDR: 15HvLBX9auG2bJdLCTxSvjvWvdgsW7BvAT
WIF:  L3LxjEnwKQMFYNYmCGzM1TqnwxRDi8UyRzQpVfmDvk96fYN44oFG
HEX:  b6c1238de89e9defea3ea0712e08726e338928ac657c3409ebb93d9a0873797f</code></pre>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/82b5e115789ac3949bbe28bb975a2826.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<p><strong>Private key found!</strong></p>



<p><strong>Bitcoin wallet restored!</strong></p>



<figure class="wp-block-image"><img src="./Bitcoin Wallet Recovery via ECDSA Short Signatures - «CRYPTO DEEP TECH»_files/50fe20dbc6d9d6f4a4dbf43c6eaba268.png" alt="Bitcoin Wallet Recovery via ECDSA Short Signatures"></figure>



<blockquote class="wp-block-quote"><p><code>Короткие подписи ECDSA</code>is&nbsp;<em>a potential threat of losing coins</em>&nbsp;<code>BTC</code>&nbsp;,&nbsp;<em>so we strongly recommend everyone to always update the software and use only verified devices.</em></p></blockquote>



<p>This video was created for the&nbsp;&nbsp;<a href="https://cryptodeeptech.ru/" target="_blank" rel="noreferrer noopener"><strong>CRYPTO DEEP TECH</strong></a>&nbsp;portal &nbsp;to ensure the financial security of data and cryptography on elliptic curves&nbsp;&nbsp;<code>secp256k1</code>&nbsp;against weak signatures&nbsp;&nbsp;<code>ECDSA</code>&nbsp;in cryptocurrency&nbsp;<code>BITCOIN</code></p>



<p><a href="https://github.com/demining/CryptoDeepTools/tree/main/09BitcoinWalletRecovery" target="_blank" rel="noreferrer noopener"><strong>Source</strong></a></p>



<p><a href="https://t.me/cryptodeeptech"><strong>Telegram</strong></a><strong>&nbsp;:&nbsp;&nbsp;</strong><a href="https://t.me/cryptodeeptech" target="_blank" rel="noreferrer noopener"><strong><u>https://t.me/cryptodeeptech</u></strong></a></p>



<p><strong><a href="https://youtu.be/xBgjWE5tA7Y" target="_blank" rel="noreferrer noopener">Video: https://youtu.be/xBgjWE5tA7Y</a></strong></p>



<p><a href="https://cryptodeeptech.ru/shortest-ecdsa-signature" target="_blank" rel="noreferrer noopener"><strong>Source: https://cryptodeeptech.ru/shortest-ecdsa-signature</strong></a></p>
	</div><!-- .entry-content -->


---


|  | Donation Address |
| --- | --- |
| ♥ __BTC__ | 1Lw2kh9WzCActXSGHxyypGLkqQZfxDpw8v |
| ♥ __ETH__ | 0xaBd66CF90898517573f19184b3297d651f7b90bf |
