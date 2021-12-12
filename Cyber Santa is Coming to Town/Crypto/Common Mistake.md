### encrypted.txt
```json

{'n': '0xa96e6f96f6aedd5f9f6a169229f11b6fab589bf6361c5268f8217b7fad96708cfbee7857573ac606d7569b44b02afcfcfdd93c21838af933366de22a6116a2a3dee1c0015457c4935991d97014804d3d3e0d2be03ad42f675f20f41ea2afbb70c0e2a79b49789131c2f28fe8214b4506db353a9a8093dc7779ec847c2bea690e653d388e2faff459e24738cd3659d9ede795e0d1f8821fd5b49224cb47ae66f9ae3c58fa66db5ea9f73d7b741939048a242e91224f98daf0641e8a8ff19b58fb8c49b1a5abb059f44249dfd611515115a144cc7c2ca29357af46a9dc1800ae9330778ff1b7a8e45321147453cf17ef3a2111ad33bfeba2b62a047fa6a7af0eef', 'e': '0x10001', 'ct': '0x55cfe232610aa54dffcfb346117f0a38c77a33a2c67addf7a0368c93ec5c3e1baec9d3fe35a123960edc2cbdc238f332507b044d5dee1110f49311efc55a2efd3cf041bfb27130c2266e8dc61e5b99f275665823f584bc6139be4c153cdcf153bf4247fb3f57283a53e8733f982d790a74e99a5b10429012bc865296f0d4f408f65ee02cf41879543460ffc79e84615cc2515ce9ba20fe5992b427e0bbec6681911a9e6c6bbc3ca36c9eb8923ef333fb7e02e82c7bfb65b80710d78372a55432a1442d75cad5b562209bed4f85245f0157a09ce10718bbcef2b294dffb3f00a5a804ed7ba4fb680eea86e366e4f0b0a6d804e61a3b9d57afb92ecb147a769874'}
{'n': '0xa96e6f96f6aedd5f9f6a169229f11b6fab589bf6361c5268f8217b7fad96708cfbee7857573ac606d7569b44b02afcfcfdd93c21838af933366de22a6116a2a3dee1c0015457c4935991d97014804d3d3e0d2be03ad42f675f20f41ea2afbb70c0e2a79b49789131c2f28fe8214b4506db353a9a8093dc7779ec847c2bea690e653d388e2faff459e24738cd3659d9ede795e0d1f8821fd5b49224cb47ae66f9ae3c58fa66db5ea9f73d7b741939048a242e91224f98daf0641e8a8ff19b58fb8c49b1a5abb059f44249dfd611515115a144cc7c2ca29357af46a9dc1800ae9330778ff1b7a8e45321147453cf17ef3a2111ad33bfeba2b62a047fa6a7af0eef', 'e': '0x23', 'ct': '0x79834ce329453d3c4af06789e9dd654e43c16a85d8ba0dfa443aefe1ab4912a12a43b44f58f0b617662a459915e0c92a2429868a6b1d7aaaba500254c7eceba0a2df7144863f1889fab44122c9f355b74e3f357d17f0e693f261c0b9cefd07ca3d1b36563a8a8c985e211f9954ce07d4f75db40ce96feb6c91211a9ff9c0a21cad6c5090acf48bfd88042ad3c243850ad3afd6c33dd343c793c0fa2f98b4eabea399409c1966013a884368fc92310ebcb3be81d3702b936e7e883eeb94c2ebb0f9e5e6d3978c1f1f9c5a10e23a9d3252daac87f9bb748c961d3d361cc7dacb9da38ab8f2a1595d7a2eba5dce5abee659ad91a15b553d6e32d8118d1123859208'}
```

n = modulus
e = encryption
ct = cipher text

