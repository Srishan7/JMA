# JMA
Programs-4
    Button pickbtn;
    Timer myTimer;
    WallpaperManager wpm;
    int prev=1;
    Drawable drawable;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        myTimer = new Timer();
        wpm = WallpaperManager.getInstance(this);
        pickbtn = findViewById(R.id.button);

        pickbtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                setWallpaper();
            }
        });
    }

    private void setWallpaper() {
        myTimer.schedule(new TimerTask() {
            @Override
            public void run() {
                if(prev==1) {
                    drawable = getResources().getDrawable(R.drawable.one);
                    prev=2;
                }
                else if(prev==2) {
                    drawable = getResources().getDrawable(R.drawable.two);
                    prev=3;
                }
                else if(prev==3) {
                    drawable = getResources().getDrawable(R.drawable.three);
                    prev=4;
                }
                else if(prev==4) {
                    drawable = getResources().getDrawable(R.drawable.four);
                    prev=5;
                }
                else if(prev==5) {
                    drawable = getResources().getDrawable(R.drawable.five);
                    prev=1;
                }
                Bitmap wallpaper = ((BitmapDrawable)drawable).getBitmap();
                try {
                    wpm.setBitmap(wallpaper);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,3000);
    }
}



Program 5

    TextView counterView;
    Button startBtn, stopBtn;
    Handler customHandler = new Handler();
    int i=1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        counterView = findViewById(R.id.counter);
        startBtn = findViewById(R.id.start);
        stopBtn = findViewById(R.id.stop);

        startBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                customHandler.postDelayed(updateTimer, 0);
            }
        });
        stopBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                customHandler.removeCallbacks(updateTimer);
            }
        });
    }
    private final Runnable updateTimer = new Runnable() {
        @Override
        public void run() {
            counterView.setText(""+i);
            customHandler.postDelayed(this,1000);
            i=i+1;
        }
    };
}



Program 7

package com.example.project7;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.speech.tts.TextToSpeech;
import android.view.View;
import android.widget.EditText;

import java.util.Locale;

public class MainActivity extends AppCompatActivity {
    EditText input;
    TextToSpeech ts;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        input = findViewById(R.id.sentance);
        ts = new TextToSpeech(getApplicationContext(), new TextToSpeech.OnInitListener() {
            @Override
            public void onInit(int status) {
                if(status!=TextToSpeech.ERROR) {
                    ts.setLanguage(Locale.UK);
                }
            }
        });
    }
    public void convert(View view) {
        String text = input.getText().toString();
        ts.speak(text, TextToSpeech.QUEUE_FLUSH,null);
    }
}



Program 8



package com.example.project8;

import static android.icu.lang.UCharacter.GraphemeClusterBreak.V;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {
    EditText editTextPhone;
    Button clearBtn, callBtn, saveBtn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextPhone = findViewById(R.id.number);
        clearBtn = findViewById(R.id.clear);
        callBtn = findViewById(R.id.call);
        saveBtn = findViewById(R.id.save);

        clearBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                editTextPhone.setText("");
            }
        });
        callBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String phoneNumber = editTextPhone.getText().toString();
                Intent intent = new Intent(Intent.ACTION_DIAL);
                intent.setData(Uri.parse("tel:"+phoneNumber));
                startActivity(intent);
            }
        });
        saveBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String phoneNumber = editTextPhone.getText().toString();
                Intent intent = new Intent(Intent.ACTION_INSERT);
                intent.setType(ContactsContract.Contacts.CONTENT_TYPE);

                intent.putExtra(ContactsContract.Intents.Insert.PHONE,phoneNumber);
                startActivity(intent);
            }
        });
    }
        public void inputNumber(View V) {
            Button btn = (Button) V;
            String digit = btn.getText().toString();
            String phoneNumber = editTextPhone.getText().toString();
            editTextPhone.setText(phoneNumber+digit);
        }
}



