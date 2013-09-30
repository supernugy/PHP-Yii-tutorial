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
Dá sa povedať, že skript napísaný v PHP je uložený na strane servera a klient, 
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
   
^^^^^^^^^^^^^^
Inštalácia PHP
^^^^^^^^^^^^^^

`PHP dowload <http://windows.php.net/download/>`_

^^^^^^^^^^^^^^^^^^^^^
Deklarace PHP skriptu
^^^^^^^^^^^^^^^^^^^^^

PHP skript sa delkaruje pomocou ``<?php nejaký PHP skript ?>`` ako to môžeme vidieť aj na
predošlom príklade. Tento spôsob delkarácie je najpoužívaniejší ale dá sa to robit 
aj pomocou ``<? nejaký PHP skript ?>``.

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

**Superglobálne**

Sú to predefinované premenné v PHP, ktoré môžu byť sprístupnené z akejkoľvek funkcie, triedy alebo súboru

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

**Globálne**

Sú to premenné, ktoré sú deklarované mimo funckií alebo deklarované pomocou slova global vo vnútri funkcií. 
Všetky globálne premenné sú dostupné v $GLOBALS. 

**Lokálne**

Premenné deklarované vo vnútri funkcií.

^^^^^
Polia
^^^^^

Polia v PHP využívajú kľúče a k nim priradené hodnoty (podobne ako Map v Jave).
K tomuto poľu sa môžeme chovať ako k obyčajnému poľu ku ktorému priradzujeme hodnoty: ::

   $pole = array ("PHP","MySQL","Apache"); //vytvoríme nové pole s troma prvkami
   $pole[] = 13;					//pridávame nový prvok na koniec poľa
   $pole[0] = "HTML";			//prepisujeme prvok na prvom mieste

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


-------------
Yii framework
-------------

Yii (skratka Yes it is!) je postavené na filozofii Convention over Configuration, čo znamená, že máte k dispozícií stavebné bloky, 
ktoré sa správajú tak, ako by ste od nich čakali (t.j. konvenčne) a iba ak chcete špecifické správanie, musíte ich dodatočne konfigurovať. 
V ideálnom prípade vyskladáte z týchto blokov celú aplikáciu s minimálnymi zásahmi do ich konfigurácie.

Veľkou výhodou Yii frameworku je generátor kódu, vďaka ktorému stačí navrhnúť schému databázy a po pár kliknutiach a trocha úsilí máte 
vygenerovanú skoro celú aplikáciu.

**Link na stiahnutie:** `Yii dowload <http://www.yiiframework.com/download/>`_

^^^^^^
Server
^^^^^^

Pred tým ako budeme môcť začať s tvorbou našej web appky, musíme nainštalovať
nejaký server (pokial už nemáte). Tu budeme používať Apache.

Podrobný tutorial inštalácie nájdete `tu <http://www.premiumwebbloghosting.com/2012/03/how-to-install-apache-server-on-windows.html>`_

^^^^^^^^^^^^^^^^^^^^^
Generovanie aplikácie
^^^^^^^^^^^^^^^^^^^^^

Skušobnú aplikáciu je potrebne generovat v cmd/terminali, následovným spôsobom: ::

   php yii/framework/yiic.php webapp brmbrm

Parametre príkazu sú ``<php alebo cesta k php.exe> <cesta ku yiic.php> <webapp> <miesto generovania>``

Po vygenerovaní je skušobná stránka plne funkčná aj keď iba veľmi základná.

^^^^^^^^^
MVC v Yii
^^^^^^^^^

Model zabezpečuje získavanie a ukladanie dát (najčastejšie z/do databázy), 
View je šablóna podľa ktorej sa dáta zobrazujú a Controller je akýsi hlavný 
prvok, ktorý sa zavolá ako prvý, vytvorí potrebný model a view-u z neho odovzdá 
vhodné dáta (prípadne odovzdá celý model). Controller taktiež vykonáva akékoľvek 
obslužné akcie ako je odosielanie mailov, ukladanie údajov prostredníctvom 
modelu, presmerovania, atď.

