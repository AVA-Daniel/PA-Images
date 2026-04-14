```mermaid
flowchart TB
    %% Definition der Rahmen-Stile
    classDef standard fill:#fff,stroke:#333,stroke-width:1px,color:#000;
    classDef rot fill:#fff,stroke:#ff0000,stroke-width:3px,color:#000;
    classDef blau fill:#fff,stroke:#003366,stroke-width:2px,color:#000;
    classDef green fill:#fff,stroke:#61822A,stroke-width:2px,color:#000;
    classDef gold fill:#fff,stroke:#FBB900,stroke-width:2px,color:#000;

    %% Gruppierung nach Verantwortlichkeiten (Farbbereiche)
    subgraph mHA [mHA]
        mha01(M20<br>Vertragsunterlagen<br>anfordern):::standard
    end
    style mHA fill:#7b1113,stroke:#333,stroke-width:1px,color:#fff

    subgraph mAP [mAP]
        map01("M40<br>Installateursannahme<br>(Optional)"):::gold
        map02(M40<br>Installateursannahme):::standard
        map03("M150<br>Installationsanlage fertigmelden<br>(Ab Abschluss M70 möglich)"):::standard
        map04("M151<br>Erzeugungsanlage fertigmelden<br>(Ab Abschluss M90 möglich)"):::standard
        map05("Erzeugungsanlage fertigmelden<br>(Schon ab Abschluss M90 möglich)"):::standard
    end
    style mAP fill:#179c9e,stroke:#333,stroke-width:1px,color:#fff

    subgraph mKA [mKA]
        mka01(M30<br>Vorgang generieren):::standard
        mka02(M32<br>Dokumente generieren):::standard
        mka03(M60<br>Prüfung Eingangsdaten):::standard
        mka04(M220<br>Prüfung der Netzverträglichkeit):::standard
        mka05(M70<br>Tachnische Planung):::standard
        mka06(M80<br>Dokumente erstellen):::standard
        mka07(M90<br>Dokumentenrücklauf prüfen):::standard
        mka08(M120<br>Zählerauftrag finalisieren):::standard
        mka09(M170<br>Warte auf<br>technische Erledigung):::standard
        mka10("M242<br>Eventtrigger E01<br>(Optional)"):::gold
        mka11(M242<br>Eventtrigger E05 / E03):::standard
        mka12(M230<br>Abschlussprüfung PV):::standard
        mka13(Status:<br>abgeschlossen):::standard
    end
    style mKA fill:#d4d300,stroke:#333,stroke-width:1px,color:#fff

    subgraph mHAP [mHAP]
        %% Hinweis: mha01 wird hier erneut aufgerufen, was das Node im Layout in mHAP verschieben kann.
        %% Exakt wie in der Vorlage übernommen.
        mhap01(Platzhalter):::standard
        mhap02(Platzhalter):::standard
        mhap03("M228/M229<br>Bank- & Steuerdaten /MaSTR.<br>(M151 & E01 müssen<br>abgeschlossen sein)"):::standard        
    end
    style mHAP fill:#AF8A66,stroke:#333,stroke-width:1px,color:#fff

    %% Definition der Zwischenschritte (Loops)

    zw001(["Datenübertragung HarNES (M240)"]):::green
    zw002(["Datenübertragung HarNES (M240)"]):::green
    zw003(["Datenübertragung HarNES (M240)"]):::green
    zw004(["Datenübertragung HarNES<br>(Nur bei Abschluss M151)"]):::green
    zw005(["Datenübertragung HarNES (M240)"]):::green
    zw006(["Instanz = installed oder aktiv"]):::green
    zw007(["Datenübertragung HarNES"]):::green
    zw008(["Datenübertragung HarNES (M240)<br>(nur bei Abschluss M151)"]):::green
    zw009(["Finale Datenübertragung<br>HarNES<br>(vor Eventtrigger)"]):::green
    zw010(["Datenübertragung HarNES"]):::green
    ende((Vorgang Ende))

    %% Logischer Ablauf
    mha01 --> map01
    map01 --> mka01
    mka01 --> mhap01
    mhap01 --> mka02
    mka02 --> mka03
    mka03 --> zw001
    zw001 --> mka04
    mka04 --> zw002
    zw002 --> mka05
    mka05 --> mka06
    mka06 --> zw003
    zw003 --> mka07
    mka07 --> map02
    map02 --> map03
    map03 --> map04
    map04 --> zw004
    zw004 --> mka08
    mka08 --> zw005
    zw005 --> mhap02
    mhap02 --> mka09
    mka09 --> zw006
    zw006 --> mka10
    mka10 --> zw007
    zw007 --> map05
    map05 --> zw008
    zw008 --> mhap03
    mhap03 --> zw009
    zw009 --> mka11
    mka11 --> mka12
    mka12 --> zw010
    zw010 --> mka13 
    mka13 --> ende

  ```

  Deine Mutter