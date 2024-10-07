# U1Comptadors

## Block 1. Activitats sobre el comptador

### Anàlisi de l'estructura del projecte

**Comenta el tipus de projecte, quina estructura té (pots incloure captures de pantalla), i quins són els fitxers i carpetes més importants.**

Els projectes d'Android utilitzen Gradle per a crear i estructurar els projectes.
Els projectes s'estructuren en mòduls, on s'organitzen els main i els xml que modificarem per a fer els que ens demana l'activitat.

1. Dins del projecte podem destacar la carpeta Kotlin-java on es troben els dos main:
	-El MainActivity és on indiquem les ordres que han de seguir els botons, on afegirems els que ens demana.
	-El MostraComptadorActivity és l'encarregat de guardar els estats de les activitats i invocar les vistes.

2. També destacarem el layout que és on es troben els dos xml que modificarem per afegir els botons:
	-El activity_main.xml és la primera pantalla que ens apareix on afegirem els botons de sumar i resetejar el comptador.
	-El activity_mostra_comptador.xml és la pantalla que apareix quan apretem el botó Open activity.

**Analitza l'estructura d'una Activitat i quins fitxers estan implicats.**

Una activitat és un esdeveniment en l'aplicació, per exemple en el nostre codi seria fer un canvi en el comptador.
En el cas de la nostra activita per exemple quan canviem el comptador i girem la pantalla perdiem l'estat de l'activitat, la qual s'ens demana
modificar el codi per mantindre-la. Hem d'utilitzar les funcions "onSaveInstanceState" i "onRestoreInstanceState", la primera s'ocupa de guardar
l'estat de l'activitat i la segona de restaurar-lo. 

```
	override fun onSaveInstanceState(estat: Bundle) {
 		super.onSaveInstanceState(estat)
 		estat.putInt("CLAU", valor)
	}

	override fun onRestoreInstanceState(estat: Bundle) {
		 super.onRestoreInstanceState(estat)
		 valor=estat.getInt("CLAU")
	}
```

El fitxer implicat es el "MainActivity" que és on afegim les dos funcions anteriors per a que quan girem la pantalla guarde l'estat de l'activitat.

### Modificacions inicials

Com hem dit abans per afegir els botons de resetejar i restar hem afegit en el "MainAtivity.kt" les funcionalitats dels botons i en el "activity_main.xml" 
hem afegit la vista dels botons.

### Activitats sobre el cicle de vida i la pèrdua d'estat

Una vegada afegides les funcions com fem en aquesta:

	override fun onStart() {
	    super.onStart()
		 Log.d(TAG, "Al mètode onStart") // TAG és una etiqueta prèviament definida
	}

Si mirem el logcat podem observar en els logs com l'aplicació passa per tots els estats quan l'executes.
En quant al mal funcionament de pèrdua de l'estat ja ho he comentat en la pregunta "d'Analitza l'estructura d'una Activitat i quins fitxers estan implicats".

### Intents entre activitats 

El que es demana en aquesta activitat ja està implementada en el codi que tenim de base. És aquesta funció la que ho fa:

```
	 val btBack=findViewById<Button>(R.id.btBack)
		btBack.setOnClickListener {
   			 finish()
		 }
```
 
**Questió: Per crear una nova activitat, seria suficient amb crear el fitxer XML amb el layout i el fitxer Kotlin amb el codi per gestionar-la?**

Per a crear l'activita no seria suficient sols amb crear l'XML i el Kotlin, també hi hauria que afegir el fitxer Kotlin a l'AndroidManifest.xml

## Bloc 2. Comptador amb MVVM

**En quant a afegir els nous botons es pràcticament el mateix que en el primer comptador, hem de afegir la vista en el layout i afegir les funcionalitats i** 
**definir els botons en el main. La diferència es que no es necessari afegir les funcions per a guardar i restablir l'estat de l'activitat.**
**Per tal de mostrar el valor del comptador en l'activitat MostraComptadorActivity, creem una Intent i li afegim com a paràmetre el valor del comptador del ViewModel.**
**Amb l'arquitectura MVVM, aquest seguiria sent necessari? No podem llançar la Intent sense proporcionar cap argument? Si modifiquem la segona activitat per a que faça**
**ús també del ViewModel, no podriem accedir directament al valor? Investiga sobre aquesta possibilitat.**

La resposta seria que no es necessari mitjançant un Intent ja que el comptador de les activitats comparteixen el mateix view model. Si que podem llançar un Intent 
sense arguments al compartir el view model. Aquesta és la ventaja de MVVM, que compartint view model podriem també modificar la segona activita i accedir directament al valor 
a més de mantindre l'estat. 

## Bloc 3. Comptador amb Compose

En quant al Compose podem destacar que és el mes senzill. Simplement afegint els botons i la funcionalitat d'aquests en el main ja els afegeix i els mostra.
Simplement hem tingut que afegir la funció Row per a poder organitzar els botons en una fila.
