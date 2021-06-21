# FOS2POP
[FOSSIL](https://fossil-scm.org/ "FOSSIL") TO [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "POP3") GATEWAY

```bash
# tree pop3 -d
.
├── bin
├── etc
└── var
    ├── log
    ├── mbox
    │   ├── fossil
    │   ├── pikchr
    │   └── sqlite
    └── repo
        ├── fossil
        │   └── forum
        ├── pikchr
        │   └── home
        └── sqlite
            └── forum
```

```bash
# cd ~/pop3/var/repo/fossil/forum

# fossil remote-url
https://fossil-scm.org/forum

# fossil pull
Pull from https://fossil-scm.org/forum
Round-trips: 1   Artifacts sent: 0  received: 0
Pull done, sent: 586  received: 2078  ip: 45.33.6.223

# fossil timeline | head
=== 2021-06-21 ===
09:30:03 [25c9155301] Reply: Unversioned file does not update (user: torstenberg)

# art2eml 25c9155301 | head
Return-Path: <>
From: torstenberg <noreplybc1ca445a@fossil-scm.org>
To: Fossil Forum <fossil-forum@fossil-scm.org>
Date: Mon, 21 Jun 2021 09:30:03 -0000
Subject: Re: Unversioned file does not update
Message-Id: <25c915530181115bc5e881c9b3e4ff7e@fossil-scm.org>
In-Reply-To: <7c2f48073c85cdbca0906b4299f31f5b@fossil-scm.org>
References: <d3dbd763374f2e3d79ddeee772fb9c50@fossil-scm.org>
 <273e43c35daafb31a877acb8af8c2a70@fossil-scm.org>
 <bdb7f7ba0b6a3e974df72eeea656e693@fossil-scm.org>

# repo2mbox ~/pop3/var/mbox/fossil
1624212685  aa3fd34d41cc57bf0032432bc5e17b3ece819318135fb83e939c7ee21b20a778  ~/pop3/var/mbox/fossil/QV0IJ1.aa3fd34d41.eml  2021-06-20T18:13:15Z
1624230819  a0286f328e37b7cd0634972f73828112dfb61fce56bb9a3adc8df24b2c4b7153  ~/pop3/var/mbox/fossil/QV0WIR.a0286f328e.eml  2021-06-20T23:14:10Z
1624232061  4fff4f275d441be6e9dfbbe57d2be014cc889ae5be4ea6186a5637b00ad00a1e  ~/pop3/var/mbox/fossil/QV0XH9.4fff4f275d.eml  2021-06-20T23:39:16Z
1624267803  25c915530181115bc5e881c9b3e4ff7ecae8b63002bfcf1864619c00ea5abfcd  ~/pop3/var/mbox/fossil/QV1P23.25c9155301.eml  2021-06-21T09:31:04Z

# nohup tcpserver -v -c42 -o -D -H -P -l 0 -R pop.textprotocol.org 1110 timeout 5m ~/pop3/bin/pop3 ~/pop3/var/mbox > ~/pop3/var/log/pop3.log &
```

```bash
# { echo 'capa'; echo 'user fossil'; echo 'pass 10'; echo 'stat'; echo 'list'; echo 'uidl'; echo 'top 10 0'; } | nc pop.textprotocol.org 1110
+OK
+OK
EXPIRE NEVER
LOGIN-DELAY 900
PIPELINING
TOP
UIDL
USER
.
+OK
+OK
+OK 10 28679
+OK
1 2344
2 6619
3 3565
4 2705
5 2343
6 3053
7 1604
8 1689
9 2699
10 2058
.
+OK
1 QUYWZG4348303a42
2 QUZ00P079483bddb
3 QUZ0EG7d8721a4c3
4 QUZ0UR9793737832
5 QUZ326836205a0f6
6 QV0HQI44defd47ce
7 QV0IJ1aa3fd34d41
8 QV0WIRa0286f328e
9 QV0XH94fff4f275d
10 QV1P2325c9155301
.
+OK
Return-Path: <>
From: torstenberg <noreplybc1ca445a@fossil-scm.org>
To: Fossil Forum <fossil-forum@fossil-scm.org>
Date: Mon, 21 Jun 2021 09:30:03 -0000
Subject: Re: Unversioned file does not update
Message-Id: <25c915530181115bc5e881c9b3e4ff7e@fossil-scm.org>
In-Reply-To: <7c2f48073c85cdbca0906b4299f31f5b@fossil-scm.org>
References: <d3dbd763374f2e3d79ddeee772fb9c50@fossil-scm.org>
 <273e43c35daafb31a877acb8af8c2a70@fossil-scm.org>
 <bdb7f7ba0b6a3e974df72eeea656e693@fossil-scm.org>
 <18fca67f866feca81ec8f60698e116f0@fossil-scm.org>
 <7c2f48073c85cdbca0906b4299f31f5b@fossil-scm.org>
Archived-At: <https://fossil-scm.org/forum/forumpost/25c915530181115bc5e881c9b3e4ff7e>
List-Archive: <https://fossil-scm.org/forum>
List-Id: Forum for discussion of the Fossil DVCS <fossil-forum@fossil-scm.org>
List-Post: NO
Importance: low
Precedence: list
Mime-Version: 1.0
Content-Type: multipart/mixed; boundary="10XF0551135519C52B4B61=_"

.
```
