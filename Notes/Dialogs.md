### Диалоги

activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="5dp"
        android:text="Hello World!"
        android:layout_weight="1"
        />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="5dp"
        android:text="Second text"
        android:layout_weight="1"
        />

    <Button
        android:id="@+id/chooseButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Press me"
        />

    <Button
        android:id="@+id/closeButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Close the app"
        />

</LinearLayout>
```

choose_book.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    >

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        />

    <Button
        android:id="@+id/cancelButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Cancel"
        />

</LinearLayout>
```

MainActivity.java

```java
package com.example.amiro.dialogapp;

import android.app.Activity;
import android.app.Dialog;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.ListView;
import android.widget.TextView;

public class MainActivity extends Activity {

    private TextView textView;
    private TextView textView2;
    private Button chooseButton;
    private Button closeButton;
    private Dialog dialog;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        textView2 = findViewById(R.id.textView2);
        chooseButton = findViewById(R.id.chooseButton);
        chooseButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                showDialog();
            }
        });
        closeButton = findViewById(R.id.closeButton);
        closeButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish();
                System.exit(0);
            }
        });
    }

    private void showDialog() {
        dialog = new Dialog(this);
        dialog.setCancelable(false);
        dialog.setTitle("Выберите экземпляр");
        dialog.setContentView(R.layout.choose_book);
        final ListView listView = dialog.findViewById(R.id.listView);
        final String[] numbers = new String[] { "111111", "222222",
            "333333", "444444", "555555", "666666", "777777",
            "888888", "999999", "000000", "AAAAAA", "BBBBBB",
            "CCCCCC" };
        ArrayAdapter<String> adapter = new ArrayAdapter<>(
            this, android.R.layout.simple_list_item_1,
            numbers);
        listView.setAdapter(adapter);
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                String selected = numbers[position];
                textView.setText(selected);
                dialog.dismiss();
            }
        });
        Button cancelButton = dialog.findViewById(R.id.cancelButton);
        cancelButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                textView.setText("Отменено");
                dialog.dismiss();
            }
        });
        dialog.show();
        textView2.setText(textView.getText());
    }
}
```