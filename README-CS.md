Případová studie: Dynamické zobrazení EAN a Hmotnosti v Shopify
Souhrn
Jedná se o implementaci na míru vytvořeného modulu pro Shopify, který na produktové stránce dynamicky zobrazuje EAN (čárový kód) a specifickou hmotnost produktu. Informace se aktualizují v reálném čase při změně produktové varianty, což zákazníkovi poskytuje okamžitý přístup k důležitým technickým parametrům.

Předpoklady a nastavení
Tato funkce využívá standardní vlastnosti varianty v Shopify. Nevyžaduje tvorbu žádných vlastních metapolí. Pro správnou funkci je potřeba mít v administraci Shopify u jednotlivých variant vyplněna tato pole:

EAN (Čárový kód): V detailu varianty, v sekci Skladové zásoby, vyplňte pole Čárový kód (ISBN, UPC, GTIN atd.).

Hmotnost: V detailu varianty, v sekci Doprava, vyplňte pole Hmotnost. Váha se musí zadávat v gramech (skript ji automaticky přepočítá a zobrazí v kg).

Detaily implementace
Vzhledem ke specifikům a zjištěným problémům s načítáním externích skriptů v použitém motivu bylo finální řešení navrženo jako jeden soběstačný blok kódu vložený přímo do šablony product.liquid. Tento přístup zaručuje stabilitu a plnou nezávislost na problematických částech motivu.

Řešení se skládá z několika částí:

Datová vrstva: Skript pomocí jazyka Liquid připraví na serveru globální JavaScriptový objekt window.productVariantData, který obsahuje čárový kód a hmotnost pro všechny varianty a zpřístupní je v prohlížeči.

HTML a CSS: Součástí bloku jsou prázdné HTML "placeholdery" (<div class="product-details-extra">) a vložený <style> tag, který definuje kompletní vzhled a zarovnání těchto prvků.

Logika: Izolovaný JavaScriptový skript čeká na načtení stránky (DOMContentLoaded), poté naslouchá na standardní událost 'change' na formuláři. Po změně varianty spustí funkci, která z připravených dat vybere správné hodnoty, naformátuje je a dynamicky je vloží do připravených HTML prvků.

Použití
Pro aktivaci funkce u produktu stačí v administraci Shopify vyplnit u jeho variant pole "Čárový kód" a/nebo "Hmotnost". Pokud pole pro danou variantu není vyplněno, příslušný řádek se na stránce automaticky nezobrazí, což zajišťuje plnou flexibilitu.