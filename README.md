# Arping

pythonによるArpingの実装をおこなう。

## 実行方法
```bash
$ python arping.py [IP Address]

// 例
$ python arping.py 192.0.0.23
```

## ARPとは
Address Resolution Protocolは、IPアドレスとMACアドレスを結びつけるプロトコル。
IPアドレスに対応するホスト、ルーターのMACアドレスを取得するために用いられる。

## 動作検証環境
Linux仮想環境にて動作確認を行った。

- ホストマシン: M1 Mac ARM
- 仮想環境ソフトウェア: UTM
- 仮想環境OS: ubuntu 20.04.2 server
```
$ uname -a
Linux linuxserver 5.4.0-72-generic #80-Ubuntu SMP Mon Apr 12 17:32:12 UTC 2021 aarch64 aarch64 aarch64 GNU/Linux
```

## メモ

- `Mac OS X`の`python`に`socket.AF_PACKET`が存在しない。`AF_PACKET`はethernatパケットを一から作成する際などに用いる。
似たようなものに`BPF`というものがあるらしい。[stackoverflow](https://stackoverflow.com/questions/7284853/af-packet-equivalent-under-mac-os-x-darwin)
> AF_PACKET is a low-level interface directly to network devices.  

- 同じコードを実行しても異なるARP応答が帰ってきた。
```bash
linuxbeginner@linuxserver:~$ sudo python3 arping.py
ARP sent....
b'\x00\x00\x00\x00\x00\x00\xee\xe2\x1d\x9c\xb1\xcb\x08\x06\x00\x01\x08\x00\x06\x04\x00\x01\xee\xe2\x1d\x9c\xb1\xcb\x7f\x00\x01\x01\x00\x00\x00\x00\x00\x00\n\x00\x02\x03'
==================================================
b"RU\n\x00\x02\x02\xee\xe2\x1d\x9c\xb1\xcb\x08\x00E\x10\x01<\xc0\xfc@\x00@\x06`\x9f\n\x00\x02\x0f\n\x00\x02\x02\x00\x16\xf1\x19\xcd\xf3\xa7\xea\x00,7;P\x18\xff\xff\xd8\x06\x00\x00\x1f8\xf0F~\xd9ce^\xe1\x99 \x0ci\xcf0v\xb2\x89\x12\xd0Wd\x00V~\xdd\x8f\xec^I\x02Z =\r\xcdnb.+$\xe4\xd6\xad\xa8\xc0N\x9f/6\x949\x89j\xf0\xe4T\xe1\x04h\x87\xe5u#\xb1\xc1@\xfd\x97\x97fT\xad\x97\xcdx\x05&\xa2\x8a\x95\x85Y\x0f\x948\xb6\xa8O\xf3\x9f\xca5\xda\xfaS\x11\x98\x05\x93\xb8\xf9\xa2\x10\xa1!\xaa\x0c\xdc\x01e\x8eJJ\xbc!|\xdd\x83\xc7\xde\xf8\xb8\xc9y\xcb\xce\x81\xd5\xdb\x07v\xc4\xe756\xfc\xd0V\x02HW\xb9\xfbH\x87\x12\x99\x1f)\\X\xa9\x0c\xef\xe8\n6\xa2\xc8qv\x9aibX\xa9W\xcd5\x0b\xf3\xbc\x86\xa4\x16\xa0\x89z\x14\x03+\x94rU\xb7\xb2\x85\xd5\x06)=W\xd1\xa0':6\xf8\xb2d\x8e\xac\xae\xb3\xec\xc8\x19d\xcc1\x1d<\xd6\xc2}\xe9\x86\xa7j-8$\xd7\xc3\x18-_\xd9D\xb6gq\xd6\x1aQ1\xf4N\x15#:@q\xff\x11\xa7\xa7\x95\x06\xaep0M^${\xf7\xdd\x7f{\x0f\x9e\x17\x06}_R,+O\x8b\x90x\xd0"
```

```bash
linuxbeginner@linuxserver:~$ sudo python3 arping.py
ARP sent....
b'\x00\x00\x00\x00\x00\x00\xee\xe2\x1d\x9c\xb1\xcb\x08\x06\x00\x01\x08\x00\x06\x04\x00\x01\xee\xe2\x1d\x9c\xb1\xcb\x7f\x00\x01\x01\x00\x00\x00\x00\x00\x00\n\x00\x02\x03'
==================================================
b'\xee\xe2\x1d\x9c\xb1\xcbRU\n\x00\x02\x03\x08\x06\x00\x01\x08\x00\x06\x04\x00\x02RU\n\x00\x02\x03\n\x00\x02\x03\xee\xe2\x1d\x9c\xb1\xcb\x7f\x00\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'
```

## 参考

- マスタリングTCP/IP 入門編　第5版
- [PythonでARPを使ったネットワークプログラミング　ARPスプーフィングを試す](https://euniclus.com/article/python-arp-spoofing/)
