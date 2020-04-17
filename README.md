# custom_view
Custom View implemented through button, radio button and checkbox

#activity_main.xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"

    tools:context=".MainActivity">


   <TextView
       android:id="@+id/text"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_marginTop="12sp"

       android:layout_gravity="center"
       android:gravity="center"


       android:text="Vote Up!"
       android:textSize="50sp" />

   <TextView
       android:id="@+id/textView1"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Gender"
       android:textSize="30sp"
       android:layout_gravity="center"
       android:gravity="center"/>
   <RadioGroup
       android:layout_width="match_parent"
       android:layout_height="wrap_content">

   <RadioButton
       android:id="@+id/rd"
       android:text="Female"
       android:layout_height="wrap_content"
       android:layout_width="wrap_content"
       />

   <RadioButton
       android:id="@+id/radioButton"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Male" />

   <RadioButton
       android:id="@+id/radioButton2"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Other" />
   </RadioGroup>

   <TextView
       android:id="@+id/textView"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Age"
       android:textSize="30sp"
       android:layout_gravity="center"
       android:gravity="center"/>

   <CheckBox
       android:id="@+id/checkBox"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Above 18" />

   <CheckBox
       android:id="@+id/checkBox2"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Below 18" />

   <Button
       android:id="@+id/button"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Check"
       android:layout_marginTop="15sp"
       />

   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/ref"
       android:text="Refresh"/>
   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:visibility="invisible"
       android:textSize="30sp"
       android:id="@+id/txt_v"
       android:text="Allowed"/>


</LinearLayout>



#MainActitvity.java

package com.example.customview_11702333;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.RadioButton;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    Button check, ref;
    TextView txt;
    CheckBox ck1,ck2;
    RadioButton f,m,o;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        check = (Button)findViewById(R.id.button);
        ref = (Button)findViewById(R.id.ref);
        ck1 = (CheckBox)findViewById(R.id.checkBox);
        ck2=(CheckBox)findViewById(R.id.checkBox2);
        txt = (TextView)findViewById(R.id.txt_v);
        ref.setVisibility(View.INVISIBLE);
        f= (RadioButton)findViewById(R.id.rd);
        m = (RadioButton)findViewById(R.id.radioButton);
        o = (RadioButton)findViewById(R.id.radioButton2);

        check.setOnClickListener(new View.OnClickListener()
        {
            @Override
            public void onClick(View v) {
                if(ck1.isChecked())
                {
                    ck1.toggle();
                    txt.setVisibility(View.VISIBLE);
                    ref.setVisibility(View.VISIBLE);

                    ref.setOnClickListener(new View.OnClickListener() {
                        @Override
                        public void onClick(View v) {
                            ck1.setSelected(false);
                            ck2.setSelected(false);
                            f.setChecked(false);
                            m.setChecked(false);
                            o.setChecked(false);
                            txt.setVisibility(View.INVISIBLE);
                        }
                    });
                }
                if(ck2.isChecked())
                {
                    ck2.toggle();
                    ref.setVisibility(View.VISIBLE);
                    ref.setOnClickListener(new View.OnClickListener() {
                        @Override
                        public void onClick(View v) {
                            ck1.setSelected(false);
                            ck2.setSelected(false);
                            f.setChecked(false);
                            m.setChecked(false);
                            o.setChecked(false);
                            txt.setVisibility(View.INVISIBLE);
                        }
                    });
                }
            }
        });
    }

}


#custom_button.java

package com.example.customview_11702333;

import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Color;
import android.util.AttributeSet;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.RadioButton;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.widget.AppCompatButton;
import androidx.core.content.res.ResourcesCompat;

public class custom_button extends AppCompatButton {
    private Boolean setColor;
    private String setText;
    Button check, ref;
    TextView txt;
    CheckBox ck1, ck2;
    RadioButton f, m, o;

    public custom_button(Context context) {
        super(context);
    }

