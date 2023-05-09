Difficulty: Very Easy

## Description
Dit team opdagede, at en af lederne i den finansielle afdeling begik bedrageri ved at stjæle penge ved hjælp af falske fakturaer fra en hemmelig kontakt. Desværre er han allerede flygtet fra landet. Du har gendannet nogle mapper fra hans Windows 10 papirkurv.

Det er op til dig at hente informationen for at muligvis fange ham.

Flaget skal besvare 3 spørgsmål:

1.  I hvilken mappe var tvivlsomme beskeder skjult?
2.  Hvor mange fakturafiler var der i januar 2023?
3.  Hvem er den hemmelige kontakt og mulige vidne?

file: Recycle Bin.zip

**Flag Format**

Finder du de ondsindede beskeder i `C:\Brugere\Finance\Dokumenter\mappe0\mappe1\beskeder.msg`, finder 25 fakturarer for januar 2023, og den hemmelige kontakt til at være `Max Mustermann`, er flaget:

`DDC{mappe1_25_MaxMustermann}`

## Phase 1
åbner vi zip filen kan vi se en bunke af filer
![[./Opened-zipfile.png]]
Vi kan åbne en terminal i mappen og derefter gør vores magi.

Hvis vi cat'er alt i mappen får vi noget underlidt output
![[./Cat-Everything.png]]
Vi kan derefter snævre det lidt mere ned, .msg filerne ser ud til at være outlook filer, så lad os fokusere på dem.
Derfor cat'er vi alle filer der ender på .msg
![[./Cat-msg-filer.png]]
Hvis vi så læser navnene på alle filerne, kan vi se noget med en der hedder CONFIDENTIONAL.
Det er da ret mystisk?
Okay, den ligger i Suits mappen.

1. Suits

## Phase 2
Vi skal nu finde hvor mange fakturaer der er fra Januar.
Derfor kan vi nu cat alle TXT filerne.
![[./Cat-txt-filer.png]]
Der er lidt for meget data til at vi gider at tælle det hele, derfor kan vi kopiere dataen ind i vores elskede gui text editor og search for hvor mange gange der står 01_Jan
![[./Hvor-mange-Jan.png]]
21 gange, det vil sige at der har ligget 21 fakturaer fra Januar måned

2. 21

## Phase 3
Der var en txt fil som gav os en masse dejlig info da vi cat'ede alle txt filerne.
![[./Sidste-txt-fil.png]]
Vi ved fra phase 1 at det var en samtale i Suits afdelingen der så mistænktsom ud.
Vi kan derfor drage til konklusion at det var Garold Hunderson som det var at han skrev med.

3. Garold Hunderson

Når vi så sammensætter det hele får vi flaget
`DDC{Suits_21_GaroldHunderson}`

