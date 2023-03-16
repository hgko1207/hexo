---
title: '[Android] Yahoo Weather API를 이용하여 날씨정보 조회'
categories:
  - Programming
  - Mobile
  - Android
tags:
  - Android
  - Weather
  - 안드로이드
date: 2021-05-12 16:58:49
thumbnail: /images/thumbnail/android.png
---

**Yahoo Weather API** 를 이용하여 현재 위치의 날씨 정보를 조회하는 방법에 대해 알아보겠습니다.

## 개발 환경

- Android Studio
- Java

## 설정

- build.gradle -> dependencies 추가

```gradle
implementation 'zh.wang.android:yweathergetter4a:1.3.0'
```

- manifest -> permission 추가

```xml
<!-- 인터넷 사용 권한 -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />

<!-- GPS 사용 권한 -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

## 코드 작성

Activity 또는 Fragment 에 `YahooWeatherInfoListener` 인터페이스를 implements 하면 `gotWeatherInfo` 함수를 오버라이딩(Override)을 하게 됩니다.

```java
public class WeatherActivity extends Activity implements YahooWeatherInfoListener {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_weather);
  }

  @Override
  public void gotWeatherInfo(WeatherInfo weatherInfo, YahooWeather.ErrorType errorType) {
  }
}
```

이제 날씨 정보를 불러오기 위해 아래 함수 중 상황에 맞게 호출합니다.

```java
// 장소 이름으로 쿼리
public void queryYahooWeatherByPlaceName(final Context context, final String cityAreaOrLocation, final YahooWeatherInfoListener result)

// 위도와 경도로 쿼리
public void queryYahooWeatherByLatLon(final Context context, final String lat, final String lon, final YahooWeatherInfoListener result)

// GPS를 사용하여 현재 위치로 쿼리
public void queryYahooWeatherByGPS(final Context context, final YahooWeatherInfoListener result)
```

이번 프로젝트에는 GPS를 사용하여 현재 위치의 날씨 정보를 얻었습니다. 쿼리 함수를 호출하면 오버라이딩한 `gotWeatherInfo` 함수를 통해 날씨 정보를 얻을 수 있습니다.

```java
YahooWeather yahooWeather = YahooWeather.getInstance();

yahooWeather.setNeedDownloadIcons(true);
yahooWeather.setUnit(YahooWeather.UNIT.CELSIUS);
yahooWeather.setSearchMode(YahooWeather.SEARCH_MODE.GPS);
yahooWeather.queryYahooWeatherByGPS(getApplicationContext(), this);
```

날씨 정보를 한 번만 불러오는 것이 아니라 1분 마다 얻기 위해 Timer 를 사용하였습니다. Timer 를 사용하기 위해 위의 코드를 함수로 만들었습니다.

```java
Timer timer = new Timer();
timer.scheduleAtFixedRate(new TimerTask() {
    @Override
    public void run() {
        new Handler(Looper.getMainLooper()).post(new Runnable() {
            @Override
            public void run() {
                searchByGPS();
            }
        });
    }
}, 0, 1000 * 60);

public void searchByGPS() {
  yahooWeather.setNeedDownloadIcons(true);
  yahooWeather.setUnit(YahooWeather.UNIT.CELSIUS);
  yahooWeather.setSearchMode(YahooWeather.SEARCH_MODE.GPS);
  yahooWeather.queryYahooWeatherByGPS(getApplicationContext(), this);
}
```

이제 1분 마다 날씨 정보를 불러올 수 있게 되었습니다. 현재 위치, 시간, 온도, 습도, 대기압, 풍향, 풍속 등의 다양한 날씨 정보를 화면에 표출하여 완성하였습니다.

```java
@Override
  public void gotWeatherInfo(WeatherInfo weatherInfo, YahooWeather.ErrorType errorType) {
      if (weatherInfo != null) {
          datetimeText.setText(dateFormat.format(new Date()));
          logitudeText.setText(weatherInfo.getAddress().getLongitude() + "");
          latitudeText.setText(weatherInfo.getAddress().getLatitude() + "");
          addressText.setText(weatherInfo.getAddress().getAddressLine(0));
          weatherText.setText(weatherInfo.getCurrentText());
          temperatureText.setText(weatherInfo.getCurrentTemp() + " ºC");
          humidityText.setText(weatherInfo.getAtmosphereHumidity() + " %");
          pressureText.setText(weatherInfo.getAtmospherePressure());
          windDirectionText.setText(weatherInfo.getWindDirection() + "˚");
          windSpeedText.setText(weatherInfo.getWindSpeed() + " m/s");
          windChillText.setText(weatherInfo.getWindChill() + " °F");
          visibilityText.setText(weatherInfo.getAtmosphereVisibility());
      }
  }
```

## 전체 코드

```java
// WeatherActivity.java

import android.os.Handler;
import android.os.Looper;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.TextView;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Timer;
import java.util.TimerTask;

import butterknife.BindView;
import butterknife.ButterKnife;
import me.hgko.networkinfo.R;
import zh.wang.android.yweathergetter4a.WeatherInfo;
import zh.wang.android.yweathergetter4a.YahooWeather;
import zh.wang.android.yweathergetter4a.YahooWeatherInfoListener;

public class WeatherActivity extends AppCompatActivity implements YahooWeatherInfoListener {

