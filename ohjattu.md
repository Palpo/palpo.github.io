Ohjattu harjoitustyö
====================

Harjoitustyössä toteutetaan kuvahakupalvelu käyttäen [Google App Engine -alustaa](https://developers.google.com/appengine/) Python-ohjelmointikielellä.
Palveluun voi tallentaa kuvia avainsanoineen.
Kuvia voi hakea avainsanojen perusteella ja kuvaan liittyviä avainsanoja voi myös muokata.
Järjestelmä pitää kirjaa toisiinsa liittyvistä avainsanoista.
Lisäksi kuvavarastoon on mahdollista toteuttaa myös lisäominaisuuksia (ks. kohta *Kuvavaraston lisäominaisuudet*).

Varsinaisen harjoitustyön lisäksi tulee suorittaa vertaisarviontitehtävä, jossa kukin ryhmä arvioi jonkin toisen ryhmän palvelun.

Jos huomaat tässä tehtävänannossa virheitä, puutteita tai epäselvyyksiä, voit ilmoittaa niistä vaikkapa luomalla issuen [Palpon web-sivun GitHub-repositorioon](https://github.com/palpo/palpo.github.io).


# Aikataulu

<table>
  <tr>
    <td>2015-10-23</td>
    <td>Harjoitustyöryhmän muodostamisen takaraja</td>
  </tr>
  <tr>
    <td>2015-11-30</td>
    <td>Harjoitustyön palautuksen takaraja</td>
  </tr>
  <tr>
    <td>2015-12-14</td>
    <td>Vertaisarvioinnin palautuksen takaraja</td>
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
Jos olet vailla harjoitustyöparia, voit etsiä sellaista vaikkapa IrcNetin IRC-kanavalla `#palpo`.


## Google App Engine

Harjoitustyö tehdään hyödyntäen Google App Engine -alustaa. App Enginen käyttö on ilmaista vähäisesti resursseja käyttäville sovelluksille. Ilmaisversion pitäisi hyvin riittää harjoitustyön tarpeisiin, kunhan tarkkailee hieman, että ei esim. suorita mitään hirveän pitkiä ja raskaita tausta-ajoja.

App Engine –kehitysympäristöä ja muita käytännön asioita käsitellään ensimmäisessä viikkoharjoituksessa. Lopuissa viikkoharjoituksissa käsitellään erilaisia App Enginen palveluita.

<table>
  <tr>
    <td>Toteutuskielenä voi halutessaan omalla vastuullaan käyttää myös jotain muuta kieltä kuin Pythonia. Tässä tapauksessa kurssihenkilökunta ei kuitenkaan voi tarjota apua; meillä ei ole tietoa miten tai kuinka hyvin (jos ollenkaan) Google App Enginen palvelut toimivat muilla kielillä. Javalla voi kenties onnistua. App Enginen Experimental-vaiheen kielillä (Go ja PHP) tuskin (esim. MapReduce-tuen osalta).</td>
  </tr>
</table>


## Toteutettava järjestelmä

Järjestelmään toteutetaan kolme osaa:

* **Kuvavarasto** - järjestelmän keskeisin osa. Tarjoaa REST-rajapinnan kuvien ja niihin liittyvien avainsanojen käsittelemiseen.
* **Kuvahaku** - web-sivu, jonka kautta voi hakea ja poistaa kuvia ja muokata avainsanoja.
* **Kuvalisäin** - yksinkertaisehko Python-skripti joka lisää kuvia Kuvavarastoon.

![Kuvavarasto](https://raw.githubusercontent.com/Palpo/palpo.github.io/master/img/kuvavarasto.png)

Harjoitustyötä varten tarvitaan siis kaksi App Engine -sovellusta, joiden tunnisteista tässä dokumentissa käytetään merkintää `<kuvavarasto>` ja `<kuvahaku>`.

Ryhmän muodostuksen yhteydessä luodaan ryhmälle GitHub-repositorio, joka sisältää pohjan harjoitustyön tekemiselle.
Pohja sisältää joitain osia valmiiksi toteutettuna.
Kaikkia valmiina annettuja tiedostoja saa vapaasti muokata.


## Kuvavarasto

Kuvavarasto tarjoaa REST-rajapinnan, jonka kautta voi lisätä ja etsiä kuvia sekä muokata kuviin liittyviä avainsanoja. Tämä rajapinta on ainoa tapa, jolla muut järjestelmän osat (Kuvahaku ja Kuvalisäin) kommunikoivat Kuvavaraston kanssa. Rajapinnan tarkempi määrittely jää harjoitustyön tekijöiden tehtäväksi.

**Rajapinta on dokumentoitava.** Rajapinnan dokumentaatio on nähtävillä juuriosoitteessa `<kuvavarasto>.appspot.com/` ja itse rajapinta vaikkapa osoitteessa `<kuvavarasto>.appspot.com/api` tai miten se dokumentaatiossa määritellään.

Tarkoituksena on harjoitella paitsi palveluiden suunnittelua ja toteutusta, myös (App Enginen) pilvipalveluiden käyttöä. Tästä syystä palvelun toteutukselle annetaan seuraavassa joitain vaatimuksia.


### Kuvien tallennus

Kuvien tallennus Kuvavarastoon tapahtuu seuraavasti:

* Asiakas lähettää Kuvavaraston rajapintaan pyynnön, jossa annetaan kuvan URL-osoite ja muut tarvittavat tiedot.

* Koska kuvien tallennustoimet ovat aikaavieviä (ainakin leikitään niin), **on tallennus tehtävä tausta-ajona käyttäen [Task Queue](https://developers.google.com/appengine/docs/python/taskqueue/) -palvelua**. Asiakkaan pyyntöön siis vastataan jotain asianmukaista ja aloitetaan tausta-ajo, joka tekee puolestaan seuraavaa:
    1. hakee kuvan annetusta URL-osoitteesta
    2. pienentää kuvan max. 128×128 pikselin kokoiseksi [Image](https://developers.google.com/appengine/docs/python/images/)-palvelun avulla
    3. tallentaa pienennetyn kuvan [Cloud Storage](https://developers.google.com/storage/docs/concepts-techniques) -palveluun haluamallaan tavalla (esimerkiksi käyttäen [Google Cloud Storage Clientiä](https://developers.google.com/appengine/docs/python/googlecloudstorageclient/)).
    4. tallentaa kuvan metatiedot [DataStore -palveluun käyttäen NDB-kirjastoa](https://developers.google.com/appengine/docs/python/ndb/)


### Toisiinsa liittyvät avainsanat

Käyttäjän kuvahakuja auttaakseen Kuvavarasto pitää tallessaan myös tietoa toisiinsa liittyvistä avainsanoista. Toisiinsa liittyvät avainsanat lasketaan sen perusteella, kuinka usein ne ovat saman kuvan yhteydessä. Esimerkiksi, jos järjestelmään on tallennettu 7 sellaista kuvaa, joiden avainsanoissa esiintyy sekä "kissa" että "mirri", niin tällöin sana "kissa" liittyy sanaan "mirri" arvolla 7, ja toisinpäin.

**Toisiinsa liittyvät avainsanat lasketaan [MapReduce](https://developers.google.com/appengine/docs/python/dataprocessing/)-ympäristössä.**
**Laskeminen suoritetaan silloin tällöin tausta-ajona**.
Avainsanojen ei siis tarvitse olla täysin ajan tasalla, mutta tieto toisiinsa liittyvistä avainsanoista on päivitettävä silloin tällöin vastaamaan Kuvavaraston uutta tilaa.
Nämäkin tiedot tallennetaan [DataStore -palveluun käyttäen NDB-kirjastoa](https://developers.google.com/appengine/docs/python/ndb/).


## Kuvahaku

Kuvahaku on osoitteessa `<kuvahaku>.appspot.com` oleva web-sivu, jolla voi etsiä Kuvavarastoon tallennettuja kuvia tietyn hakusanan perusteella.
Hakukenttään syötetään haluttu sana, jolloin käyttäjälle näytetään kaikki hakusanaa vastaavat kuvat, kuitenkin enintään 20 kuvaa.

Hakutuloksissa esitetään alla olevassa kuvassa esitetyt tiedot:

![Kuvahaku](https://raw.githubusercontent.com/Palpo/palpo.github.io/master/img/kuvahaku.png)


## Kuvalisäin

Kuvalisäin on Python-skripti, joka kaivaa annetusta HTML-sivusta kuvat sekä niihin liittyvät avainsanat ja tallentaa nämä Kuvavarastoon. Kuvalisäimen tarkoitus on vain tarjota nopea tapa uusien kuvien lisäämiseksi Kuvavarastoon. Kuvalisäintä käytetään antamalla sille komentoriviparametrina HTML-sivun URL-osoite, esim.

    python kuvalisain.py http://www.cs.tut.fi/~palpo/materiaali/testisivu.html

Kuvalisäimen pitää toimia [Lintulassa](http://www.cs.tut.fi/lintula/) ylläolevanlaisella komennolla.


## Kuvavaraston lisäominaisuudet

Yllä mainitut Kuvavaraston, Kuvahaun ja Kuvalisäimen ominaisuudet ovat pakollisia; ne pitää olla jotakuinkin toteutettu, että harjoitustyö hyväksytään.
Lisäksi on mahdollista toteuttaa lisäominaisuuksia:

<table>
  <tr>
    <td>Lisäominaisuus</td>
  </tr>
  <tr>
    <td>Käytetään jotain sellaista App Enginen tarjoamaa palvelua, jota ei ole mainittu tässä työohjeessa. Käytön pitää olla ainakin etäisesti järkevää. Esimerkiksi Memcache-palvelun käyttö suorituskyvyn parantamiseen tai  Channel-palvelun käyttö web-käyttöliittymän päivittämiseen. Tai jotain muuta.</td>
  </tr>
  <tr>
    <td>Käytetään jotain App Enginen ulkopuolista palvelua. Käytön pitää olla ainakin etäisesti järkevää. Esimerkiksi mahdollisuus kuvien julkaisuun jossain ulkopuolisessa kuvapalvelussa.</td>
  </tr>
</table>


## Harjoitustyön palautus

Harjoitustyöryhmän luonnin yhteydessä GitHub-repositorioon luotiin *issue* otsikolla "Harjoitustyö".
**Palautus tapahtuu sulkemalla (Close) tämä issue 30.11 mennessä.**

Varmistakaa, että palauttaessanne: 

* **Kuvavarasto- ja Kuvahaku-palvelut ovat ajossa App Enginessä**
* Repositorion juuressa olevan README.md -tiedosto sisältää seuraavat tiedot:
    * Ryhmän jäsenten nimet ja opiskelijanumerot.
    * App Engine -sovellusten (Kuvavarasto ja Kuvahaku) tunnisteet ja URL-osoitteet.
    * Kuvaus toteutetuista lisäominaisuuksista.
* Toteutusta on dokumentoitu niin, että tarkastajalle selviää helposti miten eri jutut (esim. toisiinsa liittyvien avainsanojen laskeminen jne.) on toteutettu. Vaikkapa README.md -tiedostoon voi kuvata yleisiä toteutusasioita, koodia voi kommentoida jne.
* README.md-tiedostossa on kuvattu mahdollisesti toteutetut lisäominaisuudet


## Arvostelu

**Harjoitustyö arvostellaan asteikolla 0-3. Arvosanan 1 saa työ, jossa kaikki pakolliset ominaisuudet on jotakuinkin toteutettu, ja se vaaditaan kurssin suoritukseen.**
Korkeamman arvosanan voi saada toteuttamalla lisäominaisuuksia ja/tai jotkut osat työstä erityisen hyvin.
Arvostelussa tarkastellaan mm. seuraavia asioita:

* Toteutetut lisäominaisuudet
    * Ainakin yksi lisäominaisuus vaaditaan arvosanaan 3
* Palvelun toimivuus, vakaus ja vikasietoisuus
* Rajapinnan suunnittelu ja REST-periaatteiden noudattaminen
* Rajapinnan dokumentaation selkeys ja oikeellisuus
* Ohjelmakoodin rakenne
* Ohjelmakoodin selkeys ja kommentointii
* Onko työssä jotain muuta poikkeuksellisen hyvää


## Vertaisarvionti

Varsinaisen harjoitustyön lisäksi tehdään vertaisarviointi jonkin toisen ryhmän Kuvavarasto-palvelulle.
Tämäkin on **pakollinen** suorite.

Harjoitustyön palautustakarajan jälkeen kullekin ryhmälle arvotaan arvioitavaksi jokin toinen ryhmä.
Arviointia varten arvontakomitea luo ryhmän GitHub-repositorioon uuden *issuen *otsikolla "Vertaisarviointi".
Tästä issuesta ilmenee mitä palvelua vertaisarvioidaan.

Ryhmä saa tarkasteltavakseen arvioitavan ryhmän Kuvavaraston dokumentaation.
Lisäksi arvioijat voivat käyttää toisen ryhmän Kuvavaraston tarjoamaa rajapintaa.

Arvioinnissa vastataan ainakin seuraaviin kysymyksiin:

* Kuinka hyvin arvioitava rajapinta noudattaa REST-periaatteita sekä yleisiä palveluiden suunnitteluperiaatteita?
* Onko dokumentaatio riittävän kattava ja selkeä? Miten sitä voisi parantaa?
* Vastaako rajapinta dokumentaatiota?
* Toimiiko rajapinta järkevästi virheellisten syötteiden tapauksessa?

Sopiva pituus arviointidokumentille on sellainen, että ylläoleviin kysymyksiin on järkevästi vastattu.
Mitään varsinaista kattavaa testausta (as in [testauskurssi](http://www.cs.tut.fi/~testaus/s2015/)) ei arvioitavalle rajapinnalle tarvitse tehdä.

**Vertaisarvioinnin palautus tapahtuu sulkemalla "Vertaisarviointi"-niminen issue ma 14.12 mennessä**.
**Mainitkaa issue:n kommenteissa mistä vertaisarviointidokumentti löytyy.**
Voitte esimerkiksi lisätä sen repositorioonne.

**Vertaisarvionti on pakollinen osa harjoitustyötä ja arvostellaan asteikolla hyväksytty/hylätty.**

