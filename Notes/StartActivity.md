### Запуск Activity

activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="Привет, Андроид!"
        android:layout_weight="1"
        android:scrollbars="vertical"
        android:gravity="center"
        />

    <Button
        android:id="@+id/button1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Нажми меня!"
        android:onClick="button_click"
        />

    <Button
        android:id="@+id/startButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Запустить"
        android:onClick="start_activity"
        />

    <Button
        android:id="@+id/stopButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Стоп машина!"
        android:onClick="stop_the_machine"
        />

</LinearLayout>
```

activity_second.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SecondActivity">

    <TextView
        android:id="@+id/connectionText"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="Тут какое-то сообщение"
        android:layout_margin="2dp"
        android:layout_weight="1"
        android:textColor="@color/blackColor"
        android:background="@color/whiteColor"
        android:scrollbars="vertical"
        android:scrollbarSize="3dp"
        android:scrollbarAlwaysDrawVerticalTrack="true"
        />

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Закрыть нафиг"
        android:onClick="close_the_activity"
        />

</LinearLayout>
```

MainActivity.java

```java
package com.example.amiro.firstapplication;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends Activity {

    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView1);
    }

    public void button_click(View view) {
        textView.setText("Нажали кнопку");
    }

    public void stop_the_machine(View view) {
        finish();
        System.exit(0);
    }

    public void start_activity(View view) {
        Intent intent = new Intent(this, SecondActivity.class);
        startActivity(intent);
    }
}
```

SecondActivity.java

```java
package com.example.amiro.firstapplication;

import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import java.util.concurrent.ExecutionException;

public class SecondActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        
        // Some code here
    }
}
```