MVC pekne separuje rozdielne funkcie, takže nech máte hocijako zložitý kód, 
dá sa v ňom v pohode orientovať.

^^^^^^^^^^^^
Konfigurácia
^^^^^^^^^^^^

Konfigurácia je v súbore ``/protected/config/main.php``, kde treba odkomentovať 
aj "Gii" (modul generátora kódu) a nastaviť prístupové heslo k nemu. Pre Gii 
taktiež treba vypnúť filter IP adries, ktoré k nemu môžu pristupovať 
parametrom ``'ipFilters'=>array('*'),`` ak k nemu nepristupujete iba z localhostu.

Defaultne je už v konfigurácii nastavená ukážková SQLite databáza a ak 
chceme Yii len vyskúšať, môžete ju nechať tak. Pokiaľ plánujete použiť 
vlastnú DB, zakomentujte SQLite a odkomentujte MySQL (alebo tam dáme inú db).

Naša defaultna db je v ``/protected/data/testdrive.db`` v ktorej je základná tabuľka
a aj nejaké dáta. My si ju však narhneme po svojom a to pomocou firefox doplnku,
ktorý nájdete tu: `SQLite Manager <https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager/>`_

Nakoniec si nastavíme základného UrlManagera lebo defaultné ulr sú nechutné. ::

   ...
   'urlManager'=>array(
            'urlFormat'=>'path',
               'rules'=>array(
                   'pattern1'=>'route1',
                   'pattern2'=>'route2',
                   'pattern3'=>'route3',
               ),
         ),
   ...

^^^^^^^^^^^^^^^^
Generovanie kodu
^^^^^^^^^^^^^^^^

Gii (generátor kodu) nájdeme na adrese `<http://localhost/test_app/index.php/gii>`_, kde treba zadať zvolené heslo.
Následne sa preklikneme do Model Generator. Tu si vygenerujeme modely zodpovedajúce tabuľkám našej db aj s prípadnými reláciami.
Čiže ak máme v db tabuľku s názvom ``user`` tak ju napíšeme do kolonky ``Table Name`` klikneme na ``Preview``
a potom ``Generate``. A máme model pre našu tabuľku. Ak máme viacero tabuliek ktoré chceme využívať tak urobíme to
isté aj pre ne. 

^^^^^^^^^^^^^^^^^^^
Základy Controllera
^^^^^^^^^^^^^^^^^^^

Keď si otvoríme SiteController.php v ``/protected/controllers``, tak vo vnútri
uvidíme mnoho funkcií ktorých názov sa začína na ``action`` ako napríklad 
``actionLogin()``. ::

   public function actionLogin()
   {
      $model=new LoginForm;

      // if it is ajax validation request
      if(isset($_POST['ajax']) && $_POST['ajax']==='login-form')
      {
         echo CActiveForm::validate($model);
         Yii::app()->end();
      }

      // collect user input data
      if(isset($_POST['LoginForm']))
      {
         $model->attributes=$_POST['LoginForm'];
         // validate user input and redirect to the previous page if valid
         if($model->validate() && $model->login())
            $this->redirect(Yii::app()->user->returnUrl);
      }
      // display the login form
      $this->render('login',array('model'=>$model));
   }

Tieto akcie tvoria základ controllera a jednotlivé akcie sa vykonajú len ak
užívateľ zadá konkretnu url. Napríklad ``localhost/index.php/site/login`` 
kde ``site`` hovorí aký controller sa má použiť (može byť ich aj viac) a za
ním sa nachádza akcia ktorá sa má vykonať. Tu je to konkrétne ``actionLogin()``.

Jednou z najzákladnejších a najpoužívanejších metod v controlleri je 
``render(string $view, array $data=NULL)``, kde
``$view`` je pohľad (view), ktorý sa zobrazí v prehliadači a ``$data`` su dáta ktoré sa 
posielajú do pohľadu (napr. formulár). Táto metóda zobrazí daný pohľad.