    public custom_button(Context context, AttributeSet attrs) {
        super(context, attrs);
        TypedArray typedArray = context.obtainStyledAttributes(R.styleable.ButtonCustom);

        try {
            setText = typedArray.getString(R.styleable.ButtonCustom_setTitle);
            if (setText == null) {
                setText("Custom Button");

            } else {
                setText("Remove");
                setColor = typedArray.getBoolean(R.styleable.ButtonCustom_setColor, false);
                if (setColor == true)
                    setTextColor(Color.MAGENTA);
            }
        } finally {
            typedArray.recycle();
            init();
        }
    }


    public custom_button(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    void init() {


    }
}




#radio_button.java

package com.example.customview_11702333;

import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Color;
import android.util.AttributeSet;
import android.widget.RadioButton;

import androidx.appcompat.widget.AppCompatRadioButton;

public class radio_button extends AppCompatRadioButton {

    private Boolean setColor;
    RadioButton f,m,o;
    private String setText;
    public radio_button(Context context) {
        super(context);
    }

    public radio_button(Context context, AttributeSet attrs) {
        super(context, attrs);
        TypedArray typedArray = context.obtainStyledAttributes(R.styleable.RadioCustom);

        try {
            setText = typedArray.getString(R.styleable.RadioCustom_setTitle1);
            if (setText == null) {
                setText("Custom Button");

            }
            else{
                setText("Remove");
                setColor = typedArray.getBoolean(R.styleable.RadioCustom_setColor1,false);
                if (setColor == true)
                    setTextColor(Color.MAGENTA);
            }
        }finally {
            typedArray.recycle();
            init();
        }
    }

    public radio_button(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    void init()
    {
        f= (RadioButton)findViewById(R.id.rd);
        m = (RadioButton)findViewById(R.id.radioButton);
        o = (RadioButton)findViewById(R.id.radioButton2);


        if(f.isChecked())
        {
           setText("Female");
        }

        if(m.isChecked())
        {
            setText("Male");
        }
        if(o.isChecked())
        {
            setText("Others");
        }
    }
}



#checkbox.java

package com.example.customview_11702333;

import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Color;
import android.util.AttributeSet;
import android.widget.CheckBox;
import android.widget.RadioButton;

import androidx.appcompat.widget.AppCompatCheckBox;

public class checkbox extends AppCompatCheckBox {

    private Boolean setColor;
    CheckBox ck1, ck2;
    private String setText;
    public checkbox(Context context) {
        super(context);
    }

    public checkbox(Context context, AttributeSet attrs) {
        super(context, attrs);
        TypedArray typedArray = context.obtainStyledAttributes(R.styleable.CheckBoxCustom);

        try {
            setText = typedArray.getString(R.styleable.CheckBoxCustom_setTitle2);
            if (setText == null) {
                setText("Custom Button");

            }
            else{
                setText("Remove");
                setColor = typedArray.getBoolean(R.styleable.CheckBoxCustom_setColor2,false);
                if (setColor == true)
                    setTextColor(Color.MAGENTA);
            }
        }finally {
            typedArray.recycle();
            init();
        }
    }

    public checkbox(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    void init()
    {
        ck1 = (CheckBox)findViewById(R.id.checkBox);
        ck2 = (CheckBox)findViewById(R.id.checkBox2);

        if(ck1.isChecked())
        {
            setText("Above 18");
        }
        if(ck2.isChecked())
        {
            setText("Below 18");
        }
    }
}


#custom_button.xml

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="ButtonCustom">
        <attr name="setColor" format="boolean"/>
        <attr name="setTitle" format="string"/>
    </declare-styleable>
</resources>



#custom_radio_button.xml

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="RadioCustom">
        <attr name="setColor1" format="boolean"/>
        <attr name="setTitle1" format="string"/>
    </declare-styleable>
</resources>

#custom_checkbox.xml

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="CheckBoxCustom">
        <attr name="setColor2" format="boolean"/>
        <attr name="setTitle2" format="string"/>
    </declare-styleable>
</resources>

