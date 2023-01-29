# Log

## Artikkeli & kommentit

Valitsin artikkeliksi otsikolla "GPT is all you need for the backend". 

Artikkeli käsitteli pääpiirteittäin seuraavia aiheita:

- Kuinka koodi ei ole ihanteellinen tapa koodata liiketoimintalogiikkaa. 
- Kuinka artikkelin kirjoittaja puhuu monikossa rakentaneensa kokonaisen Backend tietokonanna, joka toimii LLM:n avulla. Lisäksi kuinka se päättelee liiketoimintalogiikkaa API-kutsun nimen perusteella.

Artikkelissa kirjoittaja avaa mikä on tulevaisuus jota me kuvittelemme ja lainaa lopuksi Parkerin (etunimeä ei mainittu) sanoja. 
Artikkeli itessään oli melko lyhyt ja itselle sisältö vielä hieman tuntematonta, joten tiivistelmä oli osaltaan hieman hankala toteuttaa. 

Kommenttien perusteella asian toimivuudesta LLM:ään viitaten. 
"I keep hearing this assertion, that GPT can be wrong, therefore it’s an unworkable technology. But it’s a bad comparison. LLMs aren’t trying to be computationally correct like a calculator or something, the value is in their ability to semantically process a question. The other issue is assuming that the existing way of doing things is always correct."

Lähde: https://github.com/TheAppleTucker/backend-GPT

## Analysointia

Käytän ensimmäisen kohdan syslog haussa seuraavaa hakutapaa:

      $ cd var/log/
      $ sudo cat syslog
      
Tämän jälkeen sain pitkä liudan eri lokitietoja. Yritin näitä parhaani mukaan ymmärtää, mutta tekstirivien määrän ja sisällön ymmärtäminen oli hankalaa.
Käytännössä systemlog näyttää kaiken mahdollisen tapahtuman.

![Syslog](https://user-images.githubusercontent.com/100162043/215350280-aa289f8a-9448-4b43-a8af-5e6f4748efc0.jpg)


Seuraavana vuorossa oli auth.log. Tässä käytin seuraavaa komentoa.

        $ sudo tail -f /var/log/auth.log
        
Kyseisessä kuvassa näen tapahtumia, kuinka viimeisimmät istunnot on minulla alkaneet ja loppuneet. 

![authlog](https://user-images.githubusercontent.com/100162043/215350427-4b8dbb19-4b02-41bd-9f35-b3dcbacb3cfa.jpg)



Näissä apache2 kohdissa sitten ilmaantuikin ongelmia, johon en tässä ajassa löytänyt vastauksia. Yritin mennä ohjeiden antamalla tavalla lokikansioon, mutta terminaaliin tuli teksti no permission. Tähän kokeilin eri tapoja päästä kiinni apache2 hakemistoon, mutta turhaan. Alla kuvia yrityksistä, sekä terminaaliin ilmaantuneista vastauksista. 

![Apache status](https://user-images.githubusercontent.com/100162043/215350295-7b20fa76-b4de-4879-a174-0931a5069dd1.jpg)
![varlogapache2](https://user-images.githubusercontent.com/100162043/215350454-8fab9771-6fef-4e78-b2b9-00a19c14c6c0.jpg)


## Lokitapahtumat

Viimeisessä osiossa lähdin hakemaan onnistunutta ja epäonnistunutta lokitapahtumaan. Tässä esimerkissä lähdin vaihtamaan salasanaa. 

        $ passwd
        
![Oikea salasana](https://user-images.githubusercontent.com/100162043/215350381-0a28e5cc-c3db-4e6a-8227-588c0350b1de.jpg)


Ja koska kirjoitin myös kertaalleen salasanan väärin. Tämä näkyy heti komentorivillä alapuolella sekä kun hain auth.log tiedoista, löytyy sieltä seuraava ilmoitus:

![Väärin meni salasana](https://user-images.githubusercontent.com/100162043/215350390-6ef3ee89-d63c-4985-aa07-c447b3042108.jpg)


## Lopetus

Harmittaa, että en löytänyt ratkaisua apache2 tiedoistoihin. Tähän varmasti osaavat seuraavalla luennolla joku vastata. 
