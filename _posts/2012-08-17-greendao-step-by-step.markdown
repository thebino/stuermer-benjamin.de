---
layout: post
title: "GreenDAO step by step"
date: 2012-08-17 23:06:23 +0200
comments: false
sharing: false
categories: Android
---
In diesem Artikel werde ich nicht auf die Vorteile, Performance oder Größe des ORM Mappers eingehen. Lediglich eine kurze Beschreibung, welche Schritte durchgeführt werden müssen um GreenDAO verwenden zu können.


<h2>1. Erstellen des Generator Projekts</h2>
<br />
![image-title-here](/images/posts/2012-08-17_Generatorcreate.jpg){:class="img-responsive"}

Erstellen Sie in Eclipse ein neues JAVA Projekt, am besten geben Sie diesem den Namen ihres Projekts, und hängen “Generator” dahinter.
Dadurch haben Sie die zugehörigen Projekte immer beisammen.

 <!-- more -->


<h2>2. Importieren der Librarys</h2>
<br />
![image-title-here](/images/posts/2012-08-17_Generatorimport.jpg){:class="img-responsive"}

Erstellen Sie im Generator Projekt ein Verzeichnis “libs”. Dorthinein importieren Sie

<li>freemarker.jar
<li>greenDAO-generator-javadoc.jar
<li>greenDAO-generator.jar
Bei häufigerer Verwendung von GreenDAO empfiehlt es sich, die Bibliotheken mit Hilfe des Classpath in Eclipse einzubinden. Dadurch kann dieser Schritt zukünftig ausgelassen werden.
 

<h2>3. Library in Projekt einbinden</h2>
<br />
Über die Proejekt Einstellungen fügen Sie die eben importierten Librarys dem Projekt hinzu.

![image-title-here](/images/posts/2012-08-17_Generatorjar.jpg){:class="img-responsive"}
<br />

<h2>4. Erstellen des Metamodell</h2>
<br />
{% highlight java %}
package de.stuermerbenjamin.samplegenerator;
 
import java.io.IOException;
 
import de.greenrobot.daogenerator.DaoGenerator;
import de.greenrobot.daogenerator.Entity;
import de.greenrobot.daogenerator.Schema;
 
public class Samplegenerator {
    public static void main(String[] args) {
        Schema schema = new Schema(1, "de.stuermerbenjamin.samplegenerator");
        Entity note = schema.addEntity("Note");
        note.addIdProperty();
        note.addStringProperty("text").notNull();
        note.addDateProperty("date");
        try {
            new DaoGenerator().generateAll(schema, "../Sample/src-gen");
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
{% endhighlight %}
<br />

<h2>5. Codegenerierung</h2>
<br />
Nun generiert uns GreenDAO aus dem eben erstellten Code unsere DAO Objekte.

![image-title-here](/images/posts/2012-08-17_GeneratorRun.jpg){:class="img-responsive"}
<br />
![image-title-here](/images/posts/2012-08-17_GeneratorConsole1.jpg){:class="img-responsive"}
<br />


<h1>Arbeiten mit DAO Objekten</h1>
<br /><br />


<h2>1. Android Projekt anlegen</h2>
<br />
Erstellen Sie ein neues Android Application Project mit ihren gewünschten Einstellungen.

Fügen Sie dem Projekt ein Verzeichnis mit der Bezeichnung “src-gen” hinzu. Hier werden vom Generator Projekt die Generierten DAO Objekte gespeichert.

 

<h2>2. Library hinzufügen</h2>
<br />
Für die Verwendung von greenDAO fügen Sie die library “greenDAO.jar” dem Projekt hinzu und geben das Verzeichnis “src-gen” dem Build Path mit.

 

<h2>3. Mit DAO Objekten arbeiten</h2>
<br />
 

{% highlight java %}

package de.stuermerbenjamin.sample;
 
import java.util.Date;
 
import android.app.Activity;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.util.Log;
import android.view.Menu;
import de.stuermerbenjamin.samplegenerator.DaoMaster;
import de.stuermerbenjamin.samplegenerator.DaoMaster.DevOpenHelper;
import de.stuermerbenjamin.samplegenerator.DaoSession;
import de.stuermerbenjamin.samplegenerator.Note;
import de.stuermerbenjamin.samplegenerator.NoteDao;
 
public class MainActivity extends Activity {
    private String TAG = "SampleGenerator";
    private SQLiteDatabase db;
    private DevOpenHelper helper;
    private DaoSession daoSession;
    private DaoMaster daoMaster;
    private NoteDao noteDao;
 
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
 
        helper = new DaoMaster.DevOpenHelper(this, "notes-db", null);
        db = helper.getWritableDatabase();
        daoMaster = new DaoMaster(db);
        daoSession = daoMaster.newSession();
        noteDao = daoSession.getNoteDao();
 
        // Note einfügen
        Note note = new Note(null, "Nachricht", new Date());
        noteDao.insert(note);
        Log.d(TAG, "Inserted new note, ID: " + note.getId());
 
        // Note bearbeiten
        Note note1 = new Note((long) 1, "Nachricht1", new Date());
        Log.d(TAG, "Note updated, ID: " + note1.getId());
        noteDao.update(note1);
 
        // Note löschen
        Log.d(TAG, "Deleted note with ID: " + note.getId());
        noteDao.deleteByKey(note.getId());
 
        setContentView(R.layout.activity_main);
    }
 
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.activity_main, menu);
        return true;
    }
}
{% endhighlight %}



Weitere Informatioen finden sich in der Offiziellen Dokumentation