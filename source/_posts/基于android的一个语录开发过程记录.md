---
title: 基于android的一个语录开发过程记录
date: 2023-11-25 16:09:41
tags: android
---

# 开发开始

很早之前参与编写了一篇语录，大概有3W字，正好学习了android开发的一些相关知识，能否通过这个机会开发出一个app展示语录，就类似阅读器这种的。

# 尝试写第一个页面

## 刘

这一部分是关于将的介绍，那么肯定是从宇轩开始。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".family.FamilyLiuYuxuan">


    <ImageButton

        android:id="@+id/FamilyLiuYuxuanSettingButton"
        android:layout_width="40sp"
        android:layout_height="40sp"
        android:layout_alignParentTop="true"

        android:layout_alignParentRight="true"
        android:layout_marginTop="20sp"
        android:src="@mipmap/ic_launcher">

    </ImageButton>

    <ScrollView

        android:id="@+id/ScrollView"
        android:layout_width="match_parent"
        android:layout_height="550sp"
        android:layout_below="@id/FamilyLiuYuxuanSettingButton">

        <TextView

            android:id="@+id/FamilyLiuYuxuanText"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_marginLeft="40dp"
            android:layout_marginTop="0dp"
            android:layout_marginRight="40dp"
            android:text="\t\t\t\t刘宇轩(大将)女,一般称宇轩,别名SHEEN,YUEAI,妞鬼,八怪,小轩轩,刘头,宇呕,宇X(X读作lāi),夫妻,大球,(在宇呕荣耀中)大龙,李蓉泉称其为井盖脸,跟她勾肩搭背的女生称其为混世女魔头,有,圆,有和圆合称原油(由一帆创始),还有某些女生称其为老大。
            \n\t\t\t\t英文名LIGHT SHEEN(简称LS),来自一班。是戏曲里的彩旦,因为彩旦专演丑角。具有纯正的宇轩血统,是唯一的光系宇轩。长相奇丑无比,也不知道是什么原因。具有满脸痘和超亮大奔头。长相很奇特而且较黑,正面看根本看不见头发,一低头就可以看见她的发际线离眉毛很远,于是奔头就很大,而且侧面的头发也濒临消失,但她在合影的时候永远站在第一个,真够惊悚的。
            \n\t\t\t\t宇轩奔遇阳光可反射光芒,储存光芒,放光芒。但长相都是次要的,最关键她道德品质极其败坏,允许她说别人但不允许别人说她,不愧是相由心生。坐在别人椅子上,嫌人家书包硌得慌,就直接把人家的书包扔在地上。对鸡毛蒜皮不值得一提的小事斤斤计较个没完没了。初三上半学期的最后,老师发糖,宇呕就用臭爪子把糖抓来抓去,乱挑,真是恶心到家了。
            \n\t\t\t\t为了寻求保护和宠爱,经常拍老师马屁,当老师一面,背着老师一面。脾气暴,嗓门大,极其张扬。令人胆怯,闻其声而知其名,闻风丧胆,一眼都不能看,因为看完就会失明。挑拨离间女生间关系,还掐女生脖子,使得全班人都排斥她。贪污退回的饭费,一向一毛不拔的宇来还拿赃款请女生吃东西。\n\t\t\t\t著有名言:(宇轩怒之千古绝唱)“给我道歉。”
"

            ></TextView>
    </ScrollView>

    <Button
        android:id="@+id/FamilyLiuYuxuanButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/ScrollView"
        android:layout_centerHorizontal="true"
        android:text="返回"
        android:textSize="20sp" />


</RelativeLayout>
```

```java
package com.example.yuouquotation.family;

import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageButton;
import android.widget.TextView;

import com.example.yuouquotation.R;