Program2 
package com.example.simplecalculator;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import java.util.regex.Pattern;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    Button btnone, btntwo,btnthree,btnfour,btnfive,btnsix,btnseven,btneight,btnnine,btnzero;
    Button btnAdd, btnSub, btnMul, btnDiv;
    Button btnClear, btnEqual, btnDot;
    EditText txtResult;

       @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnone=(Button) findViewById(R.id.btn_1);
        btnone.setOnClickListener(this);

        btntwo=(Button) findViewById(R.id.btn_2);
        btntwo.setOnClickListener(this);

        btnthree=(Button) findViewById(R.id.btn_3);
        btnthree.setOnClickListener(this);

        btnfour=(Button) findViewById(R.id.btn_4);
        btnfour.setOnClickListener(this);

        btnfive=(Button) findViewById(R.id.btn_5);
        btnfive.setOnClickListener(this);

        btnsix=(Button) findViewById(R.id.btn_6);
        btnsix.setOnClickListener(this);

        btnseven=(Button) findViewById(R.id.btn_7);
        btnseven.setOnClickListener(this);

        btneight=(Button) findViewById(R.id.btn_8);
        btneight.setOnClickListener(this);

        btnnine=(Button) findViewById(R.id.btn_9);
        btnnine.setOnClickListener(this);

        btnzero=(Button) findViewById(R.id.btn_0);
        btnzero.setOnClickListener(this);

        btnAdd=(Button) findViewById(R.id.btn_plus);
        btnAdd.setOnClickListener(this);

        btnSub=(Button) findViewById(R.id.btn_minus);
        btnSub.setOnClickListener(this);

        btnMul=(Button) findViewById(R.id.btn_mul);
        btnMul.setOnClickListener(this);

        btnDiv=(Button) findViewById(R.id.btn_div);
        btnDiv.setOnClickListener(this);

        btnDot=(Button) findViewById(R.id.btn_dot);
        btnDot.setOnClickListener(this);

        btnClear=(Button) findViewById(R.id.btn_clear);
        btnClear.setOnClickListener(this);

        btnEqual=(Button) findViewById(R.id.btn_equals);
        btnEqual.setOnClickListener(this);

        txtResult=(EditText) findViewById(R.id.Edit_Txt);
        txtResult.setText("");

    }

    @Override
    public void onClick(View v) {
           if(v.equals(btnone))
               txtResult.append("1");
           if(v.equals(btntwo))
               txtResult.append("2");
           if(v.equals(btnthree))
                txtResult.append("3");
        if(v.equals(btnfour))
            txtResult.append("4");
        if(v.equals(btnfive))
            txtResult.append("5");
        if(v.equals(btnsix))
            txtResult.append("6");
        if(v.equals(btnseven))
            txtResult.append("7");
        if(v.equals(btneight))
            txtResult.append("8");
        if(v.equals(btnnine))
            txtResult.append("9");
        if(v.equals(btnzero))
            txtResult.append("0");
        if(v.equals(btnDot))
            txtResult.append(".");
        if(v.equals(btnAdd))
            txtResult.append("+");
        if(v.equals(btnSub))
            txtResult.append("-");
        if(v.equals(btnMul))
            txtResult.append("*");
        if(v.equals(btnDiv))
            txtResult.append("/");
        if(v.equals(btnClear))
            txtResult.setText("");
        if(v.equals(btnEqual))
        {
            try {
                 String data = txtResult.getText().toString();
                 if(data.contains("/")){
                     divide(data);
                 } else if(data.contains("*")){
                     multiplication(data);
                 } else if(data.contains("+")){
                     addition(data);
                 } else if(data.contains("-")){
                     subtraction(data);
                 }
            } catch(Exception e){
                displayInvalidMessage("Invalid Input");
            }
        }

    }

    private void displayInvalidMessage(String mes) {
        Toast.makeText(getBaseContext(),mes,Toast.LENGTH_LONG).show();

    }

    private void subtraction(String data) {
           String[] operands=data.split("-");
           if(operands.length==2){
               double operand1=Double.parseDouble(operands[0]);
               double operand2=Double.parseDouble(operands[1]);
               double result=operand1-operand2;
               txtResult.setText(String.valueOf(result));
           } else{
               displayInvalidMessage("Invalid Input");
           }
    }

    private void addition(String data) {
        String[] operands=data.split(Pattern.quote("+"));
        if(operands.length==2){
            double operand1=Double.parseDouble(operands[0]);
            double operand2=Double.parseDouble(operands[1]);
            double result=operand1+operand2;
            txtResult.setText(String.valueOf(result));
        } else{
            displayInvalidMessage("Invalid Input");
        }
    }

    private void multiplication(String data) {
        String[] operands=data.split(Pattern.quote("*"));
        if(operands.length==2){
            double operand1=Double.parseDouble(operands[0]);
            double operand2=Double.parseDouble(operands[1]);
            double result=operand1*operand2;
            txtResult.setText(String.valueOf(result));
        } else{
            displayInvalidMessage("Invalid Input");
        }
    }

    private void divide(String data) {
        String[] operands=data.split("/");
        if(operands.length==2){
            double operand1=Double.parseDouble(operands[0]);
            double operand2=Double.parseDouble(operands[1]);
            double result=operand1/operand2;
            txtResult.setText(String.valueOf(result));
        } else{
            displayInvalidMessage("Invalid Input");
        }
    }
}


