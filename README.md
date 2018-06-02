# Heroku app
https://ticketplatform.herokuapp.com/
Contract 0x097682dDe6a84acEa746CddE2e08a78D9A591c5a


# BTC first part
Проверить баланс текущего аккаунта:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getbalance
0.00000000
```


Выведем список аккаунтов
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat listaccounts
{
}
```

Видим, что есть аккаунт "по-умолчанию" с пустым названием "".

Сгенерируем первый блок в тестовом блокчейне
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat generate 1
[
  "5021193786d6bf398b17798c5b50d798c0e370f1c94d4ec0d5050771a57de382"
]
```

Проверим список транзакций:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat listtransactions
[
  {
    "account": "",
    "address": "n3txHXD3KmBfLLaVNLD3175VkHzFePiCWx",
    "category": "immature",
    "amount": 50.00000000,
    "vout": 0,
    "confirmations": 1,
    "generated": true,
    "blockhash": "5021193786d6bf398b17798c5b50d798c0e370f1c94d4ec0d5050771a57de3
82",
    "blockindex": 0,
    "blocktime": 1527795939,
    "txid": "15105d65768f688b011ee4d2ae6418551e664b17e71c4b5094441dcefa833a02",
    "walletconflicts": [
    ],
    "time": 1527795939,
    "timereceived": 1527795939,
    "bip125-replaceable": "no"
  }
]
```
Видим, что всего есть 1 транзакция создания 50 BTC (coinbase-транзакция).

Скопируем значения поля "txid" **&lt;txid&gt;** для использования в дальшейнем в примере (будет переводить эти 50 BTC).

txid = 15105d65768f688b011ee4d2ae6418551e664b17e71c4b5094441dcefa833a02

Еще раз проверить баланс текущего аккаунта:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getbalance
0.00000000`
```

Все еще 0. Дело в том, что трананзакция создания 50 BTC еще недостаточно "старая".


В информации о кошельке видим immature balance:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getwalletinfo
{
  "walletname": "wallet.dat",
  "walletversion": 159900,
  "balance": 0.00000000,
  "unconfirmed_balance": 0.00000000,
  "immature_balance": 50.00000000,
  "txcount": 1,
  "keypoololdest": 1527795352,
  "keypoolsize": 999,
  "keypoolsize_hd_internal": 1000,
  "paytxfee": 0.00000000,
  "hdmasterkeyid": "af8cdb7f57f450a1a35b204ba0ef96eb0f6de4c3"
}
```
В выводе видим, "immature_balance": 50.00000000


Создаем новый аккаунт и адрес в нем (будем на него переводить средства)
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getnewaddress "account2"

2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR
```
Записываем адрес **&lt;address2&gt;**

address2 = 2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR


Создаем для аккаунта аккаунт "по-умолчанию" адрес для "сдачи":
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getnewaddress ""
2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW
```
Записываем **&lt;address3&gt;**

address3 = 2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW


Проверим привязку адресов к аккаунтам:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getaddressesbyaccount ""

[
  "2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW"
]
```
и
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getaddressesbyaccount "a
ccount2"
[
  "2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR"
]
```
Выводим список аккаунтов
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat listaccounts
{
  "": 0.00000000,
  "account2": 0.00000000
}
```
На аккаунте "" (аккаунт "по-умолчанию") 0 BTC

На аккаунте "account2" 0 BTC