public class FamilyLiuYuxuan extends AppCompatActivity {
    private static final int REQUEST_CODE_SETTINGS = 1;
    private Button familyLiuYuxuanButton;
    private int textSize;
    private ImageButton familyLiuYuxuanSettingButton;
    private TextView familyLiuYuxuanText;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_family_liu_yuxuan);

        familyLiuYuxuanButton = findViewById(R.id.FamilyLiuYuxuanButton);
        familyLiuYuxuanSettingButton = findViewById(R.id.FamilyLiuYuxuanSettingButton);
        familyLiuYuxuanText = findViewById(R.id.FamilyLiuYuxuanText);
        SharedPreferences sharedPreferences = getSharedPreferences("app_settings", MODE_PRIVATE);
        SharedPreferences.Editor editor = sharedPreferences.edit();
        textSize = sharedPreferences.getInt("textSize", 20);
        familyLiuYuxuanText.setTextSize(textSize);
        //返回按钮
        familyLiuYuxuanButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();
            }
        });
        //设置按钮
        familyLiuYuxuanSettingButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(FamilyLiuYuxuan.this, FamilySettings.class);
                startActivityForResult(intent, REQUEST_CODE_SETTINGS);
            }
        });


    }

    @Override
    protected void onActivityResult(int requestCode , int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE_SETTINGS && resultCode == RESULT_OK) {
            Bundle parameters = data.getExtras();
            // 使用返回的参数更新初始界面的状态
            textSize = parameters.getInt("textSize");
            familyLiuYuxuanText.setTextSize(textSize);

        }
    }
}
```

调整了布局以及按钮的逻辑，同理制作出张，伪，中将和小将的信息。

## 张

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".family.FamilyLiuYuxuan">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <ImageButton

            android:id="@+id/FamilyZhangYuxuanSettingButton"
            android:layout_width="40sp"
            android:layout_height="40sp"
            android:layout_alignParentTop="true"

            android:layout_alignParentRight="true"
            android:layout_marginTop="20sp"
            android:src="@mipmap/ic_launcher"/>
        <TextView
            android:id="@+id/FamilyZhangYuxuanText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="\t\t\t\t张雨轩(大将)
男,一般称雨轩,别名老张头,英文名BLACK SHEEN(简称BS),来自五班。\n\t\t\t\t长相比黑人还黑,屁多,屁话更多,口齿不清,满身痘痘,1厘米的屌呈尖型,长相不佳但喜欢贴近别人。看起来脸上不发光,其实张头发紫外线,会吸收(吸收紫外线用来把自己变得更黑),储存,放紫外线。\n\t\t\t\t不知羞耻 ,自称对刘时骏和赵健程有爱意。整天就挠他自己脸上的痘,长满泥的指甲长得能挠破皮。爱瞎bb,还学别人说话。从初三开始就不来了,他其实还是挺可怜的。\n\t\t\t\t著有名言:“啊哈哈。”“滚犊子。”“健程。”“小健健。“ “小京楠。”“屙,好诡异!”“若熙奶奶。”“不能那么残忍!”“别闹!”“(扶着痘说)完,完,完,完,完!”
"
            android:layout_marginLeft="40dp"
            android:layout_marginRight="40dp"
            android:layout_marginTop="20dp"
            ></TextView>


        <Button
            android:id="@+id/FamilyZhangYuxuanButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="返回"
            android:textSize="20sp"
            android:layout_below="@id/FamilyZhangYuxuanText"
            android:layout_centerHorizontal="true"/>
    </RelativeLayout>

</ScrollView>
```

```java
package com.example.yuouquotation.family;

import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageButton;
import android.widget.TextView;

import com.example.yuouquotation.R;

public class FamilyZhangYuxuan extends AppCompatActivity {


    private Button familyZhangYuxuanButton;
    private TextView familyZhangYuxuanText;
    private int textSize;
    SharedPreferences sharedPreferences;
    SharedPreferences.Editor editor;
    ImageButton familyZhangYuxuanSettingButton;
    private int REQUEST_CODE = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_family_zhang_yuxuan);

        familyZhangYuxuanButton = findViewById(R.id.FamilyZhangYuxuanButton);
        familyZhangYuxuanText = findViewById(R.id.FamilyZhangYuxuanText);
        familyZhangYuxuanSettingButton = findViewById(R.id.FamilyZhangYuxuanSettingButton);
        sharedPreferences = getSharedPreferences("app_settings", MODE_PRIVATE);
        editor = sharedPreferences.edit();
        textSize = sharedPreferences.getInt("textSize", 20);

        familyZhangYuxuanText.setTextSize(textSize);

        familyZhangYuxuanButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();
            }
        });
        familyZhangYuxuanSettingButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(FamilyZhangYuxuan.this, FamilySettings.class);
                startActivityForResult(intent, REQUEST_CODE);
            }
        });

    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE && resultCode == RESULT_OK) {
            textSize = sharedPreferences.getInt("textSize", 20);
            familyZhangYuxuanText.setTextSize(textSize);
        }
    }
}
```

