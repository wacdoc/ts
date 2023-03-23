# Aka sevha ya wena yo rhumela poso ya SMTP

## xingheniso

SMTP yi nga xava vukorhokeri hi ku kongoma eka vaxavisi va le mapapa, ku fana na:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali papa email push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

U nga ha tlhela u aka sevha ya wena ya poso - ku rhumela loku nga pimiwangiki, ntsengo wa le hansi hi ku angarhela.

Laha hansi, hi kombisa goza hi goza ndlela yo aka sevha ya hina ya poso.

## Ku hlawuriwa ka sevha

Sevha ya SMTP leyi tiyimeleke yi lava IP ya mani na mani leyi nga na tiphurotho ta 25, 456, na 587 leti pfulekeke.

Mapapa ya mani na mani lama tirhisiwaka ngopfu ma pfale swikepe leswi hi ku tiyimisela, naswona swi nga ha koteka ku swi pfula hi ku humesa oda ya ntirho, kambe swi karhata swinene endzhaku ka hinkwaswo.

Ndzi ringanyeta ku xava eka host leyi nga na ti ports leti pfulekeke naswona yi seketelaka ku veka mavito ya domain ya reverse.

Laha, ndzi bumabumela [Contabo](https://contabo.com) .

Contabo i muphakeri wa vuhlayiselo loyi a tshamaka eMunich, Germany, loyi a simekiweke hi 2003 hi minxavo leyi phikizanaka swinene.

Loko u hlawula Euro tanihi mali yo xava, nxavo wu ta chipa (sevha leyi nga na 8GB ya memori na 4 wa ti-CPU yi durha kwalomu ka 529 wa ti-yuan hi lembe, naswona mali yo sungula yo nghenisa i ya mahala ku ringana lembe rin’we).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Loko u endla oda, remark `prefer AMD` , naswona sevha leyi nga na AMD CPU yi ta va na matirhelo yo antswa.

Eka leswi landzelaka, ndzi ta teka VPS ya Contabo tanihi xikombiso ku kombisa ndlela yo aka sevha ya wena ya poso.

## Ku lulamisiwa ka sisiteme ya Ubuntu

Endlelo ro tirha laha i Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Loko sevha eka ssh yi kombisa `Welcome to TinyCore 13!` (hilaha swi kombisiweke hakona eka xifaniso lexi nga laha hansi), swi vula leswaku sisiteme a yi si nghenisiwa. Hi kombela u tsema ssh u rindza timinete ti nga ri tingani leswaku u tlhela u nghena.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Loko `Welcome to Ubuntu 22.04.1 LTS` yi humelela, ku sunguriwa ku herile, naswona u nga ya emahlweni na magoza lama landzelaka.

### [Swi hlawula] Sungula ndhawu ya nhluvukiso

Goza leri i ra ku tihlawulela.

Ku olovisa, ndzi veke ku nghenisiwa na ku lulamisiwa ka sisiteme ya software ya ubuntu eka [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Tirhisa xileriso lexi landzelaka ku nghenisa hi ku tikhoma kan’we.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Vatirhisi va Xichayina, hi kombela mi tirhisa xileriso lexi landzelaka ematshan’wini ya sweswo, naswona ririmi, ndhawu ya nkarhi, na swin’wana swi ta vekiwa hi ku tisungulela.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo yi endla leswaku IPV6 yi tirha

Endla leswaku IPV6 yi tirha leswaku SMTP yi ta tlhela yi rhumela ti-imeyili leti nga na tiadirese ta IPV6.

hlela `/etc/sysctl.conf`

Cinca kumbe u engetela mitila leyi landzelaka

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Landzelela hi [dyondzo ya contabo: Ku engetela vuhlanganisi bya IPv6 eka sevha ya wena](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Hlela `/etc/netplan/01-netcfg.yaml` , engetela milayeni yi nga ri yingani tanihilaha swi kombisiweke hakona eka xifaniso lexi nga laha hansi (Fayili ya vukorhokeri bya xiviri bya Contabo VPS se yi na milayeni leyi, yi susa ntsena mavonelo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Kutani `netplan apply` ku endla leswaku vukorhokeri lebyi cinciweke byi tirha.

Endzhaku ka loko ku lulamisiwa ku humelerile, u nga tirhisa `curl 6.ipw.cn` ku languta adirese ya ipv6 ya netiweke ya wena ya le handle.

## Clone vuhlayiselo bya vuhlanganisi ops

```
git clone https://github.com/wactax/ops.soft.git
```

## Endla xitifikheti xa mahala xa SSL xa vito ra wena ra domain

Ku rhumela poso swi lava xitifikheti xa SSL xo fihla na ku sayina.

Hi tirhisa [acme.sh](https://github.com/acmesh-official/acme.sh) ku tumbuluxa switifikheti.

acme.sh i xitirhisiwa xo sayina xitifikheti xa xihlovo lexi pfulekeke xa xiothomethi, .

Nghenisa vuhlayiselo bya vuhlanganisi ops.soft, tirhisa `./ssl.sh` , naswona folda ya `conf` yi ta endliwa eka **xikombo xa le henhla** .

Kuma muphakeri wa wena wa DNS ku suka eka [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , hlela `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Kutani tirhisa `./ssl.sh 123.com` ku tumbuluxa switifikheti swa `123.com` na `*.123.com` swa vito ra wena ra domain.

Ku tsutsuma ko sungula ku ta nghenisa hi ku tisungulela [acme.sh](https://github.com/acmesh-official/acme.sh) naswona ku engetela ntirho lowu hleriweke wa ku pfuxetiwa ka otomatiki. U nga vona `crontab -l` , ku na layini yo fana na leyi landzelaka.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Ndlela ya xitifikheti lexi endliweke i nchumu wo fana na `/mnt/www/.acme.sh/123.com_ecc。`

Ku pfuxetiwa ka xitifikheti ku ta vitana `conf/reload/123.com.sh` script, hlela script leyi, u nga engetela swileriso swo fana na `nginx -s reload` ku pfuxeta cache ya xitifikheti ya switirhisiwa leswi fambelanaka.

## Aka sevha ya SMTP hi chasquid

[chasquid](https://github.com/albertito/chasquid) i sevha ya SMTP ya xihlovo lexi pfulekeke leyi tsariweke hi ririmi ra Go.

Tanihi xisirhelelo xa minongonoko ya khale ya sevha ya poso yo fana na Postfix na Sendmail, chasquid yi olovile naswona ya olova ku yi tirhisa, naswona yi tlhela yi olova eka nhluvukiso wa vumbirhi.

Run `./chasquid/init.sh 123.com` yi ta nghenisiwa hi ku tisungulela hi ku tikhoma kan’we (siva 123.com hi vito ra wena ra domain ro rhumela).

## Hlela DKIM ya Sayina ya Imeyili

DKIM yi tirhisiwa ku rhumela masayini ya imeyili ku sivela mapapila ku tekiwa tanihi spam.

Endzhaku ka loko xileriso xi tirhile hi ndlela leyi humelelaka, u ta komberiwa ku veka rhekhodo ya DKIM (hilaha swi kombisiweke hakona laha hansi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Ntsena engetela rhekhodo ya TXT eka DNS ya wena (hilaha swi kombisiweke hakona laha hansi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Languta xiyimo xa vukorhokeri & tilog

 `systemctl status chasquid` Languta xiyimo xa vukorhokeri.

Xiyimo xa matirhelo ya ntolovelo xi tani hi leswi kombisiweke eka xifaniso lexi nga laha hansi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` kumbe `journalctl -xeu chasquid` yi nga languta log ya swihoxo.

## Ku tlherisela endzhaku ku lulamisiwa ka vito ra domain

Vito ra domain ro tlhelela endzhaku i ku pfumelela adirese ya IP ku lulamisiwa eka vito ra domain leri fambelanaka.

Ku veka vito ra domain ro tlhelela endzhaku swi nga sivela ti-imeyili ku tiviwa tanihi spam.

Loko poso yi amukeriwile, sevha leyi amukelaka yi ta endla nxopaxopo wa vito ra domain yo tlhelela endzhaku eka adirese ya IP ya sevha leyi rhumelaka ku tiyisisa loko sevha leyi rhumelaka yi ri na vito ra domain yo tlhelela endzhaku leri tirhaka.

Loko sevha leyi rhumelaka yi nga ri na vito ra domain yo tlhelela endzhaku kumbe loko vito ra domain ro tlhelela endzhaku ri nga fambisani na adirese ya IP ya sevha leyi rhumelaka, sevha leyi amukelaka yi nga ha lemuka imeyili tanihi spam kumbe yi yi ala.

Endzela [https://my.contabo.com/rdns](https://my.contabo.com/rdns) ivi u lulamisa tanihilaha swi kombisiweke hakona laha hansi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Endzhaku ko veka vito ra domain ra le ndzhaku, tsundzuka ku lulamisa xiboho xa le mahlweni xa vito ra domain ipv4 na ipv6 eka sevha.

## Hlela vito ra host ya chasquid.conf

Cinca `conf/chasquid/chasquid.conf` eka nkoka wa vito ra domain ra le ndzhaku.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Kutani tirhisa `systemctl restart chasquid` ku sungula vukorhokeri nakambe.

## Backup conf ku ya eka vuhlayiselo bya git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Xikombiso, ndzi backup folda ya conf eka process ya mina ya github hi ndlela leyi landzelaka

Ku sungula ku endla ndhawu yo hlayisela swilo ya le xihundleni

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Nghena eka conf directory u rhumela eka warehouse

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Engetelani murhumeri

tsutsuma

```
chasquid-util user-add i@wac.tax
```

A nga engetela murhumeri

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Tiyisisa leswaku phaswedi yi vekiwile kahle

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Endzhaku ko engetela mutirhisi, `chasquid/domains/wac.tax/users` yi ta pfuxetiwa, tsundzuka ku yi rhumela eka ndhawu yo hlayisela swilo.

## DNS yi engetela rhekhodo ya SPF

SPF ( Sender Policy Framework ) i thekinoloji yo tiyisisa imeyili leyi tirhisiwaka ku sivela vuxisi bya imeyili.

Yi tiyisisa vutivi bya murhumeri wa poso hi ku kambela leswaku adirese ya IP ya murhumeri yi fambelana na tirhekhodo ta DNS ta vito ra domain leri yi vulaka leswaku i rona, ku sivela vaxisi ku rhumela ti-imeyili ta vuxisi.

Ku engetela tirhekhodo ta SPF swi nga sivela ti-imeyili ku tiviwa tanihi spam hi laha swi kotekaka ha kona.

Loko sevha ya wena ya mavito ya domain yi nga seketeli muxaka wa SPF, engetela ntsena rhekhodo ya muxaka wa TXT.

Xikombiso, SPF ya `wac.tax` yi le ka xiyimo lexi landzelaka

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF ya `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Xiya leswaku ndzi na `include:_spf.google.com` laha, leswi swi vangiwa hikuva ndzi ta lulamisa `i@wac.tax` tanihi adirese yo rhumela eka bokisi ra poso ra Google endzhaku.

## Ku lulamisiwa ka DNS DMARC

DMARC i xifunengeto xa (Ku Tiyisisiwa ka Mahungu lama simekiweke eka Domayini, Ku Vika & Ku Fambisana).

Yi tirhisiwa ku khoma ti SPF bounces (kumbexana swi vangiwa hi swihoxo swa configuration, kumbe un’wana u tiendla onge hi wena ku rhumela spam).

Ku engetela rhekhodo ya TXT `_dmarc` , .

Leswi nga endzeni ka yona hi leswi landzelaka

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Nhlamuselo ya parameter yin’wana na yin’wana yi le ka xiyimo lexi landzelaka

### p (Pholisi) .

Yi kombisa ndlela yo khoma ti-imeyili leti hlulekaka ku tiyisisiwa ka SPF (Sender Policy Framework) kumbe DKIM (DomainKeys Identified Mail). Parameter ya p yi nga vekiwa eka yin’wana ya mimpimo yinharhu:

* ku hava: Ku hava goza leri tekiwaka, i mbuyelo wa ku tiyisisa ntsena lowu tlheriseriwaka eka murhumeri hi ku tirhisa endlelo ro vika imeyili.
* Ku hambanisiwa: Veka poso leyi nga hundzangiki eka ku tiyisisiwa eka folda ya spam, kambe yi nga ta ala poso hi ku kongoma.
* reject: Ala hi ku kongoma ti-imeyili leti tsandzekaka ku tiyisisiwa.

### fo (Swihlawulekisi swa ku tsandzeka) .

Ku hlamusela nhlayo ya mahungu lama vuyiseriweke hi endlelo ro vika. Yi nga vekiwa eka yin’wana ya mimpimo leyi landzelaka:

* 0: Xiviko xa mbuyelo wa ku tiyisisiwa eka marungula hinkwawo
* 1: Vika ntsena marungula lama tsandzekaka ku tiyisisiwa
* d: Ku vika ntsena ku tsandzeka ka ku tiyisisiwa ka mavito ya domain
* s: vika ntsena ku tsandzeka ka ku tiyisisiwa ka SPF
* l: Vika ntsena ku tsandzeka ka ku tiyisisiwa ka DKIM

### rua & ruf

* rua (Ku vika URI ya swiviko leswi hlengeletiweke): Adirese ya imeyili yo amukela swiviko leswi hlengeletiweke
* ruf (Ku vika URI ya swiviko swa Forensiki): adirese ya imeyili ku amukela swiviko swa vuxokoxoko

## Engetelani tirhekhodo ta MX ku hundzisela ti-imeyili eka Google Mail

Hikuva a ndzi nga kumi bokisi ra poso ra mahala ra nhlangano leri seketelaka tiadirese ta misava hinkwayo (Catch-All, ndzi nga amukela ti-imeyili tihi na tihi leti rhumeriweke eka vito leri ra domain, handle ka swipimelo eka swirhangi), ndzi tirhise chasquid ku hundzisela ti-imeyili hinkwato eka bokisi ra mina ra poso ra Gmail.

**Loko u ri na bokisi ra wena ra poso ra bindzu leri hakeriwaka, hi kombela u nga cinci MX naswona u tlula goza leri.**

Hlela `conf/chasquid/domains/wac.tax/aliases` , veka bokisi ra poso ro hundzisela emahlweni

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` yi kombisa ti-imeyili hinkwato, `i` i xirhangi xa adirese ya imeyili ya mutirhisi loyi a rhumelaka lexi endliweke laha henhla. Ku hundzisela poso, mutirhisi un’wana na un’wana u fanele ku engetela layini.

Kutani engetela rhekhodo ya MX (ndzi kombetela hi ku kongoma eka adirese ya vito ra domain ya le ndzhaku laha, tanihilaha swi kombisiweke hakona eka layini yo sungula eka xifaniso lexi nga laha hansi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Endzhaku ka loko ku lulamisiwa ku herile, u nga tirhisa tiadirese tin’wana ta ti-imeyili ku rhumela ti-imeyili eka `i@wac.tax` na `any123@wac.tax` ku vona loko u nga amukela ti-imeyili eka Gmail.

Loko swi nga ri tano, languta log ya chasquid ( `grep chasquid /var/log/syslog` ).

## Rhumela email eka i@wac.tax hi Google Mail

Endzhaku ka loko Google Mail yi amukerile poso, hi ntumbuluko ndzi tshembile ku hlamula hi `i@wac.tax` ematshan’wini ya i.wac.tax@gmail.com.

Endzela [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) kutani u tikhoma "Engetela adirese yin'wana ya email".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Kutani, nghenisa khodi ya ku tiyisisa leyi amukeriweke hi imeyili leyi hundziseriweke eka yona.

Eku heteleleni, yi nga vekiwa tanihi adirese ya murhumeri ya ntolovelo (swin’we na nhlawulo wo hlamula hi adirese leyi fanaka).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Hi ndlela leyi, hi hetile ku simekiwa ka sevha ya poso ya SMTP naswona hi nkarhi lowu fanaka hi tirhisa Google Mail ku rhumela na ku amukela ti-imeyili.

## Rhumela imeyili ya xikambelo ku kambela loko ku lulamisiwa ku humelerile

Nghena eka `ops/chasquid`

Run `direnv allow` ku nghenisa swilo leswi titshegeke (direnv yi nghenisiwile eka endlelo ro sungula ra xilotlelo xin’we leri hundzeke naswona ku engeteriwile xihuku eka xikhegelo)

kutani u tsutsuma

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Nhlamuselo ya tipharamitha yi le ka xiyimo lexi landzelaka

* mutirhisi: Vito ra mutirhisi ra SMTP
* ku hundza: Phasiwedi ya SMTP
* ku: muamukeri

U nga rhumela email ya xikambelo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Swi ringanyetiwa ku tirhisa Gmail ku amukela ti-imeyili ta xikambelo ku kambela loko swivumbeko swi humelerile.

### Ku fihla ka ntolovelo ka TLS

Hilaha swi kombisiweke hakona eka xifaniso lexi nga laha hansi, ku na xilotlelo lexi lexitsongo, leswi vulaka leswaku xitifikheti xa SSL xi pfuriwile hi ndlela leyi humelelaka.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Kutani u hlanganisa "Show Original Email".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Hilaha swi kombisiweke hakona eka xifaniso lexi nga laha hansi, tluka ra poso yo sungula ya Gmail ri kombisa DKIM, leswi vulaka leswaku vukorhokeri bya DKIM byi humelerile.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Languta Received eka nhlokomhaka ya imeyili yo sungula, naswona u nga vona leswaku adirese ya murhumeri i IPV6, leswi vulaka leswaku IPV6 na yona yi lulamisiwile hi ndlela leyi humelelaka.