^^^^^^^
Pohľady
^^^^^^^

Pohľady sa nachádzaju v ``/protected/views``. 
Delia sa na 2 druhy:
   * layouty
   * pohľady controllerov

Nás budú zaujímať predovšetkým pohľady controllerov.
Napríklad pohľad ``login.php`` sa zobrazí vtedy keď sa zavolá akcia login.
V tomto pohľade je definovaný formulár prihlásenia, ktorý používa nejakú
záhadnú premennú ``$model``. Táto premenná je definovaná v controlleri v akcii login.
Odtial bola poslaná do pohľadu spomínanou metodou ``render``.

Mohli sme si všimnút, že keď sa menú stránka tak sa mení len určitá časť stránky. 
Je to spôsobené tým, že všetky pohľady controllerov sa vykresľujú do nejakého 
layoutu. V tomto prípade je to layout ``\protected\views\layouts\main.php``.

"""""""""
Formuláre
"""""""""

Opäť zoberme ako príklad pohľad ``login.php``. Pri tvorbe formulárov budeme musieť
vytvoriť model formulára ako napr. ``\protected\models\LoginForm.php``.

V tejto triede sú dôležité:
   * public premenné do ktorých sa budú ukladať informácie dané userom
   * pravidlá (rules)
   * attributeLabels (ok tak toto nie je až také dôležite, ale je dobre to mať)

Keď si otvoríme login stránku tak uvidíme, že od nás chce username. Lenže my sa 
neskôr budeme chciet prihlasovať cez email, tak v tejto triede by sme mali
zmeniť všetky vyskyty username na email. Lenže mnohí programátori sú lenivý 
a nevadí im menšia nekonzistencie kodu, preto môžeme urobiť malý 'hack' a to
tým že ku ``attributeLabels`` pridáme ``'username'=>'Email',`` aby nám formulár
zobrazoval že chce email. Toto neovplyvní samotnú implementáciu prihlasovania cez 
email kedže overovanie input dát sa deje mimo formulára.

Keď už máme triedu formulára dokončenú tak musíme vytvoriť v controlleri vytvoriť
jej inštanciu, napr: ``$model=new LoginForm``. Následne sa pošle to pohľadu v ktorom
nás zaujíma prevažme kod ktorý vykresľuje formulár ::

   <?php $form=$this->beginWidget('CActiveForm', array(
      'id'=>'login-form',
      'enableClientValidation'=>true,
      'clientOptions'=>array(
         'validateOnSubmit'=>true,
      ),
   )); ?>

      <p class="note">Fields with <span class="required">*</span> are required.</p>

      <div class="row">
         <?php echo $form->labelEx($model,'username'); ?>
         <?php echo $form->textField($model,'username'); ?>
         <?php echo $form->error($model,'username'); ?>
      </div>

      <div class="row">
         <?php echo $form->labelEx($model,'password'); ?>
         <?php echo $form->passwordField($model,'password'); ?>
         <?php echo $form->error($model,'password'); ?>
         <p class="hint">
            Hint: You may login with <kbd>demo</kbd>/<kbd>demo</kbd> or <kbd>admin</kbd>/<kbd>admin</kbd>.
         </p>
      </div>

      <div class="row rememberMe">
         <?php echo $form->checkBox($model,'rememberMe'); ?>
         <?php echo $form->label($model,'rememberMe'); ?>
         <?php echo $form->error($model,'rememberMe'); ?>
      </div>

      <div class="row buttons">
         <?php echo CHtml::submitButton('Login'); ?>
      </div>

   <?php $this->endWidget(); ?>

Používame widget ``CActiveForm``, ktorý sa správa ako obýčajný html form lenže
prídáva 'Yii kompatibilitu' (čiže využívanie modelov a formulárov). 
Najdôležitejšia vec ktorú treba vedieť je ako funguje priradzovanie premenných.

