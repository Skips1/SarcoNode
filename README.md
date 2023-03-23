<h1 align="center"> Sarcophagus </h1>

![image](https://user-images.githubusercontent.com/101149671/213923450-405963b2-8358-4a46-ae5f-3f34eda56d52.png)

<h1 align="center"> Bu rehberde Sarcophagus'un node'unu kuracağız. Belki bir çoğunuzun alışık olmadığı bir şekilde olacak bu node, okunması gereken notlarım ile başlayalım:</h1>

* Acele etmemenizi, okuyarak ve anlayarak yapmanızı şiddetsiz bir şekilde tavsiye ediyorum.
* Bir blockchain değil, Arweave üzerinde geliştirilen bir proje.
* Sarcophagus aynı zamanda bir DAO ile yönetiliyor, ödüllü testnet için oylama başlatıldı. ve DAO tarafından kabul edildi.
* İlginizi çeker mi bilmiyorum ama, bir diğer güzel haber bu linkte: [Link 1](https://coinmarketcap.com/currencies/sarcophagus/) - [Link 2](https://www.coingecko.com/en/coins/sarcophagus#markets)
* Token alırken [discorddan](https://discord.gg/Eyd5HYzj) almalıyız (rehberin devamında tokenin kullanım alanını göstereceğim)
* Sohbet için [telegram](https://t.me/SarcophagusTurkish) kanalı
* Aklıma geldikçe buraya daha fazla not eklerim.
* Node sonrası bu [listede](https://sarcopahgus.notion.site/Archaeologist-Testnet-Participant-Roster-e19dedd7d00346b2a20dce3aa46ab68b) olmalısınız.

![image](https://user-images.githubusercontent.com/101149671/213924896-1f09ce56-1057-4cf0-b030-6cda23835e8e.png)

## Donanım ve Gereksinimler:
```
10 GB SSD
1 GB RAM
```

* Goerli veya Sepolia'dan test ETH.
* Bir RPC URL (Nasıl alacağınızı bilmiyorsanız ben size vereceğim)
* Bir A kaydı olan domain.

### Domain Hakkında Notlar:

* Biliyorum, herkesin bir domain'i yok, bunu nasıl çözeceğinizi bilmiyorum.
* Ben kendi domainimi severime bağladım, sizde öyle yapmalısınız.

![image](https://user-images.githubusercontent.com/101149671/213924185-9e320b9d-a2ea-46b9-835b-ba70f6d5aa69.png)

* Domaini A kaydı yaptıktan sonra şu şekilde gözükecektir, örnektir: `ns1.ziesha.network`

* Domaininiz varsa size rehber olacak kaynaklar: [Godaddy](https://tr.godaddy.com/help/a-kaydi-ekleme-19238) - [Namecheap](https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain/) - [Name.com](https://www.name.com/support/articles/115004893508-adding-an-a-record)

* Şu an müsaitlik durumum yok, yoksa nasıl domain alınır nasıl bağlanılır tek tek anlatırdım, ama bana gerek yok size kaynak bıraktım ve youtube kaynak dolu.

* Biraz bakındım, ücretsiz domainlerde alabilirsiniz (işe yaramayan domainler genellikle ücretsiz oluyor, bu da işiniz görür), örneğin:

![image](https://user-images.githubusercontent.com/101149671/213924481-f7782c3f-44af-482c-83cc-2abd0fbdefc9.png)

> Test etmedim ama ücretsiz domain veren siteler: [Link 1](https://www.hostinger.web.tr/ucretsiz-domain) - [Link 2](https://tr.wix.com/domain/names) 

> HER NE KADAR DOMAİNİ ÜCRETSİZ BULSAKTA HOSTİNG ÜCRETLİ (2$-40$). Bunu sohbet grubunda tartışalım.

## Bunları okuduysanız ve çözdüyseniz node'umuzu kuralım:
```
sudo su
```
```
sudo apt update 
```
```
sudo apt upgrade
```
```
sudo apt install git
```
```
sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```

## Repoyu klonlayalım ve gerekli işlemlere başlayalım:
```
git clone https://github.com/sarcophagus-org/quickstart-archaeologist
```
```
cd quickstart-archaeologist
```
## Bu komutu çalıştırdıktan sonra bir 12 kelime oluşturalım:

> Altta ki komut offline seed generate isterseniz [buradan](https://iancoleman.io/bip39/) ethereum seçipte bir seed oluşturabilirsiniz.

> Konu açılmışken, yukarıda kendinize özel cüzdanlar oluşturabilirsiniz, güven ve risk konusu size kalmış :)

```
cp .env.example .env
```
```
COMPOSE_PROFILES=seed docker compose run seed-gen
```
```
touch peer-id.json
```

> Yukarıdaki `seed-gen` komutunu girdikten sonra 12 kelimenizi not edip saklayın.

> Daha sonra altta ki komutu girip nano ile `.env`'in içine girelim.

```
nano .env
```

## Yukarıda `.env`'in içine girdiğinizde yapmanız gerekenler:

> `ETH_PRIVATE_KEY` için kısmı tıpkı [taiko](https://github.com/ruesandora/taiko-node#yukar%C4%B1daki-komutlar%C4%B1-girince-a%C3%A7%C4%B1lacak-ekran-g%C3%B6rselde-ki-gibi) 'da yaptığımız gibi metamask'ın private key'ini alıyoruz. (özel anahtar = private key)

* Private keyi aldıktan sonra `ETH_PRIVATE_KEY=` 'in yanına bunu giriyoruz

> `ENCRYPTION_MNEMONIC=` kısmı, yukarıda aldığımız seed/12 kelimeyi giriyoruz.

> `DOMAIN=` kısmı yukarıda anlattığım gibi `ns1.ziesha.network` gibi olacak ve ekleyeceksiniz. (bunu boşuna denemeyin, olmayacak)

> `PROVIDER_URL=` için bir RPC URL'ye ihtiyacınız var, ben aşağıya sıralıyorum (not ben ANKR RPC kullandım):

> https://rpc.ankr.com/eth_goerli -- https://rpc.ankr.com/eth_sepolia -- https://sepolia.infura.io/v3/3f110b00aeb24807b3ac5a9a4536079c --https://goerli.infura.io/v3/3f110b00aeb24807b3ac5a9a4536079c

* Bunlar dışında kendi node'unuz varsa veya Alchemy'den bağlanabilirsiniz.

> Hepsini doldurduktan sonra `CTRL + X + Y + ENTER` yapıyoruz.

## Şimdi node'umuzu çalıştıralım:

> Çalıştırmadan önce kontrol etmemiz gerekenler: test ETH ve SARCO token lazım cüzdanımıza.

> Sepolia veya Goerli ETH faucetten bulursunuz, SARCO için discord #nodes-and-technical-discussion kanalından token istemelisiniz. (Faucet yakında gelecek)

```
COMPOSE_PROFILES=register docker compose run register
```

> Yukarı da ki  register komutunu girdikten sonra benim yaptıklarım (test ederek yaptım)

* İlk soru: `Y`` - İkinci soru: `1-5 arası` - Üçüncü soru: `190-200 arası` - Dördüncü soru: `1 yea`r - Son sour: `yes`
* 100 veya 150 de yapabilrisiniz, keyfinize bağlı.

> Başarılı olduğunda görselde ki gibi bir çıktı olacak:

![image](https://user-images.githubusercontent.com/101149671/213926991-b9a24d57-5247-4416-b3fe-cc79eca332a5.png)

## Compose up yaptık mı bu iş tamam:
```
COMPOSE_PROFILES=service docker compose up -d
```

## Ya hocam benim node çalışıyor mu?

> ls komutu ile container id'imizi alalım:

```
docker container ls
```

> container id kısmına id'inizi girip aratın
```
docker logs container id --follow
```

> Doğru çıktı görseldedir:

![image](https://user-images.githubusercontent.com/101149671/213927255-f8d40794-db0a-47c3-9eab-56f7b53e2099.png)

## Node'umuzu kaydedlim:

> [Buraya](https://dev-sarcophagus.netlify.app/embalm) giriyoruz

> Node kurduğumuz cüzdanı bağlıyoruz bir profil oluşturuyoruz. İsim kısmına bence `discord` adınızı yazın.

> 2. kısımda bir dosya yüklüyoruz

> 3. kısma Fund Arweave Bundlr yapıyoruz. (token mıntlemek gibi düşünün) (sarcophagus'u bu ekosistemin L2 gibi düşünebilirsiniz)

> 4. kısma [buradan](https://dev-sarcophagus.netlify.app/recipients) public key oluşturup giriyoruz.

> 5. kısımda Archaeologists seçiyoruz, beni seçebilirisiniz: `0x86826aB17c2AF2FBE8d74577E91ec2BB52b3A1Eb`

> 6. kısıma 1 yazıp nextliyoruz

## Node'a güncelleme gelirse bu komutlar:
```
COMPOSE_PROFILES=service docker compose stop
COMPOSE_PROFILES=service docker compose pull
COMPOSE_PROFILES=service docker compose up -d
```

## Burdan sonrasını okumanız gerekmiyor, testnet ile alakalı değil:

> Sürekli hocam Ziesha yoğunluk arttı içerik üretmeyi bıraktın diyenler üzüyor beni

> Testnet oldukça paylaşıyorum, detaylı yazmaya çalışıyorum.

> Bunu cevaplamak zorunda değilim biliyorum, ama benimde çalışmam, işimi yapmam, haliyle para kazanmam lazım.

> Hem bu 2 yıllık süreçte tamamen full artı full ücretsiz ürettim, toplulukta artık benden daha bilgili olan insanlar bile var. Artık kendi kendinize bir şeyler kazanabilirsiniz buradan. Ben çok kazandım, paradan bahsetmiyorum, sizde üretin daha fazla şey. Unutulmak istiyorum artık.

> Şu konuda haklı olabilirsiniz, her ne kadar kendi başınıza bu işleri yapabilecek olsanız bile projeyi bulma konusunda belki eksiklik olabilir. Onda da elimden geldiğince katkıda bulunuyorum size.

> Ve hala eski aktifliğimi isteyen arkadaşlar, üzgünüm. herkes bir gün gider, her güzel şey bir gün biter.

> Son olarak, son 2 günde 2 node paylaştım, bunları yaparken ülkemi ve görmek istediğim yerleri gezerken yapıyorum, yani proje oldukça ben gördükçe paylaşıyorum merak etmeyin.

> Bu gezimin devamında en az 5 şehir daha olacak, belki oralarda görüşürüz sizlerle. Telegram duyuru kanalımdan duyururum.

> Belki saçmaladım yukarıda, söylemek istedim, kolay gelsin.

* Bu arada bunu da redditte buldum, public mi bilmiyorum: [link](https://56ssnyla75tw6rvja6u74w7lf4ow26dl2lzouha4rmxiesz5jk2q.arweave.net/76Um4WD_Z29GqQep_lvrLx1teGvS8uocHIsugks9SrU)
