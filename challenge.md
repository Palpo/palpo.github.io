Open Finland Challenge -harjoitustyö
====================================

Vaihtoehtoinen tapa suorittaa palvelupohjaisten järjestelmäin harjoitustyö on osallistua
[Open Tampere Challenge](http://www.opentamperechallenge.fi/) tai
[Open Finland Challenge](http://openfinlandchallenge.fi/) -kilpailuun.
Kilpailuun osallistutaan suunnittelemalla ja toteuttamalla suomalaisia avoimia datalähteitä hyödyntävä sovellus.
Kilpailuissa on jaossa on myös [rahapalkintoja](http://openfinlandchallenge.fi/sarjat-ja-palkinnot/) [(2)](http://www.opentamperechallenge.fi/opentamperechallenge/#palkinnot).

Jos huomaat tässä tehtävänannossa virheitä, puutteita tai epäselvyyksiä, voit ilmoittaa niistä vaikkapa luomalla issuen [Palpon web-sivun GitHub-repositorioon](https://github.com/palpo/palpo.github.io).


## Aikataulu

Aikataulu on tämän harjoitustyövaihtoehdon osalta melko tiukka, johtuen Open Finland Challengen määräajasta.

<table>
  <tr>
    <td>2015-10-05</td>
    <td>Suunnitelma</td>
  </tr>
  <tr>
    <td>2015-11-09</td>
    <td>Open Finland Challenge -töiden jättöpäivä sekä harjoitustyön palautus</td>
  </tr>
  <tr>
    <td>2015-11-30</td>
    <td>Vertaisarvioinnin takaraja</td>
  </tr>
</table>


## Harjoitustyöryhmän muodostaminen

Ensimmäinen haaste on harjoitustyöryhmän muodostaminen.
Se tapahtuu [Palpoilmo-palvelussa](https://palpoilmo.appspot.com/), joka tarjoaa REST-rajapinnan harjoitusryhmien luontiin.
[Rajapinta on dokumentoitu täällä](https://palpoilmo.appspot.com).

Harjoitustyö tehdään [GitHub](https://github.com/)-repositoriossa, joten harjoitustyön tekoon tarvitaan GitHub-tili.
Lisäksi tarvitaan Google-tili, jolla luodaan pari App Engine -sovellusta.
Myös [Lintula](http://www.cs.tut.fi/lintula/)-tunnus tarvittaneen.

Työ toteutetaan oletusarvoisesti parityönä. Yksinkin saa tehdä.
Jos olet vailla harjoitustyöparia, voit etsiä sellaista vaikkapa IRC-kanavalla `#palpo`.

Yli kahden hengen ryhmätkin ovat tässä harjoitustyössä mahdollisia, mutta tällöin toteutettavan sovelluksenkin on oltava laajempi.
**Yli kahden hengen ryhmien on suunnitelmassaan perusteltava tarve lisäjäsen(e|i)lle.**
Esim. mitä sellaisia lisäominaisuuksia sovelluksessa on, että sen toteuttaminen ei pienemmällä ryhmällä onnistu


## Säännöt

[Open Finland Challengen määrittelemät vähimmäisehdot](http://openfinlandchallenge.fi/saannot/) työlle ovat varsin vähäiset.
Tästä syystä **kurssin puolesta annetaan seuraavat ****lisäehdot**, jotka työn on Open Finland Challengen sääntöjen lisäksi täytettävä:

1. Sovelluksen täytyy hyödyntää vähintään kahta eri  julkisen rajapinnan (API) kautta tarjolla olevaa datalähdettä uudenlaisen ja yksittäisiä datalähdettä rikkaamman tiedon tuottamiseen. Osa kilpailussa tarjolla olevista datalähteistä jaetaan tiedostoina. Näitäkin on mahdollista hyödyntää, mutta niitä ei lasketa kahden datalähteen vaatimuksiin, ellette sitten toteuta ja käytä erillistä omaa API:a kyseisen datan jakeluun.
2. Sovelluksen täytyy tarjota REST-rajapinta tuottamaansa tietoon.
3. REST-rajapinta on dokumentoitava.
4. Suosittelemme palvelun pystyttämistä Googlen App Engine -ympäristöön. Jos kuitenkin haluatte käyttää jotakin muuta ympäristöä, valinta täytyy perustella projektisuunnitelmassa. Työn on joka tapauksessa oltava käytettävissä projektitöitä tarkastettaessa palautuksesta n. joulukuun alkupuolelle.

Työ toteutetaan oletusarvoisesti 1-2 hengen ryhmällä. 
Tätäkin suuremmat ryhmät ovat mahdollisia, mutta tällöin toteutettavan sovelluksenkin on oltava laajempi.
**Yli kahden hengen ryhmien on suunnitelmassaan perusteltava tarve lisäjäsen(e|i)lle.**
Esim. mitä sellaisia lisäominaisuuksia sovelluksessa on, että sen toteuttaminen ei pienemmällä ryhmällä onnistu.


## Suunnitelma

Ennen työn aloittamista on tehtävä suunnitelma, jossa kuvataan **lyhyesti** toteutettava sovellus.
Suunnitelmasta on ilmettävä sovelluksen perusidea, hyödynnettävät datalähteet, sovelluksen toteutuksessa käytettävät teknologiat sekä ryhmän nimi ja jäsenet.

Suunnitelmaa varten harjoitustyörepositorioon on luotu issue nimellä *Suunnitelma*.
Suunnitelma palautetaan liittämällä se tämän issuen kommentiksi/liitetiedostoksi/linkiksi tms. ja sulkemalla issue ma 4.10. mennessä.
Antakaa tämän issuen olla osoitettu (assigned) käyttäjälle *Palpo-robotti*, jotta kurssihenkilökunta saa sähköpostin sulkemisesta ja voi saman tien hyväksyä suunnitelman.


## Harjoitustyön palautus

Open Finland Challengen kilpailutöiden viimeinen jättöpäivä on 9. marraskuuta. Tämä on myös harjoitustyön palautuksen määräaika.

Sekä itse palvelun, palvelun REST-rajapinnan että REST-rajapinnan dokumentaation on oltava julkisesti saatavilla.
Palvelun rajapintoineen on oltava kenen tahansa käytettävissä.

Luokaa repositorioon tiedosto README.md joka sisältää ainakin seuraavat tiedot:
* Ryhmän jäsenten nimet
* URL jossa palvelu on ajossa
* URL jossa REST-rajapinta sekä sen dokumentaatio on saatavilla
* Mahdolliset muut palvelun käyttöön vaadittavat ohjeet / linkki ohjeisiin

Palautus tapahtuu sulkemalla harjoitustyörepositorion issue nimeltä *Harjoitustyö* ti 9.11 mennessä.


## Arvostelu

**Harjoitustyö arvostellaan asteikolla 0-3. Arvosanan 1 saa työ, jossa kaikki pakolliset ominaisuudet on jotakuinkin toteutettu, ja se vaaditaan kurssin suoritukseen.**
Korkeamman arvosanan voi saada toteuttamalla lisäominaisuuksia ja/tai jotkut osat työstä erityisen hyvin.
Arvostelussa tarkastellaan mm. seuraavia asioita:

* Palvelun hyödyllisyys, omaperäisyys ja kekseliäisyys
* Palvelun toimivuus, vakaus ja vikasietoisuus
* REST-rajapinnan suunnittelu ja REST-periaatteiden noudattaminen
* REST-rajapinnan dokumentaation selkeys ja oikeellisuus
* Ohjelmakoodin rakenne
* Ohjelmakoodin selkeys ja kommentointi
* Onko työssä jotain muuta poikkeuksellisen hyvää


## Vertaisarvionti

Varsinaisen harjoitustyön lisäksi tehdään vertaisarviointi jonkin toisen ryhmän harjoitustyölle ja erityisesti sen tarjoamalle rajapinnalle.
Tämäkin on **pakollinen** suorite.

Harjoitustyön palautustakarajan jälkeen kullekin ryhmälle arvotaan arvioitavaksi jokin toinen ryhmä.
Arviointia varten arvontakomitea luo ryhmän GitHub-repositorioon uuden *issuen* otsikolla "Vertaisarviointi".
Tästä issuesta ilmenee mitä palvelua vertaisarvioidaan.

Arvioinnissa vastataan ainakin seuraaviin kysymyksiin:

* Kuinka hyvin arvioitava rajapinta noudattaa REST-periaatteita sekä yleisiä palveluiden suunnitteluperiaatteita?
* Onko dokumentaatio riittävän kattava ja selkeä? Miten sitä voisi parantaa?
* Vastaako rajapinta dokumentaatiota?
* Toimiiko rajapinta järkevästi virheellisten syötteiden tapauksessa?
* Millä tavoin arvioitava rajapinta eroaa omasta rajapinnastanne? Onko jompi kumpi ratkaisu parempi?

Sopiva pituus arviointidokumentille on sellainen, että ylläoleviin kysymyksiin on järkevästi vastattu.
Mitään varsinaista kattavaa testausta (as in [testauskurssi](http://www.cs.tut.fi/~testaus/s2015/)) ei arvioitavalle rajapinnalle tarvitse tehdä.

**Vertaisarvioinnin palautus tapahtuu sulkemalla "Vertaisarviointi"-niminen issue ma 23.11 mennessä**.
**Mainitkaa issue:n kommenteissa mistä vertaisarviointidokumentti löytyy.**
Voitte esimerkiksi lisätä sen repositorioonne.

**Vertaisarvionti on pakollinen osa harjoitustyötä ja arvostellaan asteikolla hyväksytty/hylätty.**

