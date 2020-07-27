## dialog_view.xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        >

        <EditText
            android:id="@+id/edit_text1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/rounded_box"
            android:layout_marginRight="10dp"
            android:layout_marginLeft="10dp"
            android:layout_marginBottom="5dp"
            />

        <EditText
            android:id="@+id/edit_text3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:minHeight="100dp"
            android:gravity="top"
            android:hint="@string/concreteContext"
            android:background="@drawable/rounded_box"
            android:layout_marginRight="10dp"
            android:layout_marginLeft="10dp"
            android:layout_marginBottom="5dp"
            />

        <EditText
            android:id="@+id/edit_text2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/rounded_box"
            android:layout_marginRight="10dp"
            android:layout_marginLeft="10dp"
            android:layout_marginBottom="5dp"
            />

    </LinearLayout>
