.. highlight:: rst

============================
PHP + Yii tutorial
============================

-----------
Základy PHP
-----------

PHP je open-source skriptovací programovací jazyk, ktorý umožňuje procedurálne, 
alebo objektovo orientované programovanie.
Využíva sa najmä na programovanie klient-server aplikácii na strane servera a 
programovanie interaktívnych dynamických www stránok a aplikácií.
Dá povedať, že skript napísaný v PHP je uložený na strane servera a klient, 
ktorý ho volá, dostane ako odpoveď klasickú statickú (X)HTML stránku.

Napríklad:
Do zdrojového kódu PHP skriptu napíšeme::

   <html>

    <body>

     <?php echo "Dnes je ".date("j.n.")."\n"; ?>

    </body>

   </html>

Server stránku spracuje a keď si zobrazíte zdrojový kód v prehliadači, uvidíte iba toto: ::

   <html>

    <body>

     Dnes je 26.10.

    </body>

   </html>

^^^^^^^^^^^^^^^^^^^^^
Deklarace PHP skriptu
^^^^^^^^^^^^^^^^^^^^^

PHP skript sa delkaruje pomocou <?php nějaký PHP skript ?> ako to môžeme vidieť aj na
predošlom príklade. Tento spôsob delkarácie je najpoužívaniejší ale dá sa to robit 
aj pomocou <? nějaký PHP skript ?>.

^^^^^^^^
Premenné
^^^^^^^^

Základné informácie o premenných:
   * premenné sú v php skriptoch reprezentované znakom $ pred názvom premennej.
   * nedeklarujeme typ premennej
   * nazvy premenných sú case-sensitive
   * názov premennej sa môže začínať len písmenom abecedy alebo "podčiarkou" ("_")
   * väčšinou je ku premennej priradená hodnota ale dá sa priradiť aj referencia na inú premennu použitím "&"

Napr: ::

   <?php
   $var = 'Bob';
   $Var = 'Joe';
   echo "$var, $Var";      // outputs "Bob, Joe"

   $foo = 'Bob';              // Assign the value 'Bob' to $foo
   $bar = &$foo;              // Reference $foo via $bar.
   $bar = "My name is $bar";  // Alter $bar...
   echo $bar;
   echo $foo;                 // $foo is altered too.
   ?>

""""""""""""""""""
3 typy premenných:
""""""""""""""""""

**Superglobálne*

Sú to predefinované premenné v PHP, ktoré môžu byť sprístupnené z akejkoľvek funkcie, triedy alebo súboru.
Sú to: 
   * $GLOBALS
   * $_SERVER
   * $_REQUEST
   * $_POST
   * $_GET
   * $_FILES
   * $_ENV
   * $_COOKIE
   * $_SESSION

**Globálne*

Sú to premenné, ktoré sú deklarované mimo funckií alebo deklarované pomocou slova global vo vnútri funkcií. 
Všetky globálne premenné sú dostupné v $GLOBALS. 

**Lokálne*

Premenné deklarované vo vnútri funkcií.

^^^^^
Polia
^^^^^

Polia v PHP využívajú kľúče a k nim priradené hodnoty (podobne ako Map v Jave).
K tomuto poľu sa môžeme chovať ako k obyčajnému poľu ku ktorému priradzujeme hodnoty: ::

   $pole = array ("PHP","MySQL","Apache");	//vytvoríme nové pole s troma prvkami
   $pole[] = 13;							//pridávame nový prvok na koniec poľa
   $pole[0] = "HTML";						//prepisujeme prvok na prvom mieste

alebo ako k mape (napr pri slovníku): ::

   $pole = array(
       "slovo" => "word",
       "stolička" => "chair",
      "stôl" => "table",
   );
   $pole["PHP"] = "PHP: Hypertext Preprocessor";	//pridávame nový prvok s nový kľúčom

V prvom príklade nezadávame žiadne kľúče takže kľúčmi sú teraz indexy. Takéto pole
sa nazýva indexované. Indexuje sa od nuly, tak ako zvýčajne.
V druhom príklade zadávame kľúč a k nemu hodnotu (key  => value). Takéto pole
voláme asociatívne.

^^^^^^^
Funkcie
^^^^^^^

Pri vytváraní vlastných funkcií sa používa následovná syntax ::

function napis($meno, $priezvisko)
{
echo "$meno";
echo "$priezvisko";
}

Funkcia môže obsahovať vstupné argumenty pričom ich počeť môže byť ľobovolný (aj nula).

^^^^^^
Triedy
^^^^^^

V PHP je trieda kolekciou premenných a funkcií, ktoré pracujú s týmito premennými. 
V triedach sú premenné definované pomocou var. No často sa definujú aj pomocou public, private, protected... ::

   class Cart 
   {
       var $items;  // Items in our shopping cart

       // Add $num articles of $artnr to the cart

       function add_item($artnr, $num) 
      {
           $this->items[$artnr] += $num;
       }
   }

Funkcie možu byt tiez definované pomocou public, private, protected...
Vytvoriť a používať objekt tejto triedy môžeme nasledovne ::

   $cart = new Cart;
   $cart->add_item("10", 1);

Môžeme si všimúť že na rozdiel od iných jazykov ako Java alebo C++ metody/funkcie sa
volajú pomocou "->" a nie "."

----------------
MVC architektúra
----------------

Architektura MVC delí aplikáciu na 3 logické časti tak, aby ju šlo upravovať samostatne a dopad zmien bol na ostatné časti co najmenší. 
Tieto tri časti sú: Model, View a Controller. 

Model reprezentuje data, business logiku aplikacie ale aj pracu s databázami.

View zobrazuje uživateľské rozhranie, je to zväčša phtml šablona.

Controller má na starosti tok udalostí v aplikácii a obecne aplikačnú logiku.
Controller môžeme chápať ako spojovníka s ktorým komunikuje model aj view. Teda
drží cely systém pohromade a komponenty prepojuje

Táto architektúra sa používa vo webových aplikáciach.