Napr. ``echo $form->textField($model,'username')`` zobrazí textové políčko, ktorého
hodnota bude v controlleri priradená k premennej ``username`` v ``LoginForm`` 
(všimnite si, že sa všetky premenné zhodujú s premennými v LoginForm).

Na konci každého formulára by mal byť submit button: ``echo CHtml::submitButton('Login')``.
Po jeho stlačení sa opäť vykoná akcia ``actionLogin`` lenže s iným priebehom: ::

   if(isset($_POST['LoginForm']))
	{
		$model->attributes=$_POST['LoginForm'];
		// validate user input and redirect to the previous page if valid
		if($model->validate() && $model->login())
			$this->redirect(Yii::app()->user->returnUrl);
	}

Tento kod sa vykonáva ak sa v superglobálnej premennej $_POST nachádzaju dáta s indexom
'LoginForm' (presný názov triedy). Tento prípad nastane len po submitnutí formulára.
No a vo vnutri ifu sa už môžu spracovávať dáta (v tomto prípade login).

^^^^^^^^^^^^^^^^^
Model používateľa
^^^^^^^^^^^^^^^^^

Upravíme si vygenerovaný model používateľa - protected/models/User.php. ::

   class User extends CActiveRecord
   {

      protected $_oldPassword;
      protected $_fullName;

      /**
       * Returns the static model of the specified AR class.
       * @param string $className active record class name.
       * @return User the static model class
       */
      public static function model($className=__CLASS__)
      {
         return parent::model($className);
      }

      /**
       * @return string the associated database table name
       */
      public function tableName()
      {
         return 'user';
      }

      /**
       * @return array validation rules for model attributes.
       */
      public function rules()
      {
         // NOTE: you should only define rules for those attributes that
         // will receive user inputs.
         return array(
            array('email, first_name, last_name, password', 'required'),
            array('email', 'email'),
            // The following rule is used by search().
            // Removed password
            array('id, email, first_name, last_name', 'safe', 'on'=>'search'),
         );
      }

      /**
       * @return array relational rules.
       */
      public function relations()
      {
         // NOTE: you may need to adjust the relation name and the related
         // class name for the relations automatically generated below.
         return array(
         );
      }

      /**
       * @return array customized attribute labels (name=>label)
       */
      public function attributeLabels()
      {
         return array(
            'id' => 'ID',
            'email' => 'Email',
            'first_name' => 'First Name',
            'last_name' => 'Last Name',
            'password' => 'Password',
         );
      }

      /**
       * Retrieves a list of models based on the current search/filter conditions.
       * @return CActiveDataProvider the data provider that can return the models based on the search/filter conditions.
       */
      public function search()
      {
         // Warning: Please modify the following code to remove attributes that
         // should not be searched.

         $criteria=new CDbCriteria;

         $criteria->compare('id',$this->id);
         $criteria->compare('email',$this->email,true);
         $criteria->compare('first_name',$this->first_name,true);
         $criteria->compare('last_name',$this->last_name,true);
         $criteria->compare('password',$this->password,true);

         return new CActiveDataProvider($this, array(
            'criteria'=>$criteria,
         ));
      }
      protected function getHash($password)
      {
         //Add you custom string here
         return md5("supernugy is awesome" . $password);
      }

      function afterFind()
      {
         $this->_oldPassword = $this->password;
         $this->password = '';
         
         $this->_fullName = $this->first_name.' '.$this->last_name;

         return parent::afterFind();
      }

      function beforeSave()
      {
         if (!$this->password)
            $this->password = $this->_oldPassword;
         else
            if ($this->_oldPassword != $this->password) $this->password = $this->getHash($this->password);

         return parent::beforeSave();
      }
         
      public function matchesPassword($password)
      {
         return ($this->getHash($password) == $this->_oldPassword);
      }
   }

^^^^^^^^^^^^^^^^^^^
Prihlasovanie v Yii
^^^^^^^^^^^^^^^^^^^

