---
layout: post
title:  "AES/CBC/NoPadding实现"
date:   2017-05-23 09:00:00 +0800
categories: Linux
---
直接帖代码
<pre>
<code>
import base64
import hashlib
from Crypto import Random
from Crypto.Cipher import AES
import binascii

class AESCipher(object):

    def __init__(self, key,iv): 
        self.bs = 16
        #self.key = hashlib.sha256(key.encode()).digest()
        self.key = key
        self.iv = iv
        

    def encrypt(self, raw):
        raw = self._pad(raw)
        #iv = Random.new().read(AES.block_size)
        cipher = AES.new(self.key, AES.MODE_CBC, self.iv)
        encrypt_bytes = cipher.encrypt(raw)
        #return base64.b64encode(iv + cipher.encrypt(raw))
        return binascii.hexlify(encrypt_bytes)

    def decrypt(self, enc):
        #enc = base64.b64decode(enc)
        #iv = enc[:AES.block_size]
        enc = enc.decode('hex')
        cipher = AES.new(self.key, AES.MODE_CBC, self.iv)
        decrypt_str = cipher.decrypt(enc).decode('utf-8')
	#return self._unpad(cipher.decrypt(enc[AES.block_size:])).decode('utf-8')
        return decrypt_str        

    def _pad(self, s):
        #return s + (self.bs - len(s) % self.bs) * chr(self.bs - len(s) % self.bs)
        padding_char = ' '
        plaintext_bytes = s.encode(encoding='utf-8')
        x = len(plaintext_bytes) % self.bs
        pad_length = self.bs - x
        for i in range(0,pad_length):
            s = s + padding_char
        return s



    @staticmethod
    def _unpad(s):
        return s[:-ord(s[len(s)-1:])]

</code>
</pre>
