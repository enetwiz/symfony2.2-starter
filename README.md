Symfony2 (2.2) - instalacja bazowa
==================================



Czym jest instalacja bazowa?
----------------------------

Celem niniejszego pakietu jest umożliwienie szybkiego utworzenia nowego projektu Symfony 2.2 wraz z podstawowymi 
pakietami i bibliotekami jakimi jak:

 * jQuery - popularna biblioteka JS (domyslnie jest jednak ladowana z Google CDN)
 
 * / wkrótce / Initializr - pakiet startowy dla projektow HTML5 :: [http://www.initializr.com](http://www.initializr.com)
 
 * TwitterBoostrap :: bundle [BraincraftedBootstrapBundle](http://bootstrap.braincrafted.com) + kompilator NodeJs

 * SonataAdminBundle - [panel administracyjny](http://sonata-project.org/bundles/admin/master/doc/index.html) wraz z 
   obsluga ORM Doctrine

 * FOSUserBundle - [moduł zarządzania użytkownikami](https://github.com/FriendsOfSymfony/FOSUserBundle) (logowanie, 
   edycja konta, uprawnienia)
 
 * Composer - narzędzie do zarządzania zależnościami (przypomina nieco PEAR)
 
Wazna wlasciwoscia instalacji bazowej jest wyodrebnienie bibliotek (bundle'i) Symfony2 poza katalog z projektami, dzieki 
czemu mozna uzyskac wspoldzielenie klas w ramach tego samego serwera, przy okazji zwiekszajac efektywnosc dzialania
akceleratorow PHP jak chociazby popularny APC. 

W instrukcji zawarta jest rowniez podpowiedz dotyczaca instalacji i konfiguracji kompilatora Nodejs (kompilatora plikow 
LESS), a takze opis konfiguracji serwera i wskazowki dotycz. najczesciej wystepujacych problemow zw. z instalacja / 
uzyciem Symfony2.

Pakiet podstawowy zostal tak skonstruowany aby mozliwie najszybciej uzyskac gotowosc Frameworka do pracy bez wykonywania 
standardowych czynnosci.

Wszystkie omawiane w instrukcji czynnosci i polecenia byly wykonywane na systemie *nixowym.



Wymagania
---------

 * zainstalowany serwer Apache 2.2 + PHP 5.3+ + MySQL 5.x ( zalecam pakiet LAMP ) :: patrz 
   [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

 * zainstalowany pakiet GIT - system kontroli wersji :: instalujemy poleceniem w terminalu

        sudo apt-get install git

 * zainstalowana biblioteka curl

        sudo apt-get install curl
            
            
Instalacja przy uzyciu Composer'a
---------------------------------

    *`UWAGA: mozesz pominac te sekcje, jezeli zrobiles to w poprzedniej instalacji pakietu symfony2.2-starter`*


 1. Pobieramy i instalujemy system zarządzania zależnościami Composer ( np. w katalogu www: `/var/www/` )
    
        cd /var/www/
        curl -s https://getcomposer.org/installer | php

    *`UWAGA: jezeli nie posiadasz uprawnien do operacji na danych w katalogach poza Twoim katalogiem domowym 
      np. /home/nazwa_uzytkownika/, wowczas kazda komende musisz poprzedzic poleceniem "sudo": `*

        sudo curl -s https://getcomposer.org/installer | sudo php

    .. todo: wspomniec o zasadach bezpieczenstwa i instalacji w katalogu domowym
 
 2. Generujemy katalog na projekty Symfony2 przy pomocy Composera

        php composer.phar create-project enetwiz/symfony2.2-starter /var/www/sf2-2projects --stability=dev

    Na pytanie instalatora > "Do you want to remove the exisitng VCS (.git, .svn.)" odpowiedz twierdzaco. Dzieki temu 
    pozbedziesz sie zbednego katalogu '.git'.

    .. todo: dopisz informacje o modyfikacji composer.json



Konfiguracja serwera
--------------------

 *`UWAGA: mozesz pominac te sekcje, jezeli zrobiles to w poprzedniej instalacji pakietu symfony2.2-starter`*

Podstawa do uruchomienia projektu Symfony 2.2 jest odpowiednia konfiguracja serwera. Koniecznie nalezy wlaczyc modul 
`rewrite` ( umozliwi nam poprawne mapowanie adresow ). Nalezy rowniez dokonac zmian w konfiguracyjnym `PHP.ini`. 
Niezbedna moze okazac sie rowniez [konfiguracja wirtualnych hostow](#konfiguracja-virtualhost) ( `<VirtualHost>` ).


**Konfiguracja PHP**

Uruchom adres 
[http://localhost/sf2-2projects/project1/web/config.php](http://localhost/sf2-2projects/project1/web/config.php) 
w przegladarce aby zidentyfikowac typowe problemy konfiguracyjne.
W tym momencie powinienes rozwiazac wszystkie bledy z sekcji **Major problems** - bez wykonania tego kroku aplikacja SF2 
najprawdopodobniej nie bedzie dzialac poprawnie.


**Instalacja rozszerzenia "intl" (internacjonalizacja)**
 
Mimo, że rozszerzenie `intl` nie nalezy do modułów wymaganych nalezy rowniez je zainstalowac w Twojej wersji PHP, 
poniewaz bez niego *NIE zadziała* pakiet `SonataUserBundle`. Aby zainstalować to rozszerzenie wydaj w konsoli polecenie:

        sudo apt-get install php5-intl


**Wlaczanie modulu rewrite (mod_rewrite)**

W wiekszosci podstawowych konfiguracji serwera modul przekierowan (rewrite) jest domyslnie wylaczony. Wpisz zatem w 
terminalu:

        sudo a2enmod rewrite
        sudo service apache2 restart



Tworzenie nowego projektu / aplikacji
-------------------------------------

TODO: opisz


Aplikacje i system Bundle'i
---------------------------

TODO: opisac jak to jest z kilkoma aplikacjami projaktami



Konfiguracja VirtualHost
------------------------

TODO: dokoncz - mozna to wyodrebnic do innej sekcji bo virtuale definiujemy za kazdym razem


Composer - manager pakietow
---------------------------

Do projektu zostal automatycznie dolaczony manager pakietow, ktory pozwala na sprawne dolaczanie bundle'i wraz z 
pakietami zaleznymi do naszego projektu. Wiecej informacji o tym jak uzywac Composera znajdziesz 
[TUTAJ](http://knplabs.pl/blog/skorzystaj-z-composera-ze-co-ze-jak)

    UWAGA: Znany jest blad zw. z ustawieniem timezone w php.ini, ktory wystepuje TYLKO w terminalu przy wywolaniu 
    polecen Composer'a. Blad to: "Warning: date_default_timezone_get(): It is not safe to rely on the system's 
    timezone settings" - rozwiazanie: https://github.com/Seldaek/monolog/pull/121#issuecomment-10328515

TODO: opisz problem z bledem: [RuntimeException] Failed to clone
TODO: napisz o szybkiej instalacji pakietow z packagist: php composer.phar require sonata-project/admin-bundle
TODO: napisz o wyrzucaniu .git i gitignore


Less
----

Z uwagi na to ze domyslnie dolaczana paczka tj. `TwitterBoostrap` posiada pliki zgodne z LESS ( 
[więcej o LESS](http://ciembor.github.com/lesscss.org/) ) zalecam zainstalowanie kompilatora plikow LESS tj. `Nodejs` 
na maszynie developerskiej. Dzieki Nodejs uzyskamy niesamowita latwosc w zmianie roznych wartosci domyslnych styli od 
TwitterBootstrap ( nareszcie koniec z nadpisywaniem styli domyslnych TB! ). Aby zainstalowac Nodejs nalezy wydac 
ponizsze polecenia w konsoli:

	sudo apt-get install npm
	sudo npm install -g less

Co wazne kompilator Nodejs jest ustawiony domyslnie w konfiguracji pakietu Assetic ( patrz 
`nowy_projekt/app/config/config.yml` > sekcja: # Assetic Configuration > filters ) dzieki czemu kazdorazowe wywolanie 
komendy: `php app/console assetic:dump --env=prod --no-debug` przepusci wszystkie pliki bootstrapa (CSS, JS) przez ww 
kompilator.


Zarządzanie użytkownikami
-------------------------
TODO: app/console doctrine:schema:update --force
TODO: app/console fos:user:create --super-admin


Znane problemy
--------------
TODO: linki symboliczne (dowiazania) i windows


TODO: zdefiniuj licencje; wymien licencje poszczeglnych paczek

TODO: composer.json - warto pododawac jakies stabilne wersje bo ciagnie paczki spoza cache i jest wolniej