Program 3-
Signup 

package com.example.signupandloginin;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
EditText Signup_Username, Signup_Password;
Button btnSignup;
String regularExpression="^(?=.*[A-Z])(?=.*[a-z])(?=.*\\d)(?=.*[@$!])[A-Za-z\\d@$!]{8,}$";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Signup_Username=(EditText)findViewById(R.id.txt_username);
        Signup_Password=(EditText)findViewById(R.id.txt_password);
        btnSignup=(Button)findViewById(R.id.btn_signup);
        btnSignup.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        String username=Signup_Username.getText().toString();
        String password=Signup_Password.getText().toString();
        if(validatePassword(password)){
            Toast.makeText(getBaseContext(),"Valid Password", Toast.LENGTH_LONG).show();
            Bundle bundle=new Bundle();
            bundle.putString("User",username);
            bundle.putString("Pwd",password);
            Intent it=new Intent(this,Login.class);
            it.putExtra("data",bundle);
            startActivity(it);
        } else
        {
            Toast.makeText(getBaseContext(),"Invalid Password",Toast.LENGTH_LONG).show();
        }

    }

    private boolean validatePassword(String password) {
        Pattern pattern=Pattern.compile(regularExpression);
        Matcher matcher=pattern.matcher(password);
        return matcher.matches();
    }
}


Login.java

package com.example.signupandloginin;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class Login extends AppCompatActivity implements View.OnClickListener {
    EditText LoginUsername, LoginPassword;
    Button btnLogin;
    String user, pass;
    int count=0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        LoginUsername=(EditText)findViewById(R.id.login_username);
        LoginPassword=(EditText)findViewById(R.id.login_password);
        btnLogin=(Button)findViewById(R.id.btn_login);
        btnLogin.setOnClickListener(this);
        Bundle bundle=getIntent().getBundleExtra("data");
        user=bundle.getString("User");
        pass=bundle.getString("Pwd");
    }

    @Override
    public void onClick(View v) {
        String user1=LoginUsername.getText().toString();
        String pass1=LoginPassword.getText().toString();
        if(user.equals(user1)&& pass.equals(pass1))
        {
            Toast.makeText(this,"Login Successful",Toast.LENGTH_LONG).show();

        }
        else
        {
            count++;
            if(count==3){
                btnLogin.setEnabled(false);
                Toast.makeText(this,"Failed Login Attempts",Toast.LENGTH_LONG).show();
            }
            else
            {
                Toast.makeText(this,"Login Failed" +count,Toast.LENGTH_LONG).show();
            }
        }

    }
}


