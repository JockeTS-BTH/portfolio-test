---
Title: Load
Description: This is our load page.
---

# Webbplatsers Laddningstider

## Urval
Jag började med bth.se eftersom det kändes lämpligt att testa webbplatsen tillhörande den institution där jag studerar.

Därefter ville jag testa en kommersiell webbplats med inriktning på främst teknik-produkter. För detta ändamål valdes Webhallen.

Jag valde webbplatser inom tekniska områden då jag antog att dessa skulle vara ganska väl optimerade för hastighet och användarupplevelse. Den här analysen blev således en möjlighet att testa detta antagande.

## Metod
Det första steget är att köra varje webbplats i Google's verktyg PageSpeed Insights. Där testas webbplatsen och får ett antal betyg i olika kategorier, där "Performance" är det vi är mest intresserade av i den här undersökningen. 

Vidare får man även data på hur lång tid olika moment tar från det att webbläsaren gör en första förfrågan till att servern levererar innehållet samt hur lång tid det tar för webbläsaren att rendera detsamma. Man kan växla mellan att se denna data för både mobil och desktop. 

Man får även förslag på åtgärder att vidta för att snabba upp webbplatsen, såsom att ta bort kod som inte används och att minifiera filer. Även rena fel listas och hur mycket dessa påverkar tiden.

Därefter används Chrome DevTools för att undersöka innehållet som skickats från servern samt hur lång tid detta tagit. Network-fliken används för att se hur många förfrågningar som gjorts, storleken på de resurser som skickats över nätverket (i komprimerat format) samt tiden det tog i sekunder för webbläsaren att ta emot dessa. 

## Parametrar
First Contentful Paint (FCP) är tiden från förfrågan tills dess att det första innehållet börjar renderas i webbläsaren.

Largest Contentful Paint (LCP) är tiden från förfrågan tills dess att det största innehållet i viewporten har renderats.

Speed Index (SI) mäter tiden från förfrågan tills dess att allt innehåll i viewporten har renderats.

Time to Interactive (TTI) är tiden det tar tills det går att interagera med sidan. Tex att scrolla eller klicka på olika element.

Total Blocking Time (TBT) mäter tiden mellan FCP och TTI där huvudtråden var blockerad i mer än 50 ms vilket gör att sidan upplevs som långsam.

Cumulative Layout Shift (CLS) mäter hur mycket de olika elementen flyttas runt när sidan laddas in. En högre poäng gör det mer sannolikt att användaren av misstag klickar på länkar i ett försök att navigera innehållet.

## Resultat

<div class="embed-container">
    <iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQ5KBmwVb0i1AR5PPIviBFTDfox6S2rRYj2cnXsVg7b7DkEQkgf2QTlr-u1jZ_FFNvLRXZcvH--cxsj/pubhtml?widget=true&amp;headers=false"></iframe>
</div>

### BTH

<img src="%assets_url%/img/bth.png" alt="bth" width="500">

Det verkar som att BTH har en hel del kod på sin webbplats som inte används. Främst i form av JavaScript men även CSS. Bara att ta bort denna skulle spara nästan 4 sekunder för mobila enheter. Google föreslår även att förkorta svarstiden från servern, minifiera JS och spara bilder i "next-gen"-format.

### Webhallen

<img src="%assets_url%/img/webhallen.png" alt="webhallen" width="500">

Även här står oanvänd JS och CSS för den största orsaken till längre laddtider. Det står även att vissa resurser blockerar renderingen, vilket jag antar innebär att det körs JS innan DOM-trädet är färdigtbyggt. Dessa kan då placeras längst ner i koden alternativt använda "defer"-keywordet för att vänta på sin tur.

### PC för Alla

<img src="%assets_url%/img/pcforalla.png" alt="pcforalla" width="500">

Här verkar det enbart vara oanvänd JS/CSS som gör webbplatsen långsammare. Att ta bort denna skulle resultera i ett tidsspar om lite mer än en sekund.

## Analys
Av mina mätningar att döma så verkar det som att det är en stor skillnad i hastighet beroende på om man ansluter till webbplatserna med desktop eller mobil enhet. 

Jag vet inte hur tillförlitliga resultaten är eftersom de skiljer så mycket och undrar ifall PageSpeed Insights emulering av en Moto G4 påverkar hastigheten. 


Även fast den överförda datamängden var nästan identisk (något lägre på mobil) så var många av parametrarna (FCP, SI, LCP, TTI) ofta 4 gånger så långsamma på mobil jämfört med desktop. 

Detta återspeglas även i det övergripande betyget (Performance) som webbplatserna fick av PS Insights. Det låg oftast under 25 för BTH och Webhallen men var betydligt bättre hos PC för Alla.

Den gemensamma nämnaren för alla sidor verkar vara att det ligger oanvänd kod (JS/CSS) och skräpar på servern, vilket drar ner hastigheten mer än man kanske kunde tro.

Överlag så skulle jag utse PC för Alla till vinnare i det här testet. Den gjorde minst antal requests och filstorleken var något mindre. Men framförallt så laddade den nästan 75% snabbare än de två andra på nätverkssidan. Den var inte bäst i alla kategorier men överlag var den betydligt snabbast i det här testet.

Personligen skulle jag nog säga att man i de flesta lägen förväntar sig att en sida inte tar längre än ca 2 sekunder att ladda innan man börjar bli stressad och frustrerad. På mobil kanske man kan vara lite mer tålmodig och sätta gränsen till 3 sekunder. 

Jag upplevde trots det att samtliga testade webbplatser uppfyllde dessa krav när jag surfade runt både på mobil och desktop så jag är inte riktigt säker på att resultaten som PageSpeed Insights visade är 100% tillförlitliga i alla lägen.

## Referenser
<a href="https://bth.se/" class="reference">BTH</a>
<a href="https://www.webhallen.com/se/" class="reference">Webhallen</a>
<a href="https://pcforalla.idg.se/" class="reference">PC för Alla</a>

## Övrigt
Analys genomförd och skriven av Jocke T. Sjölin