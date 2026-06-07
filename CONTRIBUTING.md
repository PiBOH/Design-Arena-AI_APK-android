#### il nome originale di questo file era "BUILDARE-APK+TESTARE-APP-SU-PC.md" ora è rinominato in "CONTRIBUTING.md" per far si che vengaa visto in fianco al "README.md"

#  COME BUILDARE L'APK 



##  **PREREQUISITI (installa prima di tutto il resto)**


  1. [Node.js 20+](https://nodejs.org)  →  scarica la versione LTS

  2. [Java JDK 21](https://adoptium.net)  →  scarica "Temurin 21 LTS"
     Durante l'installazione spunta:
       ✔ Set JAVA_HOME variable
       ✔ Add to PATH

  3. Android SDK (senza Android Studio)
     https://developer.android.com/studio#command-line-tools-only
     Scarica solo "[Command line tools only](https://developer.android.com/studio#command-line-tools-only)" per Windows.


```
fai questi passaggi solo se non dovesse funzionare

     Poi esegui in PowerShell (adatta il percorso):
       mkdir C:\Android\cmdline-tools\latest
       # estrai il contenuto dello zip dentro quella cartella

     Poi aggiungi queste variabili d'ambiente di sistema:
       ANDROID_HOME = C:\Android
       Aggiungi al PATH:
         C:\Android\cmdline-tools\latest\bin
         C:\Android\platform-tools

     Poi installa i pacchetti SDK:
       sdkmanager "platform-tools"
       sdkmanager "platforms;android-34"
       sdkmanager "build-tools;34.0.0"
       sdkmanager --licenses   ← accetta tutte le licenze
```

***
##  **BUILD APK**

  Dalla ROOT del progetto in PowerShell:

    npm install
    npm run build
    npx cap sync android
    cd android
    .\gradlew.bat assembleDebug
    cd ..

###  **DOVE SI TROVA L'APK**

  android\app\build\outputs\apk\debug\app-debug.apk  
  
***

##  **ERRORI COMUNI E SOLUZIONI**


  ✖ '.\gradlew' non riconosciuto
    → Usa SEMPRE ``.\gradlew.bat``  (non .\gradlew)
      .\gradlew è uno script Linux, non funziona su Windows.

  ✖ JAVA_HOME non impostato / java non trovato
    → Reinstalla JDK 21 da adoptium.net
      Spunta "Set JAVA_HOME" durante l'installazione.
      Poi riavvia PowerShell.

  ✖ SDK location not found / ANDROID_HOME mancante
    → Imposta la variabile d'ambiente:
      ``ANDROID_HOME = C:\Android``   (o dove hai installato l'SDK)
      Riavvia PowerShell dopo averla impostata.

  ✖ "License for package not accepted"
    → Esegui:  ``sdkmanager --licenses``
      Digita "`y`" a tutte le domande.

  ✖ Build fallita con errori Gradle generici
    → Prova a pulire e ricompilare:
      ``.\gradlew.bat clean assembleDebug``


##  **TESTARE L'APP NEL BROWSER (senza buildare l'APK)**

  Remove-Item -Recurse -Force node_modules
  Remove-Item package-lock.json
  npm install
  npm run dev

  Poi apri il browser su:  [http://localhost:5173/](http://localhost:5173/)


***
***

*Se dopo avere letto queste belle istruzioni che ho scritto con impegno non hai ancora capito niente ti consiglio di chiedere all' intelligenza artificiale Claude (By antropich)*
