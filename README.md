# imageswitcher
xml file-
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    tools:context=".MainActivity">

    <ImageSwitcher
        android:id="@+id/imageSwitcher"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_above="@+id/btnNext"
        android:layout_centerInParent="true">

    </ImageSwitcher>

    <Button
        android:id="@+id/btnPrevious"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentStart="true"
        android:layout_alignParentBottom="true"
        android:layout_marginStart="16dp"
        android:layout_marginBottom="16dp"
        android:text="Previous" />

    <Button
        android:id="@+id/btnNext"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentEnd="true"
        android:layout_alignParentBottom="true"
        android:layout_marginEnd="16dp"
        android:layout_marginBottom="16dp"
        android:text="Next" />

</RelativeLayout>

javafile-
package com.example.imageswitcher;

import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.os.Bundle;
import android.widget.Button;
import android.widget.ImageSwitcher;
import android.widget.ImageView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private ImageSwitcher imageSwitcher;
    private final int[] images = {R.drawable.target, R.drawable.values, R.drawable.vision};
    private int currentIndex = 0;

    @Override
    @SuppressLint({"MissingInflatedId", "LocalSuppress"})
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imageSwitcher = findViewById(R.id.imageSwitcher);
        Button next = findViewById(R.id.btnNext);
        Button previous = findViewById(R.id.btnPrevious);

        imageSwitcher.setFactory(() -> {
            ImageView imageView = new ImageView(MainActivity.this);
            imageView.setScaleType(ImageView.ScaleType.FIT_CENTER);
            return imageView;
        });

        imageSwitcher.setImageResource(images[currentIndex]);

        previous.setOnClickListener(view -> {
            currentIndex--;
            if (currentIndex < 0) {
                currentIndex = images.length - 1;
            }
            imageSwitcher.setImageResource(images[currentIndex]);
            Toast.makeText(this,images[currentIndex], Toast.LENGTH_SHORT).show();
        });

        next.setOnClickListener(view -> {
            currentIndex++;
            if (currentIndex >= images.length) {
                currentIndex = 0;
            }
            imageSwitcher.setImageResource(images[currentIndex]);
            Toast.makeText(this,images[currentIndex], Toast.LENGTH_SHORT).show();
        });



    }
}
