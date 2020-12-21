Q: 
Was hat es mit den VB-Projekten und der Projektgruppe 
in diesem Ordner auf sich?

A:
* In diesem Ordner sind zwei VB-Projekte:
  - MBOFastGeo.vbp,
  - MBOFGbas.vbp
  und eine VB-Projektgruppe:
  - FGGroup.vbg,
  wobei die Projektgruppe die zwei oben genannten Projekte 
  enth�lt.

* (AXDll) Das VB-Projekt MBOFastGeo.vbp enth�lt den Sourcecode, 
  also alle Klassen und Module, f�r die ActiveXdll: 
  - MBOFastGeo.dll,
  die sich nach dem Kompilieren ein Verzeichnis dar�ber 
  befindet.
  im einzelnen sind das die Dateien:
  Module:
  - ModConsts.bas
  - ModDelphi.bas
  Klassenmodule:
  - FastGeo.cls (der eigentliche Grafikkern als Klasse) 
  - FGTypes.cls
  - TBaseConvexHull.cls
  - TConvexHull2D.cls
  - TOrderedPolygon2D.cls
  - TOrderedPolygon3D.cls
  > wobei die Klasse FastGeo.cls das Attribut hat:
    - Instancing: 6 - GlobalMultiUse  
    d.h. bei Verwendung der dll in einem Projekt mu� kein
    Objekt der Klasse FastGeo.cls angelegt werden, alle 
    Funktionen sind vorhanden, wie man es sonst von einem 
    Modul her gewohnt ist. Dies hat den Vorteil, da� die 
    ActiveXdll mit der bas+tlb austasuchbar ist, und 
    umgekehrt.
  > die Klasse FGTypes enth�lt alle UDTypes als Public Member 
    (dies ist nur in einer Klasse in einer ActiveXdll m�glich)
    da die Klasse FGTypes sonst keine eigene Funktionalit�t 
    besitzt, ist sie mit dem Attribut:
    - Instancing: 2 - PublicNotCreatable
    belegt.
  > die anderen Klassen m�ssen im Prinzip nicht verwendet 
    werden, da die Funktionalit�t �ber Funktionen in der 
    FastGeo.cls bereitgestellt wird. Die Klassen haben demnach
    das Attribut:
    - Instancing: 1 - Private      
  Das Projekt ben�tigt nur die obengenannten Dateien und 
  ansonsten keine Verweise oder Komponenten.
  Es sollten also keine Probleme beim Kompilieren auftreten. 

* (bas+tlb) Das VB-Projekt MBOFGbas.vbp enth�lt den Sourcecode, und
  alle Klassen die f�r die Verwendung der Grafik-Bibliothek ohne 
  die ActiveXdll gedacht ist, also zur Verwendung, als 
  einkompiliertes Modul.
  Im einzelnen sind das die Dateien:
  Module:
  - FastGeo.bas (der eigentliche Grafikkern, als Modul)
  - FGTypes.bas  
  - ModDelphi.bas
  Klassenmodule:
  - TBaseConvexHull.cls
  - TConvexHull2D.cls
  - TOrderedPolygon2D.cls
  - TOrderedPolygon3D.cls
  die letzgenannten vier Klassen und die Datei ModDelphi.bas
  sind die selben Dateien wie im Projekt MBOFastGeo.vbp.
  (deswegen liegen die Projekte im selben Verzeichnis) 
  > Achtung! Die Datei FGTypes.bas enth�lt nur ein paar 
    Funktionen und keine UD-Types, diese sind auskommentiert.
    Die UDTypes m�ssen zur Verwendung in einem Standardexe-
    projekt in eine Typelibrary ausgelagert werden.
    Das Projekt hat also einen Verweis auf die Datei 
    - TLBFastGeo.tlb
    Die Datei enth�lt alle Grafikprimitiven auf die die
    Funktionen abgestimmt sind.
    wo die tlb-Datei liegt bleibt dem Anwender selber �berlassen, 
    also in das Windows/System32 Verzeichnis kopieren oder in den 
    Programmordner oder sonstwo. Dort mu� die Datei allerdings 
    dann auch registriert werden.
    Sollten beim Start des Projektes komische Ph�nomene auftauchen,
    ein Absturz von VB gar oder sonstwas, dann liegt das vermutlich 
    daran da� die Datei nicht registriert ist.  
  
  Will man also keine dll verwenden, sondern arbeitet lieber 
  mit der einkompilierten Version, so sind diese Dateien 
  erforderlich um die komplette Funktionalit�t in einem 
  Standardexe Projekt zur Verf�gung zu haben.
  �brigens die ActiveXdll belegt ca. 600kb
  das Modul und tlb nur ein paar kb in der Exe-Datei
  
sollten noch Fragen offen bleiben?

-> Oliver Meyer 
   www.MBO-Ing.com
   oliver.meyer@mbo-ing.com
   olimilo@gmx.net        