    private final SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy.MM.dd HH:mm:ss");

    @BindView(R.id.logitudeText)
    TextView logitudeText;
    @BindView(R.id.latitudeText)
    TextView latitudeText;
    @BindView(R.id.datetimeText)
    TextView datetimeText;
    @BindView(R.id.addressText)
    TextView addressText;
    @BindView(R.id.weatherText)
    TextView weatherText;
    @BindView(R.id.temperatureText)
    TextView temperatureText;
    @BindView(R.id.humidityText)
    TextView humidityText;
    @BindView(R.id.pressureText)
    TextView pressureText;
    @BindView(R.id.windDirectionText)
    TextView windDirectionText;
    @BindView(R.id.windSpeedText)
    TextView windSpeedText;
    @BindView(R.id.windChillText)
    TextView windChillText;
    @BindView(R.id.visibilityText)
    TextView visibilityText;

    private YahooWeather yahooWeather;

    private Timer timer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_weather);
        ButterKnife.bind(this);

        yahooWeather = YahooWeather.getInstance();

        timer = new Timer();
        timer.scheduleAtFixedRate(new TimerTask() {
            @Override
            public void run() {
                new Handler(Looper.getMainLooper()).post(new Runnable() {
                    @Override
                    public void run() {
                        searchByGPS();
                    }
                });
            }
        }, 0, 1000 * 60 * 10);
    }

    @Override
    public void gotWeatherInfo(WeatherInfo weatherInfo, YahooWeather.ErrorType errorType) {
        if (weatherInfo != null) {
            datetimeText.setText(dateFormat.format(new Date()));
            logitudeText.setText(weatherInfo.getAddress().getLongitude() + "");
            latitudeText.setText(weatherInfo.getAddress().getLatitude() + "");
            addressText.setText(weatherInfo.getAddress().getAddressLine(0));
            weatherText.setText(weatherInfo.getCurrentText());
            temperatureText.setText(weatherInfo.getCurrentTemp() + " ºC");
            humidityText.setText(weatherInfo.getAtmosphereHumidity() + " %");
            pressureText.setText(weatherInfo.getAtmospherePressure());
            windDirectionText.setText(weatherInfo.getWindDirection() + "˚");
            windSpeedText.setText(weatherInfo.getWindSpeed() + " m/s");
            windChillText.setText(weatherInfo.getWindChill() + " °F");
            visibilityText.setText(weatherInfo.getAtmosphereVisibility());
        }
    }

    private void searchByGPS() {
        yahooWeather.setNeedDownloadIcons(true);
        yahooWeather.setUnit(YahooWeather.UNIT.CELSIUS);
        yahooWeather.setSearchMode(YahooWeather.SEARCH_MODE.GPS);
        yahooWeather.queryYahooWeatherByGPS(getApplicationContext(), this);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        if (timer != null) {
            timer.cancel();
            timer = null;
        }
    }
}
```

```xml
<!-- activity_weather.xml -->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="20dp"
    android:paddingLeft="20dp"
    android:paddingRight="20dp"
    android:paddingTop="20dp"
    tools:context=".activity.WeatherActivity">

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Datetime :" />

                <TextView
                    android:id="@+id/datetimeText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Logitude :" />

                <TextView
                    android:id="@+id/logitudeText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Latitude :" />

                <TextView
                    android:id="@+id/latitudeText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Address :" />

                <TextView
                    android:id="@+id/addressText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Weather :" />

                <TextView
                    android:id="@+id/weatherText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Temperature :" />

                <TextView
                    android:id="@+id/temperatureText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Wind Chill :" />

                <TextView
                    android:id="@+id/windChillText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Wind Direction :" />

                <TextView
                    android:id="@+id/windDirectionText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Wind Speed :" />

                <TextView
                    android:id="@+id/windSpeedText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Humidity :" />

                <TextView
                    android:id="@+id/humidityText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Pressure :" />

                <TextView
                    android:id="@+id/pressureText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:orientation="horizontal">

                <TextView
                    style="@style/TextStyle1"
                    android:text="Visibility :" />

                <TextView
                    android:id="@+id/visibilityText"
                    style="@style/TextStyle2"
                    android:textColor="@color/colorBlue" />
            </LinearLayout>
        </LinearLayout>
    </ScrollView>
</LinearLayout>
```

TextView 에 공통으로 스타일을 지정하기 위해 styles.xml 에 추가합니다.

```xml
<style name="TextStyle1">
    <item name="android:layout_width">0dp</item>
    <item name="android:layout_height">wrap_content</item>
    <item name="android:layout_weight">1</item>
    <item name="android:textColor">@color/colorText</item>
    <item name="android:textSize">14sp</item>
</style>

<style name="TextStyle2">
    <item name="android:layout_width">0dp</item>
    <item name="android:layout_height">wrap_content</item>
    <item name="android:layout_weight">2</item>
    <item name="android:textColor">@color/colorText</item>
    <item name="android:textSize">14sp</item>
</style>
```

## 실행 결과

앱을 실행하면 아래 이미지와 같이 현재 위치의 날씨 정보를 확인할 수 있습니다.

<img width="50%" src="/images/android/dev1/weather.png" alt="" title="">

## 참고

- https://github.com/zh-wang/YWeatherGetter4a
