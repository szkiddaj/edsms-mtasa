## edsms-mtasa
Automatikus jóváírás SMS fizetés esetén MTA:SA-n. A fizetést követően bármilyen kódot le lehet futtatni MTA--n ezzel a kóddal. (Szóval csinálhatsz olyan SMS jóváírást mint seen.)

**Követelmények**
Webtárhely
MTA szerver
SQL adatbázis

## Telepítés menete
Hozz létre egy ACL  felhasználót az MTA szerveren, a belépési adatokat add meg a php kódban (edsms.php), majd az **acl.xml-be rakd be az alábbi kódokat.** (Ha nem rakod be nem fog működni.)

    <group name="php">
		<acl name="phpgroup"></acl>
		<object name="user.phpsdk"></object>
	</group>

    <acl name="phpgroup">
		<right name="general.http" access="true"></right>
		<right name="command.authserial" access="false"></right>
	</acl>

A(z) **src/mtasa/** mappa tartalmát rakd bele a **mods/deathmatch/resources** mappába, majd indítsd el. **(Ha át akarod nevezni a mappát, akkor az új nevét is írd bele az edsms.php-ba, mivel azt a resourcet fogja meghívni.)**

A(z) **src/web/** mappa tartalmát másold fel egy webtárhelyre, egy olyan helyre ahol webről is eléred. (Szóval megtudod úgy nyitni böngészőbe hogy https://127.0.0.1/edsms.php például.)

Nyisd meg az edsms.php-t, majd add meg a felső részben lévő változókba, a szükséges adatokat. (SQL hozzáférés, ACL account hozzáférés, stb..)
A phpMyAdminban válaszd ki a szervered adatbázisát, majd menj az SQL fülre felül. Másold be az alábbi kódot, majd nyomd meg az indítás gombot.

    CREATE TABLE `edsms`.`edsms` ( `id` INT(11) NOT NULL AUTO_INCREMENT , `phone` VARCHAR(16) NOT NULL , `value` INT(6) NOT NULL , `prefix` VARCHAR(24) NOT NULL , `msg` TEXT NOT NULL , PRIMARY KEY (`id`)) ENGINE = InnoDB;

**Az alábbi részben az SRKHOST-nál lévő EDSMS rendszerhez való beállítást fogom bemutatni, más hostingoknál lehet máshogy lesz!**

Lépj be az ügyfélkapuba a **https://ugyfelkapu.srkhost.eu** címen, majd menj az egyenleg fülre, azon belül az **EDSMS menüpontra.** Ha még nincs EDSMS prefixed, igényelj egyet. Válasz üzenet helyett válaszd ki a feldolgozó fájlt, majd add meg a PHP kód elérési linkjét. (https://127.0.0.1/edsms.php például) Ha esetleg már van sms prefixed, menj a beállítások menüpontra, majd válaszd ki a feldolgozó fájlt, és oda másold be a PHP kód elérési linkjét.