## 伪

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".family.FamilyLiuYuxuan">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <ImageButton

            android:id="@+id/FamilyWeiYuxuanSettingButton"
            android:layout_width="40sp"
            android:layout_height="40sp"
            android:layout_alignParentTop="true"

            android:layout_alignParentRight="true"
            android:layout_marginTop="20sp"
            android:src="@mipmap/ic_launcher"/>
        <TextView
            android:id="@+id/FamilyWeiYuxuanText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginLeft="40dp"
            android:layout_marginTop="20dp"
            android:layout_marginRight="40dp"
            android:text="\t\t\t\t伪宇轩(大将)
女,真名刘思多,别名伪头,英文名FALSE SHEEN(简称FS),来自四班。长相剧黑无比。\n\t\t\t\t源于菊花村,远看神似张雨轩,近看半似刘宇轩,痘虽少,但也挺丑的。学习好,一帆致词:自古英雄出宇轩。(伪宇轩夫:四班口齿不清、智商低下的儿童贺铂中。思多哥:刘思宇)
"></TextView>


        <Button
            android:id="@+id/FamilyWeiYuxuanButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/FamilyWeiYuxuanText"
            android:layout_centerHorizontal="true"
            android:text="返回"
            android:textSize="20sp" />
    </RelativeLayout>

</ScrollView>
```

```java
package com.example.yuouquotation.family;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageButton;
import android.widget.TextView;

import com.example.yuouquotation.R;

public class FamilyWeiYuxuan extends AppCompatActivity {


    private Button familyWeiYuxuanButton;
    private TextView familyWeiYuxuanText;
    private int textSize;
    private ImageButton familyWeiYuxuanSettingButton;
    SharedPreferences sharedPreferences;
    SharedPreferences.Editor editor;
    private int REQUEST_CODE = 1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_family_wei_yuxuan);


        sharedPreferences = getSharedPreferences("app_settings", MODE_PRIVATE);
        editor = sharedPreferences.edit();
        textSize = sharedPreferences.getInt("textSize", 20);

        familyWeiYuxuanButton = findViewById(R.id.FamilyWeiYuxuanButton);
        familyWeiYuxuanText = findViewById(R.id.FamilyWeiYuxuanText);
        familyWeiYuxuanSettingButton = findViewById(R.id.FamilyWeiYuxuanSettingButton);


        familyWeiYuxuanText.setTextSize(textSize);
        familyWeiYuxuanButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();
            }
        });


        familyWeiYuxuanSettingButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(FamilyWeiYuxuan.this, FamilySettings.class);
                startActivityForResult(intent, REQUEST_CODE);
            }
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE && resultCode == RESULT_OK) {
            textSize = sharedPreferences.getInt("textSize", 20);
            familyWeiYuxuanText.setTextSize(textSize);
        }
    }
}
```

## 中将

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".family.FamilyLiuYuxuan">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <ImageButton

            android:id="@+id/FamilyZhongjiangSettingButton"
            android:layout_width="40sp"
            android:layout_height="40sp"
            android:layout_alignParentTop="true"

            android:layout_alignParentRight="true"
            android:layout_marginTop="20sp"
            android:src="@mipmap/ic_launcher"/>
        <TextView
            android:id="@+id/FamilyZhongjiangText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="\t\t\t\t二伪宇轩(中将)\n
\t\t\t\t女,真名张静宇,英文名2 FALSE SHEEN(简称2FS)来自二班。"
            android:layout_marginLeft="40dp"
            android:layout_marginRight="40dp"
            android:layout_marginTop="20dp"
            android:textSize="20sp"
            ></TextView>

        <TextView
            android:id="@+id/FamilyZhongjiangText2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="\t\t\t\t伪二伪宇轩(中将)\n
\t\t\t\t女,真名朱祎文,英文名3 FALSE SHEEN(简称3FS),来自六班。

"
            android:layout_marginLeft="40dp"
            android:layout_marginRight="40dp"
            android:layout_marginTop="20dp"
            android:layout_below="@id/FamilyZhongjiangText"
            android:textSize="20sp"
            ></TextView>

        <TextView
            android:id="@+id/FamilyZhongjiangText3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="
\t\t\t\t伪张雨轩(中将)男,真名薛斌,别名伪张。\n\t\t\t\t英文名FALSE BLACK SHEEN(简称FBS)。来自比第一大将刘宇轩低一届的一班。经典动作有:上齿咬下唇,挠头。与张雨轩极其相似:长相丑无奔头,脸色不黑,痘多却比张雨轩少,不愧是老张的化身。
"
            android:layout_marginLeft="40dp"
            android:layout_marginRight="40dp"
            android:layout_marginTop="20dp"
            android:layout_below="@id/FamilyZhongjiangText2"
            android:textSize="20sp"
            ></TextView>


        <Button
            android:id="@+id/FamilyZhongjiangButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="返回"
            android:textSize="20sp"
            android:layout_below="@id/FamilyZhongjiangText3"
            android:layout_centerHorizontal="true"/>
    </RelativeLayout>

</ScrollView>
```