Na overenie identity uživateľov sa používa trieda UserIdentity, ktorá sa nachádza v 
``protected/components/UserIdentity.php`` ::
   
   class UserIdentity extends CUserIdentity
   {
      
      public $email;
      private $_id;
      
      public function __construct($email,$password)
      {
         $this->email = $email;
         $this->password = $password;
      }
      
      /**
       * Authenticates a user.
       * @return boolean whether authentication succeeds.
       */
      public function authenticate()
      {
         $u = User::model()->findByAttributes( array('email'=>$this->email) );
         
         if ( !$u )
            $this->errorCode = self::ERROR_USERNAME_INVALID;
         else if( !$u->matchesPassword($this->password) )
            $this->errorCode = self::ERROR_PASSWORD_INVALID;
         else 
         {
            $this->_id = $u->id;
            $this->username = $this->email;
            $this->errorCode = self::ERROR_NONE;
         }
         
         return !$this->errorCode;
      }
      
      public function getId()
      {
         return $this->_id;
      }
   }

Ďalej by bolo dobré pridať triedu WebUser ``protected/components/WebUser.php`` 
čo je špeciálna trieda, ktorej inštancia je globálne dostupná v aplikácii 
cez Yii::App()->user. ::

   class WebUser extends CWebUser {

      protected $_model = null;

      //Pokiaľ nie je načítaný model, loadne ho a vráti. V $this->id je vždy ID 
      //prihláseného používateľa, ktoré keď chýba, metóda vracia prázdny model.
      public function getModel()
      {
         if (!$this->_model)
         {
            if ($this->id) $this->_model = User::model()->findByPk($this->id);
            else $this->_model = User::model();
         }

         return $this->_model;
      }
   }