### Attack Type : RSA-common modulus
[reference](https://infosecwriteups.com/rsa-attacks-common-modulus-7bdb34f331a5)

Using the RSA CTF tool [RSACTFTOOL](https://github.com/Ganapati/RsaCtfTool)
to generate public key

Example: 
```bash
python RsaCtfTool.py --createpub -n 0xa96e6f96f6aedd5f9f6a169229f11b6fab589bf6361c5268f8217b7fad96708cfbee7857573ac606d7569b44b02afcfcfdd93c21838af933366de22a6116a2a3dee1c0015457c4935991d97014804d3d3e0d2be03ad42f675f20f41ea2afbb70c0e2a79b49789131c2f28fe8214b4506db353a9a8093dc7779ec847c2bea690e653d388e2faff459e24738cd3659d9ede795e0d1f8821fd5b49224cb47ae66f9ae3c58fa66db5ea9f73d7b741939048a242e91224f98daf0641e8a8ff19b58fb8c49b1a5abb059f44249dfd611515115a144cc7c2ca29357af46a9dc1800ae9330778ff1b7a8e45321147453cf17ef3a2111ad33bfeba2b62a047fa6a7af0eef -e 0x10001
```

key 1:
``` bash
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqW5vlvau3V+fahaSKfEb
b6tYm/Y2HFJo+CF7f62WcIz77nhXVzrGBtdWm0SwKvz8/dk8IYOK+TM2beIqYRai
o97hwAFUV8STWZHZcBSATT0+DSvgOtQvZ18g9B6ir7twwOKnm0l4kTHC8o/oIUtF
Bts1OpqAk9x3eeyEfCvqaQ5lPTiOL6/0WeJHOM02Wdnt55Xg0fiCH9W0kiTLR65m
+a48WPpm216p9z17dBk5BIokLpEiT5ja8GQeio/xm1j7jEmxpauwWfRCSd/WEVFR
FaFEzHwsopNXr0ap3BgArpMwd4/xt6jkUyEUdFPPF+86IRGtM7/rorYqBH+mp68O
7wIDAQAB
-----END PUBLIC KEY-----
```
key 2:
```bash
-----BEGIN PUBLIC KEY-----
MIIBIDANBgkqhkiG9w0BAQEFAAOCAQ0AMIIBCAKCAQEAqW5vlvau3V+fahaSKfEb
b6tYm/Y2HFJo+CF7f62WcIz77nhXVzrGBtdWm0SwKvz8/dk8IYOK+TM2beIqYRai
o97hwAFUV8STWZHZcBSATT0+DSvgOtQvZ18g9B6ir7twwOKnm0l4kTHC8o/oIUtF
Bts1OpqAk9x3eeyEfCvqaQ5lPTiOL6/0WeJHOM02Wdnt55Xg0fiCH9W0kiTLR65m
+a48WPpm216p9z17dBk5BIokLpEiT5ja8GQeio/xm1j7jEmxpauwWfRCSd/WEVFR
FaFEzHwsopNXr0ap3BgArpMwd4/xt6jkUyEUdFPPF+86IRGtM7/rorYqBH+mp68O
7wIBIw==
-----END PUBLIC KEY-----

```

### using the RSA-Common-Modulus-Attack Tool
[github link for RSA common-modulus-attack tool](https://github.com/HexPandaa/RSA-Common-Modulus-Attack/blob/master/rsa-cm.py)

```python
# c1 and c2 need to be in b64
c1 = b64decode(args.c1.read())
c1 = bytes_to_long(c1)
c2 = b64decode(args.c2.read())
c2 = bytes_to_long(c2)

```

c1 in base64
```bash
Vc/iMmEKpU3/z7NGEX8KOMd6M6LGet33oDaMk+xcPhuuydP+NaEjlg7cLL3COPMyUHsETV3uERD0kxHvxVou/TzwQb+ycTDCJm6Nxh5bmfJ1Zlgj9YS8YTm+TBU83PFTv0JH+z9XKDpT6HM/mC15CnTpmlsQQpASvIZSlvDU9Aj2XuAs9Bh5VDRg/8eehGFcwlFc6bog/lmStCfgu+xmgZEanmxrvDyjbJ64kj7zM/t+Augse/tluAcQ14NypVQyoUQtdcrVtWIgm+1PhSRfAVegnOEHGLvO8rKU3/s/AKWoBO17pPtoDuqG42bk8LCm2ATmGjudV6+5LssUenaYdA==
```
c2 in base64
```bash
eYNM4ylFPTxK8GeJ6d1lTkPBaoXYug36RDrv4atJEqEqQ7RPWPC2F2YqRZkV4MkqJCmGimsdeqq6UAJUx+zroKLfcUSGPxiJ+rRBIsnzVbdOPzV9F/Dmk/JhwLnO/QfKPRs2VjqKjJheIR+ZVM4H1PddtAzpb+tskSEan/nAohytbFCQrPSL/YgEKtPCQ4UK06/Wwz3TQ8eTwPovmLTqvqOZQJwZZgE6iENo/JIxDryzvoHTcCuTbn6IPuuUwuuw+eXm05eMHx+cWhDiOp0yUtqsh/m7dIyWHT02HMfay52jirjyoVldei66Xc5avuZZrZGhW1U9bjLYEY0RI4WSCA==
```

run the script 
```bash
python rsa-cm.py -k1 k1.pub -k2 k2.pub -c1 1.b64 -c2 2.b64 

```

output
```bash
[+] Recovered message:                                                                                                                          
154494104151501230741951698942733388017524925426108770319061863579333462036794337421344018523054973                                             
[+] Recovered bytes:                                                                                                                            
b'HTB{c0mm0n_m0d_4774ck_15_4n07h3r_cl4ss1c}'
```
> Learn From [CryptoCat](https://www.youtube.com/watch?v=20FkOdoMiRU)