```java
package com.example.yuouquotation.family;

import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageButton;
import android.widget.TextView;

import com.example.yuouquotation.R;

public class FamilyZhongjiang extends AppCompatActivity {


    private Button familyZhongjiangButton;
    private TextView familyZhongjiangText;
    private TextView familyZhongjiangText2;
    private TextView familyZhongjiangText3;
    private int textSize;
    private ImageButton familyZhongjiangSettingButton;
    SharedPreferences sharedPreferences;

    SharedPreferences.Editor editor;
    private int REQUEST_CODE = 1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_family_zhongjiang);


        familyZhongjiangButton = findViewById(R.id.FamilyZhongjiangButton);
        familyZhongjiangText = findViewById(R.id.FamilyZhongjiangText);
        familyZhongjiangText2 = findViewById(R.id.FamilyZhongjiangText2);
        familyZhongjiangText3 = findViewById(R.id.FamilyZhongjiangText3);
        familyZhongjiangSettingButton = findViewById(R.id.FamilyZhongjiangSettingButton);
        sharedPreferences = getSharedPreferences("app_settings", MODE_PRIVATE);
        editor = sharedPreferences.edit();
        textSize = sharedPreferences.getInt("textSize", 20);

        familyZhongjiangText.setTextSize(textSize);
        familyZhongjiangText2.setTextSize(textSize);
        familyZhongjiangText3.setTextSize(textSize);
        familyZhongjiangButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();
            }
        });

        familyZhongjiangSettingButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(FamilyZhongjiang.this, FamilySettings.class);
                startActivityForResult(intent, REQUEST_CODE);
            }
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(REQUEST_CODE == requestCode && resultCode == RESULT_OK){

            textSize = sharedPreferences.getInt("textSize", 20);
            familyZhongjiangText.setTextSize(textSize);
            familyZhongjiangText2.setTextSize(textSize);
            familyZhongjiangText3.setTextSize(textSize);
        }
    }
}
```

## 小将

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".family.FamilyLiuYuxuan">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <ImageButton

            android:id="@+id/FamilyXiaojiangSettingButton"
            android:layout_width="40sp"
            android:layout_height="40sp"
            android:layout_alignParentTop="true"

            android:layout_alignParentRight="true"
            android:layout_marginTop="20sp"
            android:src="@mipmap/ic_launcher"/>
        <TextView
            android:id="@+id/FamilyXiaojiangText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="\t\t\t\t侯宇轩(小将)\n\t\t\t\t
男,英文名MONKEY SHEEN(简称MS),来自四班。无奔头,无痘,但高颧骨,长相似骷髅。是宇轩家族的一代炮灰。\n\t\t\t\t出场率极少,在宇轩界中不受重视。
"
            android:layout_marginLeft="40dp"
            android:layout_marginRight="40dp"
            android:layout_marginTop="20dp"
            android:textSize="20sp"
            ></TextView>


        <Button
            android:id="@+id/FamilyXiaojiangButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="返回"
            android:textSize="20sp"
            android:layout_below="@id/FamilyXiaojiangText"
            android:layout_centerHorizontal="true"/>
    </RelativeLayout>

</ScrollView>
```

```java
package com.example.yuouquotation.family;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageButton;
import android.widget.TextView;

import com.example.yuouquotation.R;

public class FamilyXiaojiang extends AppCompatActivity {


