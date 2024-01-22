+++
title = "Embassy crates released and Rust stable support"
+++

The Embassy HAL, USB, networking, Bluetooth and bootloader crates have now been released to crates.io! Read on to learn about this major milestone for the Embassy project.

<!-- more -->

Following the recent releases of [embedded-hal](https://github.com/rust-embedded/embedded-hal/) crates and [Rust 1.75](https://releases.rs/docs/1.75.0/), the Embassy HALs for [Nordic nRF](https://crates.io/crates/embassy-nrf), [STM32](https://crates.io/crates/embassy-stm32) and [Raspberry Pi RP2040](https://crates.io/crates/embassy-rp) have now been released to [crates.io](https://crates.io) ([What is a HAL?](https://docs.rust-embedded.org/book/appendix/glossary.html#hal)).

This is a major milestone with contributions from a lot of people: thank you for all the contributions over the years! At the time of writing, 255 contributors have made changes to the Embassy code base in one way or the other.

The most time has probably been spent on the `embassy-stm32` STM32 HAL, which has taken a different approach than other STM32 HALs. It's built upon the [stm32-data](https://github.com/embassy-rs/stm32-data/) project, which provides machine-readable metadata about all STM32 chips. `embassy-stm32` is generated from this data for all 1400+ supported chips. This allows precise coverage of all STM32 families, quick support for newly released chips, and a unified API making it easy to port code between families and chips.

## Something for everyone

A common source of confusion is that you have to buy into the entire Embassy ecosystem to use an Embassy HAL. However, the Embassy HAL crates all support both blocking and async operation in most cases, and you can use them without any runtime, or using another runtime such as [RTIC](https://rtic.rs/2/book/en/). This way there should be very few cases where you can _not_ use Embassy in one way or the other. The existence of the [esp-hal](https://github.com/esp-rs/esp-hal) which works with the Embassy executor shows that it goes both ways.

## HAL traits

Embassy HALs implement the traits from `embedded-hal` (both blocking and async). With the release of `embedded-hal` 1.0, embedded Rust applications now have a stable API with semantic versioning that they can rely on for their applications. This improves maintainability for the applications themselves but also makes it easier to write drivers that will remain working for a long time.

## Stable compiler

Starting with Rust 1.75, Embassy can now be compiled with a stable Rust compiler. This removes a roadblock for many who have reservations against using a nightly compiler. This will also improve the situation where different crates have different compiler support and put another hurdle for compiler regressions to impact Embassy applications.

## USB

In addition to the HALs, the Embassy USB stack has also been released ([embassy-usb](https://crates.io/crates/embassy-usb) and [embassy-usb-driver](https://crates.io/crates/embassy-usb-driver)). The USB stack is a fully async USB stack that works with all the Embassy HALs. 

There are also some generic functionality in Embassy using it such as [`embassy-usb-logger`](https://crates.io/crates/embassy-usb-logger) and [`embassy-usb-dfu`](https://crates.io/crates/embassy-usb-dfu). 

## Networking

In addition to the existing `embassy-net` crate, there are now multiple network drivers released:

* [cyw43](https://crates.io/crates/cyw43) - WiFi driver for the Raspberry Pi Pico W
* [embassy-net-esp-hosted](https://crates.io/crates/embassy-net-esp-hosted)
* [embassy-net-wiznet](https://crates.io/crates/embassy-net-wiznet)
* [embassy-net-adin1110](https://crates.io/crates/embassy-net-adin1110)
* [embassy-net-enc28j60](https://crates.io/crates/embassy-net-enc28j60)
* [embassy-net-tuntap](https://crates.io/crates/embassy-net-tuntap)
* [embassy-net-ppp](https://crates.io/crates/embassy-net-ppp)

These drivers integrate ethernet and WiFi chips with the `embassy-net` networking stack (Embassy-net is an async layer on top of [smoltcp](https://crates.io/crates/smoltcp) TCP/IP stack).

## Bootloader

Embassy Boot is a lightweight bootloader supporting firmware updates in a power-fail-safe way, with trial boots and rollbacks. With the release of Embassy HALs, the chip specific libraries can also be released: `embassy-boot-nrf`, `embassy-boot-stm32` and `embassy-boot-rp`.

## `nrf-softdevice`

The [`nrf-softdevice`](https://github.com/embassy-rs/nrf-softdevice) crates provide an idiomatic Rust API wrapping Nordic's Softdevice bluetooth stack for nRF52 series microcontrollers. Together with `embassy-nrf`, you can use it to build low-power applications that act as Bluetooth Low Energy central or peripheral devices.

## The future

With all that out of the way, what is the way forward? As with all software, Embassy will still have bugs that needs fixing, new features that needs adding, so little will change in that regard. We will regularly release new versions of the crates to `crates.io` with the latest improvements and features.

Now that crates no longer need to be built from git, board support crates and anything requiring a dependency on the HAL can now also be released, and it will be interesting to see what developers will built in the coming year.

Clearly, 2024 will be the year of Rust on embedded. Help us spread the word by showing, demoing and talking about Embassy as well as Embedded Rust!

## Thanks

Thanks to the Rust Foundation for sponsoring Dario Nieuwenhuis ([@dirbaio](https://github.com/Dirbaio))'s work on Embassy through the [Fellowship grants program](https://foundation.rust-lang.org/news/announcing-the-rust-foundation-s-2023-fellows/).

Also, many thanks to all contributors to helped make this release possible!

- 28Smiles ([@28Smiles](https://github.com/28Smiles))
- 9names ([@9names](https://github.com/9names))
- Aaron Tsui ([@overheat](https://github.com/overheat))
- Adam Greig ([@adamgreig](https://github.com/adamgreig))
- Adam Rizkalla ([@ARizzo35](https://github.com/ARizzo35))
- AdinAck ([@AdinAck](https://github.com/AdinAck))
- Aidan Temple ([@aidant](https://github.com/aidant))
- Alec C ([@avlec](https://github.com/avlec))
- Aleksandr Krotov ([@AzazKamaz](https://github.com/AzazKamaz))
- Alessandro Pezzato ([@alepez](https://github.com/alepez))
- alexferro ([@alexferro](https://github.com/alexferro))
- Alex Martens ([@newAM](https://github.com/newAM))
- Alex Moon ([@alexmoon](https://github.com/alexmoon))
- Alpha3__0
- Antoine Mugnier
- Andres Hurtado Lopez
- Andres O. Vela ([@andresovela](https://github.com/andresovela))
- Andres Vahter ([@andresv](https://github.com/andresv))
- Andrew Ealovega ([@andyblarblar](https://github.com/andyblarblar))
- Ardelean Călin ([@Ardelean-Calin](https://github.com/Ardelean-Calin))
- arturkow2000 ([@arturkow2000](https://github.com/arturkow2000))
- arturkow2 ([@arturkow2](https://github.com/arturkow2))
- Aurélien Jacobs ([@aurelj](https://github.com/aurelj))
- Badr Bouslikhin ([@badrbouslikhin](https://github.com/badrbouslikhin))
- Barnaby Walters ([@barnabywalters](https://github.com/barnabywalters))
- bartekkowalski ([@bartekkowalski](https://github.com/bartekkowalski))
- Ben Gamari ([@bgamari](https://github.com/bgamari))
- Benjamin Ward ([@WardBenjamin](https://github.com/WardBenjamin))
- Ben Schattinger ([@lights0123](https://github.com/lights0123))
- Ben Simms ([@simmsb](https://github.com/simmsb))
- Ben V. Brown ([@Ralim](https://github.com/Ralim))
- Björn Quentin ([@bjoernQ](https://github.com/bjoernQ))
- Bob McWhirter ([@bobmcwhirter](https://github.com/bobmcwhirter))
- bofh ([@bofh](https://github.com/bofh))
- bors[bot] ([@bors[bot]](https://github.com/apps/bors))
- Brandon Ros ([@brandonros](https://github.com/brandonros))
- Brendon ([@Weshnaw](https://github.com/Weshnaw))
- brian horakh
- Brooks Rady ([@TheLostLambda](https://github.com/TheLostLambda))
- Caleb Jamison ([@CBJamo](https://github.com/CBJamo))
- Cameron Harris ([@ilikepi63](https://github.com/ilikepi63))
- Carlos Barrales ([@cbruiz](https://github.com/cbruiz))
- Carl St-Laurent ([@cstlaurent](https://github.com/cstlaurent))
- Catherine ([@whitequark](https://github.com/whitequark))
- chrenderle ([@chrenderle](https://github.com/chrenderle))
- Chris Price ([@chrisprice](https://github.com/chrisprice))
- Christopher Hunt ([@huntc](https://github.com/huntc))
- Christopher N. Hesse ([@raymanfx](https://github.com/raymanfx))
- Chris Zen ([@chris-zen](https://github.com/chris-zen))
- chrysn ([@chrysn](https://github.com/chrysn))
- Chuck Davis ([@ceekdee](https://github.com/ceekdee))
- Côme ([@numero-744](https://github.com/numero-744))
- Corey Schuhen
- Cristian Eigel ([@ceigel](https://github.com/ceigel))
- cumthugo ([@cumthugo](https://github.com/cumthugo))
- Daehyeok Mun ([@daehyeok](https://github.com/daehyeok))
- dalegaard ([@dalegaard](https://github.com/dalegaard))
- Daniel Berlin ([@dberlin](https://github.com/dberlin))
- Daniel Bevenius ([@danbev](https://github.com/danbev))
- Dániel Buga ([@bugadani](https://github.com/bugadani))
- Daniel Franklin ([@dzfranklin](https://github.com/dzfranklin))
- Daniel Larsen ([@daniel-larsen](https://github.com/daniel-larsen))
- Dave Hylands ([@dhylands](https://github.com/dhylands))
- David Andersen ([@dave-andersen](https://github.com/dave-andersen))
- Davide Della Giustina ([@davidedellagiustina](https://github.com/davidedellagiustina))
- David Kleingeld ([@dvdsk](https://github.com/dvdsk))
- David Lenfesty ([@davidlenfesty](https://github.com/davidlenfesty))
- David Purser ([@davidpurser](https://github.com/davidpurser))
- Derek Hageman ([@Sizurka](https://github.com/Sizurka))
- dev-guruprasath ([@dev-guruprasath](https://github.com/dev-guruprasath))
- Dietrich Beck
- Dion Dokter ([@diondokter](https://github.com/diondokter))
- Dirk Stolle ([@striezel](https://github.com/striezel))
- Dominic Clifton ([@hydra](https://github.com/hydra))
- Dominik Boehi ([@Tiwalun](https://github.com/Tiwalun))
- Dominik Sliwa ([@randomplum](https://github.com/randomplum))
- Don Reilly ([@dreilly1982](https://github.com/dreilly1982))
- dstric-aqueduct ([@dstric-aqueduct](https://github.com/dstric-aqueduct))
- Emil Fresk ([@korken89](https://github.com/korken89))
- Eric Yanush ([@ericyanush](https://github.com/ericyanush))
- exoticorn ([@exoticorn](https://github.com/exoticorn))
- eZio Pan ([@eZioPan](https://github.com/eZioPan))
- Fabian Kunze ([@fakusb](https://github.com/fakusb))
- Folkert de Vries ([@folkertdev](https://github.com/folkertdev))
- F_Punk ([@fnafnio](https://github.com/fnafnio))
- Frederik
- Frostie314159 ([@Frostie314159](https://github.com/Frostie314159))
- ftilde ([@ftilde](https://github.com/ftilde))
- Gabriel Górski ([@glaeqen](https://github.com/glaeqen))
- Gabriel Smith ([@yodaldevoid](https://github.com/yodaldevoid))
- gak ([@gak](https://github.com/gak))
- GeorgeSoton ([@georgeSoton](https://github.com/georgeSoton))
- Ghaith Oueslati ([@OueslatiGhaith](https://github.com/OueslatiGhaith))
- Glenn Dirkx ([@Juravenator](https://github.com/Juravenator))
- GrantM11235 ([@GrantM11235](https://github.com/GrantM11235))
- Guillaume MICHEL ([@guillaume-michel](https://github.com/guillaume-michel))
- Hailey Somerville ([@haileys](https://github.com/haileys))
- Hannes ([@umgefahren](https://github.com/umgefahren))
- Harry Brooke ([@ExplodingWaffle](https://github.com/ExplodingWaffle))
- Henk Oordt ([@hdoordt](https://github.com/hdoordt))
- Henrik Alsér ([@kalkyl](https://github.com/kalkyl))
- Henrik Berg ([@henrikberg](https://github.com/henrikberg))
- Ian McIntyre ([@mciantyre](https://github.com/mciantyre))
- Ilya Epifanov ([@ilya-epifanov](https://github.com/ilya-epifanov))
- Imran K ([@imrank03](https://github.com/imrank03))
- ivmarkov ([@ivmarkov](https://github.com/ivmarkov))
- Jaap Prickartz ([@jp99](https://github.com/jp99))
- Jacob Davis-Hansson ([@jakewins](https://github.com/jakewins))
- Jacob Rosenthal ([@jacobrosenthal](https://github.com/jacobrosenthal))
- Jake Swensen ([@jdswensen](https://github.com/jdswensen))
- James Munns ([@jamesmunns](https://github.com/jamesmunns))
- James Waples ([@jamwaffles](https://github.com/jamwaffles))
- jan ([@aspizu](https://github.com/aspizu))
- Jan Christoph Bernack ([@JcBernack](https://github.com/JcBernack))
- Jan Niehusmann ([@jannic](https://github.com/jannic))
- jaxter184 ([@jaxter184](https://github.com/jaxter184))
- Jeremy Fitzhardinge ([@jsgf](https://github.com/jsgf))
- Jesse Braham ([@jessebraham](https://github.com/jessebraham))
- Joakim Hulthe ([@hulthe](https://github.com/hulthe))
- johannes ([@johannesneyer](https://github.com/johannesneyer))
- Johann Tuffe ([@tafia](https://github.com/tafia))
- Jomer ([@JomerDev](https://github.com/JomerDev))
- Jonathan Dickinson ([@jcdickinson](https://github.com/jcdickinson))
- Joonas Javanainen ([@Gekkio](https://github.com/Gekkio))
- Josh Mcguigan ([@JoshMcguigan](https://github.com/JoshMcguigan))
- Joshua Salzedo ([@theunkn0wn1](https://github.com/theunkn0wn1))
- Julian ([@JuliDi](https://github.com/JuliDi))
- Jurgis ([@chemicstry](https://github.com/chemicstry))
- Justin Beaurivage ([@jbeaurivage](https://github.com/jbeaurivage))
- Kai Bleeke ([@kbleeke](https://github.com/kbleeke))
- Kaitlyn Kenwell ([@Redrield](https://github.com/Redrield))
- Kaspar Schleiser ([@kaspar030](https://github.com/kaspar030))
- Kevin Lannen ([@kevswims](https://github.com/kevswims))
- KingCol13 ([@KingCol13](https://github.com/KingCol13))
- Lachezar Lechev ([@elpiel](https://github.com/elpiel))
- Liam Murphy ([@Liamolucko](https://github.com/Liamolucko))
- Liigo Zhuang ([@liigo](https://github.com/liigo))
- Linus Harberg
- Lixou ([@DasLixou](https://github.com/DasLixou))
- Loïc Damien ([@dzamlo](https://github.com/dzamlo))
- lonesometraveler ([@lonesometraveler](https://github.com/lonesometraveler))
- loris libralato ([@lorislibralato](https://github.com/lorislibralato))
- Luca Barbato ([@lu-zero](https://github.com/lu-zero))
- Lucas Granberg ([@lucasgranberg](https://github.com/lucasgranberg))
- Lucas Kent ([@rukai](https://github.com/rukai))
- Lukas Joeressen ([@kext](https://github.com/kext))
- Lukas Krejci ([@metlos](https://github.com/metlos))
- luveti ([@luveti](https://github.com/luveti))
- m5p3nc3r ([@m5p3nc3r](https://github.com/m5p3nc3r))
- Maja Piechotka ([@uzytkownik](https://github.com/uzytkownik))
- Marco Pastrello
- Mateusz Butkiewicz ([@Mirror0](https://github.com/Mirror0))
- Mateusz ([@dragonnn](https://github.com/dragonnn))
- Mathias Koch ([@MathiasKoch](https://github.com/MathiasKoch))
- Mathieu Dupont ([@m-dupont](https://github.com/m-dupont))
- Matous Hybl ([@matoushybl](https://github.com/matoushybl))
- Matthias Devlamynck ([@mdevlamynck](https://github.com/mdevlamynck))
- mattiasgronlund ([@mattiasgronlund](https://github.com/mattiasgronlund))
- Matt Ickstadt ([@mattico](https://github.com/mattico))
- Matt Johnston ([@mkj](https://github.com/mkj))
- Max ([@mxdbck](https://github.com/mxdbck))
- mbrieske ([@mbrieske](https://github.com/mbrieske))
- Mehmet Ali Anil ([@mehmetalianil](https://github.com/mehmetalianil))
- Mia ([@miathedev](https://github.com/miathedev))
- Michael van Niekerk ([@mvniekerk](https://github.com/mvniekerk))
- Michal Srb ([@michalsrb](https://github.com/michalsrb))
- Mick van Gelderen ([@mickvangelderen](https://github.com/mickvangelderen))
- Mike Beaumont ([@michaelbeaumont](https://github.com/michaelbeaumont))
- mryndzionek ([@mryndzionek](https://github.com/mryndzionek))
- msamsonoff ([@msamsonoff](https://github.com/msamsonoff))
- Nicolas Viennot ([@nviennot](https://github.com/nviennot))
- Nigecat ([@Nigecat](https://github.com/Nigecat))
- Nils Fitinghoff ([@nilfit](https://github.com/nilfit))
- ⭐️NINIKA⭐️ ([@DCNick3](https://github.com/DCNick3))
- nitroxis ([@nitroxis](https://github.com/nitroxis))
- Oliver Rockstedt ([@sourcebox](https://github.com/sourcebox))
- Olivier Monnom ([@papyDoctor](https://github.com/papyDoctor))
- Olle Sandberg ([@oll3](https://github.com/oll3))
- olofwalker ([@olofwalker](https://github.com/olofwalker))
- Patricio Whittingslow ([@soypat](https://github.com/soypat))
- Patrick Oppenlander ([@pattop](https://github.com/pattop))
- Paweł Czochański ([@czocher](https://github.com/czocher))
- Pawel Rawski ([@itdiuna](https://github.com/itdiuna))
- pbert519 ([@pbert519](https://github.com/pbert519))
- Pedro Ferreira ([@pferreir](https://github.com/pferreir))
- pennae ([@pennae](https://github.com/pennae))
- Peter Gibson ([@petegibson](https://github.com/petegibson))
- Peter Hansen ([@peter9477](https://github.com/peter9477))
- Peter Krull ([@peterkrull](https://github.com/peterkrull))
- Philip A Reimer ([@ant32](https://github.com/ant32))
- Phil Markgraf ([@ShakenCodes](https://github.com/ShakenCodes))
- Piotr Esden-Tempski ([@esden](https://github.com/esden))
- Polly ([@FuzzyLitchi](https://github.com/FuzzyLitchi))
- Priit Laes ([@plaes](https://github.com/plaes))
- Qix ([@Qix-](https://github.com/Qix-))
- Quentin Smith ([@quentinmit](https://github.com/quentinmit))
- Rafael Bachmann ([@barafael](https://github.com/barafael))
- Ralf ([@jr-oss](https://github.com/jr-oss))
- Randipa Gunathilake ([@HelloWorldTeraByte](https://github.com/HelloWorldTeraByte))
- Rasmus Melchior Jacobsen ([@rmja](https://github.com/rmja))
- Rasmus Pedersen ([@rasmuspeders1](https://github.com/rasmuspeders1))
- René van Dorst ([@vDorst](https://github.com/vDorst))
- Richard Dodd (dodj) ([@derekdreery](https://github.com/derekdreery))
- Riley Williams ([@riley-williams](https://github.com/riley-williams))
- Robert T Dowling ([@RobertTDowling](https://github.com/RobertTDowling))
- Roman Isaikin ([@romixlab](https://github.com/romixlab))
- Roman Valls Guimera ([@brainstorm](https://github.com/brainstorm))
- Roy Buitenhuis ([@royb3](https://github.com/royb3))
- Ruben De Smet ([@rubdos](https://github.com/rubdos))
- Russ Hewgill
- Sam Lakerveld ([@darkwater](https://github.com/darkwater))
- Sam Mason ([@CaptainMaso](https://github.com/CaptainMaso))
- Samuel Čavoj ([@sammko](https://github.com/sammko))
- Samuel Tardieu ([@samueltardieu](https://github.com/samueltardieu))
- Satoshi Tanaka ([@tana](https://github.com/tana))
- sawi97 ([@sawi97](https://github.com/sawi97))
- schphil ([@schphil](https://github.com/schphil))
- Scott Mabin ([@MabezDev](https://github.com/MabezDev))
- Scott Mansell ([@phire](https://github.com/phire))
- Sebastian Goll ([@sgoll](https://github.com/sgoll))
- SekoiaTree ([@SekoiaTree](https://github.com/SekoiaTree))
- Simon Berg ([@fluffware](https://github.com/fluffware))
- Sjoerd Simons ([@sjoerdsimons](https://github.com/sjoerdsimons))
- Slushee ([@Slushee-a](https://github.com/Slushee-a))
- smeenka ([@smeenka](https://github.com/smeenka))
- sodo ([@djdisodo](https://github.com/djdisodo))
- Stephan Wolski ([@Slowki](https://github.com/Slowki))
- Swanand Mulay ([@swanandx](https://github.com/swanandx))
- swolix ([@swolix](https://github.com/swolix))
- T-Bakker ([@T-Bakker](https://github.com/T-Bakker))
- Ted Feng ([@artisdom](https://github.com/artisdom))
- Thales ([@thalesfragoso](https://github.com/thalesfragoso))
- Thierry Fleury ([@TFleury](https://github.com/TFleury))
- Thomas Shufps ([@shufps](https://github.com/shufps))
- Til Blechschmidt ([@TilBlechschmidt](https://github.com/TilBlechschmidt))
- Timo Kröger ([@timokroeger](https://github.com/timokroeger))
- Timo ([@t-moe](https://github.com/t-moe))
- Tobias Breitwieser ([@tarfu](https://github.com/tarfu))
- Tobias Pisani
- Torin Cooper-Bennun ([@tcbennun](https://github.com/tcbennun))
- Tshepang Mbambo ([@tshepang](https://github.com/tshepang))
- Tyler ([@tyler-gilbert](https://github.com/tyler-gilbert))
- Ulf Lilleengen ([@lulf](https://github.com/lulf))
- Vadim Kaushan ([@Disasm](https://github.com/Disasm))
- Val Packett ([@valpackett](https://github.com/valpackett))
- Vasanthakumar Vijayasekaran ([@VasanthakumarV](https://github.com/VasanthakumarV))
- vasilNnikolov ([@vasilNnikolov](https://github.com/vasilNnikolov))
- Vincent Stakenburg ([@FrozenDroid](https://github.com/FrozenDroid))
- Wilfried Chauveau ([@ithinuel](https://github.com/ithinuel))
- Will Farrell ([@wkf](https://github.com/wkf))
- Will Glynn ([@willglynn](https://github.com/willglynn))
- Will Yager ([@wyager](https://github.com/wyager))
- xoviat ([@xoviat](https://github.com/xoviat))
- Zoey Riordan ([@ZoeyR](https://github.com/ZoeyR))