Nakoniec do konfigurácie protected/config/main.php musíme ešte pridať jeden riadok, 
aby sa používal náš WebUser namiesto defaultej implementácie ::

   ...
   'components'=>array(
      'user'=>array(
         'allowAutoLogin'=>true,
         'class' => 'WebUser', // tento riadok treba pridat
      ),
   ...

A teraz už len stačí dať do našej db skušobnéhu usera a skúsiť sa s ním prihlásiť.

^^^^^^^^^^^^^^^^
Práca s DB v Yii
^^^^^^^^^^^^^^^^

Na záver si ukážeme ako pracovať sa v Yii pracuje s databázou (čítanie a zapisovanie).
Na tento účel si vytvoríme novú stranku, kde si budeme moct zmeniť osobné údaje.

""""""""""""""""
Vytvorenie akcie
""""""""""""""""

Pred tým než budeme moct vytvoriť nový akciu budeme potrebovať nový formulár 
aj pohľad. Začneme formulárom.

Vytvoríme si ``UserInfoForm.php`` s kodom: ::

   <?php
   class UserInfoForm extends CFormModel
   {
      public $email;
      public $password;
      public $first_name;
      public $last_name;

      public function rules()
      {
         return array(
            // username and password are required
            array('email, password, first_name, last_name', 'required'),
         );
      }

      /**
       * Declares attribute labels.
       */
      public function attributeLabels()
      {
         return array(
            'password'=>'Password',
            'email'=>'Email',
            'first_name'=>'First Name',
            'last_name'=>'Last Name',
         );
      }

   }

Teraz si vytvoríme pohľad ``changeUserInfo.php``: ::

   <h1>Change user info</h1>

   <div>
       <?php 
         if(Yii::app()->user->hasFlash('change_info'))
         {
            echo Yii::app()->user->getFlash('change_info');
         }?>
   </div>

   <div class="form">
   <?php $form=$this->beginWidget('CActiveForm', array(
      'id'=>'login-form',
      'enableClientValidation'=>true,
      'clientOptions'=>array(
         'validateOnSubmit'=>true,
      ),
   )); ?>

      <p class="note">Fields with <span class="required">*</span> are required.</p>

      <div class="row">
         <?php echo $form->labelEx($model,'email'); ?>
         <?php echo $form->textField($model,'email'); ?>
         <?php echo $form->error($model,'email'); ?>
      </div>

      <div class="row">
         <?php echo $form->labelEx($model,'password'); ?>
         <?php echo $form->passwordField($model,'password'); ?>
         <?php echo $form->error($model,'password'); ?>
      </div>

      <div class="row">
         <?php echo $form->labelEx($model,'first_name'); ?>
         <?php echo $form->textField($model,'first_name'); ?>
         <?php echo $form->error($model,'first_name'); ?>
      </div>
      
      <div class="row">
         <?php echo $form->labelEx($model,'last_name'); ?>
         <?php echo $form->textField($model,'last_name'); ?>
         <?php echo $form->error($model,'last_name'); ?>
      </div>

      <div class="row buttons">
         <?php echo CHtml::submitButton('Login'); ?>
      </div>

   <?php $this->endWidget(); ?>
   </div><!-- form -->

V ``SiteController.php`` si vytvoríme novú akciu tým že tam dodáme: ::

   public function actionChangeUserInfo()
   {
      $model = new UserInfoForm;
      $currentUser = User::model()->findByAttributes(array('id'=>Yii::app()->user->getId()));
      
      if($currentUser == null)
      {
         $this->redirect(array('site/index'));
         return;
      }
      
      //load existin data
      $model->email = $currentUser->email;
      $model->first_name = $currentUser->first_name;
      $model->last_name = $currentUser->last_name;
      
      if(isset($_POST['UserInfoForm']))
      {
         $model->attributes=$_POST['UserInfoForm'];
         $currentUser->email = $model->email;
         $currentUser->password = $model->password;
         $currentUser->first_name = $model->first_name;
         $currentUser->last_name = $model->last_name;
         
         if($currentUser->update())
         {
            Yii::app()->user->setFlash('change_info','User information changed!');
         }
         else 
         {
            Yii::app()->user->setFlash('change_info','ERROR');
         }
      }
      
      $this->render('changeUserInfo',array('model'=>$model));
   }

Premenná ``$currentUser`` je vlastne User model ktorý má v sebe info o teraz prihlásenom
užívateľovi. Následne sa jeho údaje vložia do formulára ktorý sa pošle pohľady.
Vďaka tomu uz budeme mat vo formulári existujúce data ktoré si možeme prezrieť a upraviť.
Po submitnutí sa nové data ulozia do premennej ``$currentUser`` a pouzijeme metodu ``update()``.

Nakoniec aby sme nemuseli stale písať ručne url, tak si vytvoríme link na hlavnom menu.

Čiže v layoutu ``\protected\views\layouts\main.php`` si najdeme tento kod: ::

	<div id="mainmenu">
		<?php $this->widget('zii.widgets.CMenu',array(
			'items'=>array(
				array('label'=>'Home', 'url'=>array('/site/index')),
				array('label'=>'About', 'url'=>array('/site/page', 'view'=>'about')),
				array('label'=>'Contact', 'url'=>array('/site/contact')),
				array('label'=>'Login', 'url'=>array('/site/login'), 'visible'=>Yii::app()->user->isGuest),
				array('label'=>'Logout ('.Yii::app()->user->name.')', 'url'=>array('/site/logout'), 'visible'=>!Yii::app()->user->isGuest)
			),
		)); ?>
	</div><!-- mainmenu -->

Tento kus kodu vykresluje hlavne menu a položky v ňom. Tu za 'Contact' pridáme riadok 
``array('label'=>'Change Info', 'url'=>array('/site/changeUserInfo')),`` čím pridáme 
nový button ktorý sa odkazuje na našu novú akciu.

-----
Úloha
-----

Úlohou je vytvoriť funkčnú stránku registrácie. Táto úloha pozostáva z viacerých 
menších úloh:

   * vytvoriť registračný formulár
   * vytvoriť akciu registrácie, kde sa nový user uloží do db
   * vytvoriť pohľad registrácie
   * vytvoriť link na túto stránku

Poznámky: pri vytvárani nového usera použijeme metodu ``save()`` namiesto ``update()``.