    private Button familyXiaojiangButton;
    private TextView familyXiaojiangText;
    private int textSize;
    private SharedPreferences sharedPreferences;
    private SharedPreferences.Editor editor;
    private ImageButton familyXiaojiangSettingButton;
    private int REQUEST_CODE = 1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_family_xiaojiang);

        familyXiaojiangButton = findViewById(R.id.FamilyXiaojiangButton);
        familyXiaojiangText = findViewById(R.id.FamilyXiaojiangText);
        familyXiaojiangSettingButton = findViewById(R.id.FamilyXiaojiangSettingButton);
        sharedPreferences = getSharedPreferences("app_settings", MODE_PRIVATE);
        editor = sharedPreferences.edit();
        textSize = sharedPreferences.getInt("textSize", 20);

        familyXiaojiangText.setTextSize(textSize);
        familyXiaojiangButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();
            }
        });
        familyXiaojiangSettingButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(FamilyXiaojiang.this, FamilySettings.class);
                startActivityForResult(intent, REQUEST_CODE);

            }
        });
    }
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE && resultCode == RESULT_OK) {
            textSize = sharedPreferences.getInt("textSize", 20);
            familyXiaojiangText.setTextSize(textSize);
        }
    }
}
```

## 关于其中的信息传递逻辑实现

本来使用的是相应的每一个界面都有一个Setting按钮，对于文字颜色进行调整，而后发现比如A界面更改了信息，B界面还要经历一次修改过程，每一步都要用Bundle来完成么？显然繁琐，于是找到了sharedPreferences的方式，类似共享内存，不过建议是存储一些简单的信息。

# 完成夫的相应逻辑

## 思考能否进一步精简

因为之前每一次都是要定义类似的控件，能否创建一个类，使得其new一个实例，再往里赋值就可以了。在实现的过程中，发现可以直接采用继承的方式，甚至不需要使用new一个实例。

不过在获取对象时遇到了空指针的问题如下

## sharedPreferences null pointer?

我最初是在那个基类中获取的所有的Button，View等控件，会出现android：Initializing SharedPreferences提供：尝试在空对象引用上调用虚拟方法的问题。而后下午更改至OnCreate方法中竟然就不再报错，那么暂时不想深究，继续其他的开发。

当解决这个问题后发现采用相应的类进行开发，编写速度会有很大的提升，因为此时对于一个新的类，仅仅在获取控件的时候采用不同的id即可，而无需创建新的不同命名的控件。

于是创建了相应夫的xml与java文件进行交互。

## 模板类

```java
package com.example.yuouquotation.fu;

import android.content.SharedPreferences;
import android.widget.Button;
import android.widget.ImageButton;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class FuView extends AppCompatActivity {
    //布局文件
    private android.view.View fuActivity;
    //文字大小
    private int textSize;
    //设置请求
    public static final int REQUEST_CODE = 1;
    //返回按钮
    private Button fuButton;
    //介绍文字
    private TextView fuText;
    //设置按钮
    private ImageButton fuSettingButton;

    public SharedPreferences sharedPreferences;
    public SharedPreferences.Editor editor;

    public TextView getFuText() {
        return fuText;
    }

    public void setFuText(int fuText) {
        this.fuText = findViewById(fuText);
    }


    public ImageButton getFuSettingButton() {
        return fuSettingButton;
    }

    public void setFuSettingButton(int fuSettingButton) {
        this.fuSettingButton = findViewById(fuSettingButton);
    }
    public int getTextSize() {
        return textSize;
    }

    public void setTextSize(int textSize) {
        this.textSize = textSize;
    }


    public Button getFuButton() {
        return fuButton;
    }

    public void setFuButton(int fuButton) {
        this.fuButton = findViewById(fuButton);
    }

    public FuView() {
        super();
        //sharedPreferences = getSharedPreferences("app_settings", MODE_PRIVATE);
        //editor = sharedPreferences.edit();

    }

    public android.view.View getFuActivity() {
        return fuActivity;
    }

    public void setFuActivity(int fuActivity) {
        this.fuActivity = findViewById(fuActivity);
    }



}

```



# 建立第一章 家族介绍

## 结构

包含两大家族宇轩和夫，同样是通过Intent进行交互，不过为他们设置了不同的图标，在drawable文件夹下放置了需要使用的图片，使用的时候将其通过id引用。
