.. highlight:: rst

============================
PHP + Yii tutorial
============================

-----------------
Základy PHP
-----------------

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

-----
Links
-----

* `Sphinx <http://sphinx.pocoo.org>`_
* `Sphinx tutorial <http://sphinx.pocoo.org/tutorial.html>`_
* `reStructuredText Primer <http://sphinx.pocoo.org/rest.html#rst-primer>`_
* `Quick reStructuredText reference <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_ 
* `Sphinx documentation <http://sphinx.pocoo.org/contents.html>`_
* `rst2pdf (generates PDF from reStructuredText) <http://code.google.com/p/rst2pdf/>`_

