# Inlämningsrapport

Information
OBS!!! Ändra absolut inte på rubrikerna i denna fil!!!!

## Databasdesign

### Beskriv hur du har strukturerat din data i MongoDB

För att strukturera data i MongoDB har jag skapat en collection kallad recipes där varje recept lagras som ett dokument. Varje dokument innehåller fält som beskriver olika aspekter av ett recept, inklusive name (receptets namn), cookingTime (tillagningstid), ingredients (en lista med ingredienser) och steps (en lista med tillagningssteg). Denna struktur gör det enkelt att hantera varje recept som en självständig enhet och underlättar för CRUD-operationer på enskilda dokument.

--- Skriv ovanför och ta inte bort denna raden ---

### Jämför kort hur denna struktur skiljer sig från hur du skulle ha gjort i en relationsdatabas

I en relationsdatabas hade jag skapat en tabell för recipes, där varje recept är en rad och varje egenskap (exempelvis name, cookingTime, ingredients, steps) motsvarar en kolumn. Eftersom ingredienser och steg är listor hade jag förmodligen skapat ytterligare tabeller för dessa, för att representera relationerna mellan recepten och deras ingredienser respektive steg. I MongoDB kan dessa strukturer direkt ligga i dokumentet, medan en relationsdatabas skulle kräva flera tabeller och relationer för att uppnå samma resultat

--- Skriv ovanför och ta inte bort denna raden ---

### Nämn några skillnader mellan relationsdatabaser och dokumentdatabaser

Relationsdatabaser använder tabeller och strukturerar data i rader och kolumner med starkt definierade relationer. Dokumentdatabaser, som MongoDB, använder dokument i collections, där data är mer flexibel och inte behöver följa en strikt schema.
I relationsdatabaser normaliseras data ofta för att minimera redundans, medan dokumentdatabaser kan duplicera data för att underlätta läsoperationer.
Relationsdatabaser är vanligtvis starkt typade med fördefinierade datatyper för varje kolumn, medan dokumentdatabaser kan hantera dynamiska och varierande datatyper i dokument.


--- Skriv ovanför och ta inte bort denna raden ---

### Förklara vad collection, document och field är

Collection: En collection är en samling dokument och motsvarar en tabell i en relationsdatabas. Det är en grupp dokument som vanligtvis relaterar till ett gemensamt tema, till exempel recipes för alla recept.
Document: Ett dokument är en individuell post i en collection, motsvarande en rad i en tabell i en relationsdatabas. Dokumentet innehåller data för ett specifikt objekt och är representerat som en uppsättning fält och värden.
Field: Ett fält är en nyckel-värdepar i ett dokument, där nyckeln är namnet på egenskapen (t.ex. name, cookingTime) och värdet är datan för den egenskapen. Fält motsvarar kolumner i en tabell.
--- Skriv ovanför och ta inte bort denna raden ---

### Beskriv vad det är för skillnad på BSON och JSON

BSON (Binary JSON) är ett binärt format som används internt av MongoDB för att lagra dokument. BSON liknar JSON men är optimerat för snabbare läs- och skrivprestanda och tillåter fler datatyper, som datum och binära data, vilket gör det mer effektivt för databasanvändning. JSON (JavaScript Object Notation) är ett textbaserat format som används för att strukturera data på ett lättläst sätt, ofta i webbsammanhang. BSON är en binär version av JSON och är mer kompakt samt stöder fler datatyper än standard JSON

--- Skriv ovanför och ta inte bort denna raden ---