Сгенерируем еще 100 блоков, чтобы разблокировать средства в первом блоке (не меньше, см. https://bitcoin.org/en/developer-examples#regtest-mode)
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat generate 100
[
  "103d05fd682f6f6d607612a046a809bc964871545c4affcbd7581ab4e4db1b48",
  "21dbcf9cb8dd890aa969d07dd0557018e474ac3e40a79e2dac1019a29f006008",
  "735d7ab81f2a84e52954c708fdf1934b79edc1f8c7f477e99d05d67b8eccd8a6",
  "4c4e2d61cdb045edc1e83e75af8d87aca1c267d3de78a3e96bbec3031405322f",
  "27220d82fcc445cea8db7a673c67fc87dc7ae5f7fdbc456c6831ae6fac5337a1",
  "6f5281b6e59e1fdc6c5ed472063e8d0cb9f7fe59fa147f842c553ea542201794",
  "7a0c7edef803f0e52ea0e4424aa347c601bd8ae69f977144f4b42850bf9586fd",
  "7f18228b8ba208cd1700d600ecedd3b0d55ad58ec39d59655bfa7b958e05dd2b",
  "05fa4c582cb020e6e68f699febe611557709a446ef65b33b707e9ec1fa947c2c",
  "505b1d96a53c0121e98da7a42bcf3760ddc2f5fc49bffcf318b0819799efe7ae",
  "333f842d79e2d32333eb300a988a30f7e4955f449d45d4ec91b5108fdf4304ae",
  "345a9d5e56d94cd7c948e81a1727263cb5ec22b37158672c8c7501896c67ab26",
  "5934a08d4ef4cdff7914ee6cd6fd4735b18e47d8239069784bfe6526d3d1b094",
  "0288720ed8279a157ac511772ca1ddc8207121893a24f5e3b1d2af3e436b2df5",
  "6295d1b8b33f47045dfc944a8da2078574626b599e431b74f95dd1778b2bdeb2",
  "1604ad62302a0f5fc50a890f0877e4a04b0190866953a710895f0432e1dff02b",
  "6ea671095c89ae0c1fa0289ef21e44bef1610380f9d4d1b30206fbe2c4c2b42a",
  "40b4971f3a2a2faf71cc4006ed167a67a74ec80a611045d3dce050ba5eb6ab6d",
  "4c93811e11c731e730099823a46cffcbf7fc0afa68ee679f1ca6b97bdfb5b393",
  "65a104c69502b58d63a0cd37f3feb14e254301520651646be3e21d95fd0db5e2",
  "08757aff00253b76d0a3a14201570fe38651d22fe8f44e74db0f0b01f4b8b9bb",
  "52cda3f7b4485216d3394d1934d30d479b5ca5aaf58f8a97ad5b9013f395183e",
  "19a70ae46c9ffcbd82c7d85995fe67d8d75fcc58bab4ed3056aa15dad7c81c94",
  "4ce64f20f58df4527e656c48668e48f0a5537f804558a9252b6e6bcf2f2f3d03",
  "51239d38f1910987fb0b7be2aaf4d10e5616d76a143f5b8ad54ffae698a16c2c",
  "065d0f222ed9807914d2a61a71043a2e141659ad8c013d77a06704c127c6d381",
  "5c666b13b9874f325a07a37c751fd11f56824f53e378a262e542227d791e5924",
  "60fee62d3dde919b96cc021aad5917a8a60734eec1dfca7ea4032bd90da14a0f",
  "213178975b9b6574395e749084503b1d632b685fa9b87b3cb605370d034972a3",
  "2ab93a3bc2162a9ad968efb51f68002338d078739e047b2f35afd7acfa8bdf29",
  "6a6432500892be65ff392ec85439f2abb9529714b9395dbedf3493ce33857ac8",
  "117dfca151e43bdb9435526d481d8da4dd5c9de2892e550a72e85bf27f1e666a",
  "68fb574e599d1f7327073012ad541814dbc23f17888ba9b453c7058bc2d34cd3",
  "12dbc09caccd4867b07cd5b56518e4937dce2dc88190f1a467661fd8d046e02c",
  "6f0f33e23d5e1771b167fa5ce28153b4527a371abc65377cd405d75089f62809",
  "25e652714a12404c7acb8c75bccbbfe58d96efe1f076f9ff7de3dc791ec609ee",
  "56282ee0625a146cccc62ed526584872f189c2591721b665f87b1754fbd1832a",
  "745c0b4aa53508978cf6ce4c1c04ba42b248cafe8fada6d882df026841a701bb",
  "7c57699e4739bce408fcf27fbff3db1852e0c8e5f1725e1b9e16c51586d576c5",
  "7c56fffc1fad50d1fd5e66f22d4ed1e9d479fb26a1c5063355f1a72c059d4cc7",
  "484a2bf7b3b3c40ab88ab2634192b6518c97371d70aa0ae437ff7a41ff4a26ea",
  "4f4a7d0cbfd1d17c76113be6ca93fabc5ee95147ab4bbdcd116b37e04a8a4445",
  "0c500a2d587c21d3c2c148e4a0f1aef5c8a1dfbb5712371df47eaaa17edd2dc8",
  "56fbb7cd07dcc8bbce5b8f96900668d0928ad2a5ab12828509f6770dc9371502",
  "4130c98854dd029f634828aeb6b888bdd3b9abccf00534dee09e3eff9346c421",
  "48fd836fbcb41e28fed782d32b68f75b14472355722b3daa2488a59e44cf28c7",
  "6d52cbcc49589ebc70d780a23f20f226278bb33660efce8d61c0f290196d8b0e",
  "5de3d7514bfb0601c1d25e7071e4cc6cf8e761d656b742ac74bcc2fb51f72af1",
  "574f8f3c65354ab6d1746e9729f39993413f0e4aa5718833c783a3545bce44a9",
  "521ffb57e03110a5dd9b6f01e976e1a436a98f2a3840a0d9d9cf0e07d5194b84",
  "55e081ab8e59dbe8a1ab318031c86d3afe15f9813548c3219106205b45c32aa0",
  "0711f45664a1198ae6f64cbc4f08c3f5fb982c944aa9c536d72c1f79a1063476",
  "068343696172becf9413cacfc44af6cfd1fd6890cbf8d22958d659bedc970d34",
  "039865af9e8877b12d3393654fe5b2bcc930a8090e62f0f992e151f78237d5ba",
  "4f170ef71bfbe98ba1480b191c1497c4b0e82050b5e9c0268c2837b18846f3f5",
  "1fdac4c02725b15b089e9c0bcca36e3715575bc10d7972227d277a27a939ee93",
  "302a32d483ffaded780fa5d3597bde929b51fc4434d34085c0648a740c2403b3",
  "412def45f9409b7e4d91ce7423ef016aeb9a3048f27b0e9ab2155413d8554c17",
  "2c2b2971440ea37d6392162518396940f9b9e7771b7412dc79776869f9edc722",
  "0c5ea634a3cdbf0b483eafa50405f11a80eca1f32322b10de68a26a87c7eb5d8",
  "0106386de0444e93cd3f5b28812cacebd62f5daf5147575628b942e539cad21a",
  "69206a2313f18c9b3cf8b728cd0c97337450fe0fcab2cc8dcfb2d856598fb0af",
  "44011486ab69e3d7e4b2697d07299c4b5ed7294cdea2026e484bd292c05e6892",
  "1c1c2420c4e1c62add267cb175f92cd99f6471d84923230ac87bebae9f54bcb9",
  "417379a67b34f95e3a51e22781b5b752436c1f3cc31a510e590c0e4102d99d9b",
  "0e7cadcc668853365d99f297109fcf7dca329f585814f87b19a8870a42a09559",
  "784f045030917b18f3dd49f9bdf40a7cc15c6b727ec1ad5814c752ec7410800a",
  "7aa27a1b2ab45af8c3e4496904533a3ea24ddba0d791dbb8a82273cc579899ea",
  "0fecfd51faf83a8e00a79fd755af371f050e486316cd8dc63106aa73ae98db63",
  "1db419f87f95952faeec02ff20bdbb5b79c5baccf1918eb7b6e0e66efaba7f41",
  "29e82cdd40be9681506a45ba0b5c9b23e57226c55c38e58499c9d85c2ee8ff45",
  "70acb9c31f1e994b91e040eed503e4a1b2ea826318b2cc911dced51c50b419d2",
  "0c41c31c8d88fe64c98dcddb20b9544eae31f5086609537f50199c57d1d00f18",
  "213fb294c398fac65cfcb0f269fb80b153bbd8181c6220db7803616f8815d72f",
  "7ab3ac789ecdb9e674466b5fe396b1cc1403ade08ad0647be813ee8c16e4467c",
  "0750a9fe306b81e992b1a5a28d0c58240cc6307a2b1e06bf2c2b83574e295c99",
  "33935eb6a7fd140a0a56b47e87fe0cc249910b06e762aff923b8762670c7b69e",
  "23716d1f782a58cf2a5c6f47e2b4b2ec33be8095daf5edc045406c1c24adf3d4",
  "029ddc1a861429f8f38309222906e8403c50dc916302d3629b3ed8a917b9542c",
  "2bdacb413379e187050b074b0da9ac6387c6a858f83bbd06ba2c4636def6a403",
  "6cedf2031c1014573389e08e779798c0d89078181053d7986675924b14c2ed9e",
  "5f32597f324f8b5125e2521d7cd0a0c0434b15024ec3180346f93fd9396d7e24",
  "0ba369159a556049b6abcac09bfc8a53bf98569604d3c1329751f0b10963992f",
  "416f315927f95fc294a797c8e89285dc92da9757b5cdd203ea36a07b0db80a73",
  "134f2d6d835db346fdcd87313d644ab8f644768fba2b5a15c33916753722ca82",
  "54e892dfdc923b9544884296fc367ba7b47a52907780f62bb49cf772ea602c77",
  "2bbdc283f17e13f5e6e8487ef71f74658c7fc31718ec489bea0b028896b33229",
  "2388920119c1184e7ed3cd625706fe6b41a6c073ddd235056fb514503ef422f7",
  "59f76efc0695744349440161fdebe62eebe3e909f4f1794607ecb910425bd8ad",
  "1effca91876ff2fbd26cc65c7a3864559d628990fd76412de703badc81522018",
  "00131f761e331a9ae0788c82331bc47d39cb1c6f9e6e4ccea418392f1cce6b2f",
  "3530ef4c9ae632a6de3572aa6e0c80e96bbb13b8cca54d4cd6e55938c910879b",
  "514f0fdb52f2a289b4c88d496fcfd9ea19a584781d00befbf8db28e2d3d5fbfa",
  "28fd4088dec98b0a7b25c00ed363e9cfba2589089fc1585f245bb73a894fb82c",
  "0b5a477aef52164907f8cf366b6e53ab89ef0290178051d898c96058f063cae2",
  "24350104d0c6397d1761c27844f190e1f53d931d328b5446259a9acdce98971c",
  "525ae7b0e0fb133edb1a0477175043eea61a54327378fc9ef90911092c4d2e79",
  "21abd93bac4be5343ee15319899b034919843156df628af557253ebc0f59903b",
  "7f392adb8bf0d3c9d227635eb8af5d0e8a9f28edf5a54eb50f4491c5a27b0073",
  "5006daecdb77930eab755a3dec2cfad5f96e8b875f2908a56286ce9d4d50354f"
]
```

Выводим список аккаунтов
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat listaccounts
{
  "": 50.00000000,
  "account2": 0.00000000
}
```


На аккаунте "" (аккаунт "по-умолчанию") 50 BTC

На аккаунте "account2" 0 BTC


Сделаем перевод между адресами аккаунта по-умолчанию и аккаунта 2.

Создаем транзакцию перевода 10 BTC с непотраченного output coinbase-транзакции самого первого блока на **&lt;address2&gt;** со сдачей на **&lt;address3&gt;**:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat createrawtransaction "[{
\"txid\": \"15105d65768f688b011ee4d2ae6418551e664b17e71c4b5094441dcefa833a02\",\
"vout\":0}]" "{\"2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR\": 10, \"2N427Z1UiWBjdzmt35
nafzjBbnDymYD6qGW\": 39.9999 }"
0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d10150000000000ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006bee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000
```
Получаем hex транзакции **&lt;raw transaction hex&gt;**

hex =  0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d10150000000000ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006bee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000*


Подписываем транзакцию:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat signrawtransaction 0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d10150000000000ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006bee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000
{
  "hex": "0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d1015000000004948304502210099ea8a9e517e4c281c3e0cbe2c247ff5a3df534806c5534d4b25afc9ae5dd692022016c219c534e4ba05e23dbbd89c86ac5e93376f9cae84ae1dcd16d12a96cad7df01ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006bee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000",
  "complete": true
}
```

Получаем **&lt;signed raw transaction hex&gt;**

Ожидаем "complete": true

signed raw transaction hex = 0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d1015000000004948304502210099ea8a9e517e4c281c3e0cbe2c247ff5a3df534806c5534d4b25afc9ae5dd692022016c219c534e4ba05e23dbbd89c86ac5e93376f9cae84ae1dcd16d12a96cad7df01ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006bee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000

Проверяем, что транзакции нет в мемпуле (она еще не отправлена):
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getrawmempool
[
]
```
Получаем: пустой массив (мемпул пуст)


Отправляем транзакцию:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat sendrawtransaction 02000
00001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d101500000000494
8304502210099ea8a9e517e4c281c3e0cbe2c247ff5a3df534806c5534d4b25afc9ae5dd69202201
6c219c534e4ba05e23dbbd89c86ac5e93376f9cae84ae1dcd16d12a96cad7df01ffffffff0200ca9
a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006bee0000000017a91
4762e9a92f0d2616a73c8e6bec23adf61057d02968700000000
c6b62d9a3a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191
```

В случае успеха выводится хеш нашей транзакции перевода  **&lt;transaction hash&gt;**

transaction hash = c6b62d9a3a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191


Можем посмотреть содержание транзакции:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat gettransaction c6b62d9a3
a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191
{
  "amount": 0.00000000,
  "fee": -0.00010000,
  "confirmations": 0,
  "trusted": true,
  "txid": "c6b62d9a3a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191",
  "walletconflicts": [
  ],
  "time": 1527797743,
  "timereceived": 1527797743,
  "bip125-replaceable": "no",
  "details": [
    {
      "account": "",
      "address": "2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR",
      "category": "send",
      "amount": -10.00000000,
      "label": "account2",
      "vout": 0,
      "fee": -0.00010000,
      "abandoned": false
    },
    {
      "account": "",
      "address": "2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW",
      "category": "send",
      "amount": -39.99990000,
      "label": "",
      "vout": 1,
      "fee": -0.00010000,
      "abandoned": false
    },
    {
      "account": "account2",
      "address": "2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR",
      "category": "receive",
      "amount": 10.00000000,
      "label": "account2",
      "vout": 0
    },
    {
      "account": "",
      "address": "2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW",
      "category": "receive",
      "amount": 39.99990000,
      "label": "",
      "vout": 1
    }
  ],
  "hex": "0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d
1015000000004948304502210099ea8a9e517e4c281c3e0cbe2c247ff5a3df534806c5534d4b25af
c9ae5dd692022016c219c534e4ba05e23dbbd89c86ac5e93376f9cae84ae1dcd16d12a96cad7df01
ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006b
ee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000"
}
```

Проверяем, что транзакция появилась в мемпуле (она еще не включена в блок):
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getrawmempool
[
  "c6b62d9a3a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191"
]
```
В пуле появилась транзакция **&lt;transaction hash&gt;**.


Генерируем еще 1 блок, чтобы транзакция из mempool попала в блок. При этом из состава immature в состав mature передет еще несколько блоков, которые пополнят баланс первого аккаунта "":
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat generate 1
[
  "54dcd3994ff003af7efd14a1591d048a3fe28e180103678e02065e0e0bb3040c"
]
```

Проверяем mempool:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat getrawmempool
[
]
```
Транзакций нет, так как наша транзакция перевода замайнена (включена в блок).


Смотрим балансы:
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat listaccounts
{
  "": 89.99990000,
  "account2": 10.00000000
}
```

1.1. Объясните, почему при вызове getbalance отображается 99.99990000 BTC? Где еще 0.0001 BTC?
Если вывести транзакцию, то видно, что 0,0001 - это стоимость fee
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat gettransaction c6b62d9a3
a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191
{
  "amount": 0.00000000,
  "fee": -0.00010000,
  "confirmations": 0,
  "trusted": true,
  "txid": "c6b62d9a3a32e919d7977d5b5429f31ea03edc20f0651ec2857350f34a027191",
  "walletconflicts": [
  ],
  "time": 1527797743,
  "timereceived": 1527797743,
  "bip125-replaceable": "no",
  "details": [
    {
      "account": "",
      "address": "2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR",
      "category": "send",
      "amount": -10.00000000,
      "label": "account2",
      "vout": 0,
      "fee": -0.00010000,
      "abandoned": false
    },
    {
      "account": "",
      "address": "2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW",
      "category": "send",
      "amount": -39.99990000,
      "label": "",
      "vout": 1,
!!!!  "fee": -0.00010000, !!!!
      "abandoned": false
    },
    {
      "account": "account2",
      "address": "2N4VPfhJWD6c7Z1QZAZiESanVkAqNPnBtzR",
      "category": "receive",
      "amount": 10.00000000,
      "label": "account2",
      "vout": 0
    },
    {
      "account": "",
      "address": "2N427Z1UiWBjdzmt35nafzjBbnDymYD6qGW",
      "category": "receive",
      "amount": 39.99990000,
      "label": "",
      "vout": 1
    }
  ],
  "hex": "0200000001023a83face1d4494504b1ce7174b661e551864aed2e41e018b688f76655d
1015000000004948304502210099ea8a9e517e4c281c3e0cbe2c247ff5a3df534806c5534d4b25af
c9ae5dd692022016c219c534e4ba05e23dbbd89c86ac5e93376f9cae84ae1dcd16d12a96cad7df01
ffffffff0200ca9a3b0000000017a9147b574981ca6594b807e9181fc26c712e572bb5d387f0006b
ee0000000017a914762e9a92f0d2616a73c8e6bec23adf61057d02968700000000"
}
```

1.2. Что будет с балансами аккаунтов при выполнении generate 1 (создании еще одного блока)?
При генерации блока аккаунт "по умолчанию" получает 50BTC (премия):
```
D:\Projects\BlockchainDeveloper\week6\btc>btcclient.bat listaccounts
{
  "": 139.99990000,
  "account2": 10.00000000
}
```

# BTC second part
Попробуем подключиться к демону и запросить статус блокчейна:
```
$ ./btctestnet.bat getblockchaininfo
{
  "chain": "test",
  "blocks": 1320856,
  "headers": 1320856,
  "bestblockhash": "00000000000003c9894024faf0c2d1e50fed38b4a88ddf0cdd5faaab6b5d4b60",
  "difficulty": 3310843.932078449,
  "mediantime": 1527880159,
  "verificationprogress": 0.9999996950720793,
  "initialblockdownload": false,
  "chainwork": "0000000000000000000000000000000000000000000000419acebb399eb82498",
  "size_on_disk": 13289039257,
  "pruned": false,
  "softforks": [
    {
      "id": "bip34",
      "version": 2,
      "reject": {
        "status": true
      }
    },
    {
      "id": "bip66",
      "version": 3,
      "reject": {
        "status": true
      }
    },
    {
      "id": "bip65",
      "version": 4,
      "reject": {
        "status": true
      }
    }
  ],
  "bip9_softforks": {
    "csv": {
      "status": "active",
      "startTime": 1456790400,
      "timeout": 1493596800,
      "since": 770112
    },
    "segwit": {
      "status": "active",
      "startTime": 1462060800,
      "timeout": 1493596800,
      "since": 834624
    }
  },
  "warnings": "Warning: unknown new rules activated (versionbit 28)"
}
```

Количество blocks должно быть равно максимальному номеру блока тут https://live.blockcypher.com/btc-testnet/
Если она меньше, то нужно дождаться завершения синхронизации.

### Запрашиваем тестовый BTC через faucet

Создаем адрес для получения BTC:
$ ./btctestnet.bat getnewaddress ""
2NCKJYpnwQjzK1hYMF8Kddmgq5wEBU3wDWL

Получаем адрес **&lt;testnet_address1&gt;**.
testnet_address1 = 2NCKJYpnwQjzK1hYMF8Kddmgq5wEBU3wDWL

Далее идем сюда https://testnet.manu.backend.hamburg/faucet и запрашиваем получение BTC в тестнете на этот адрес **&lt;testnet_address1&gt;**.


В случае успеха сревис выводит хеш транзакции.
f91fc0ca60e7f744c2febc28f26a2ca648e48b42142415cd97cc3233a01b09e3


Проверяем, что имеем входящую транзакцию:
```
$ ./btctestnet.bat listtransactions
[
  {
    "account": "",
    "address": "2NCKJYpnwQjzK1hYMF8Kddmgq5wEBU3wDWL",
    "category": "receive",
    "amount": 0.27500000,
    "label": "",
    "vout": 0,
    "confirmations": 0,
    "trusted": false,
    "txid": "f91fc0ca60e7f744c2febc28f26a2ca648e48b42142415cd97cc3233a01b09e3",
    "walletconflicts": [
    ],
    "time": 1527881254,
    "timereceived": 1527881254,
    "bip125-replaceable": "no"
  }
]
```
txid = f91fc0ca60e7f744c2febc28f26a2ca648e48b42142415cd97cc3233a01b09e3


Копируем **&lt;txid&gt;** из входящей транзакции для создания новой.


Создаем транзакцию перевода средств со своего адреса на другой свой с одновременным указанием произвольных данных в транзакции:
```
$ ./btctestnet.bat  createrawtransaction "[{\"txid\": \"f91fc0ca60e7f744c2febc28f26a2ca648e48b42142415cd97cc3233a01b09e3\",\"vout\":0}]" "{\"2NCKJYpnwQjzK1hYMF8Kddmgq5wEBU3wDWL\": 0.2735, \"data\":\"4a756c696127732074657374\"}"
0200000001e3091ba03332cc97cd152414428be448a62c6af228bcfec244f7e760cac01ff90000000000ffffffff02f053a1010000000017a914d12fdc71c91a7e27ddd3f34ff6849cc7bf5b9dfb8700000000000000000e6a0c4a756c69612773207465737400000000
```

Вместо deadbeef можно указать произвольные данные в hex-формате (до 80 байт, то есть до 140 символов в формате hex). Преобразовать текстовую строку в hex можно тут http://www.swingnote.com/tools/texttohex.php.

После создания транзакции подписываем ее `signrawtransaction` и отправляем через `sendrawtransaction`.
```
$ ./btctestnet.bat signrawtransaction 0200000001e3091ba03332cc97cd152414428be448a62c6af228bcfec244f7e760cac01ff90000000000ffffffff02f053a1010000000017a914d12fdc71c91a7e27ddd3f34ff6849cc7bf5b9dfb8700000000000000000e6a0c4a756c69612773207465737400000000
{
  "hex": "02000000000101e3091ba03332cc97cd152414428be448a62c6af228bcfec244f7e760cac01ff90000000017160014cd60fa9d2cc1e1b0f383ce4e426c96f61d3c00a1ffffffff02f053a1010000000017a914d12fdc71c91a7e27ddd3f34ff6849cc7bf5b9dfb8700000000000000000e6a0c4a756c6961277320746573740247304402205015ea716566bd2cc41dea612a72e08f90662db51f5b86498c371b3eebf98c3402206280fef4bc81ef4a443a7953e75e1b940086351aaca1c8becfa2470ffd581d980121020b18e40f7bf4f887369de98fd1108335aba0cd52c19d09f074262e8ef2743dce00000000",
  "complete": true
}
```

```
$ ./btctestnet.bat sendrawtransaction 02000000000101e3091ba03332cc97cd152414428be448a62c6af228bcfec244f7e760cac01ff90000000017160014cd60fa9d2cc1e1b0f383ce4e426c96f61d3c00a1ffffffff02f053a1010000000017a914d12fdc71c91a7e27ddd3f34ff6849cc7bf5b9dfb8700000000000000000e6a0c4a756c6961277320746573740247304402205015ea716566bd2cc41dea612a72e08f90662db51f5b86498c371b3eebf98c3402206280fef4bc81ef4a443a7953e75e1b940086351aaca1c8becfa2470ffd581d980121020b18e40f7bf4f887369de98fd1108335aba0cd52c19d09f074262e8ef2743dce00000000
6a30b475c242476e89730584db8efde0f8f870edd7ecc5fc983288da4d037fa9
```

В реультате отправки получаем хеш (txid) новой транзакции и идем смотреть ее в блокчейн-эксплорере тестнета биткойна https://www.blocktrail.com/tBTC
txid = 6a30b475c242476e89730584db8efde0f8f870edd7ecc5fc983288da4d037fa9

https://www.blocktrail.com/tBTC/tx/6a30b475c242476e89730584db8efde0f8f870edd7ecc5fc983288da4d037fa9#tx_messages

### Задание 2
2.1. Easy. Запишите свой текст в тестовый блокчейн биткойна с использованием техники, описанной выше.
6a0c4a756c696127732074657374
Julia's test


# lightning application 
Идея - чатбот. Например, который за небольшую плату, поможет найти подходящие рецепты из тех продуктов,что у тебя есть
