[![](https://jitpack.io/v/Kunzisoft/Android-SwitchDateTimePicker.svg)](https://jitpack.io/#Kunzisoft/Android-SwitchDateTimePicker) [![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-SwitchDateTimePicker-blue.svg?style=flat)](http://android-arsenal.com/details/1/4513)

# Android SwitchDateTime Picker

<img src="https://raw.githubusercontent.com/Kunzisoft/Android-SwitchDateTimePicker/master/art/logo.png"> SwitchDateTime Picker is a library for select a *Date* object in dialog with a DatePicker (Calendar) and a TimePicker (Clock) in the same UI.

<img src="https://raw.githubusercontent.com/Kunzisoft/Android-SwitchDateTimePicker/master/art/demo2.gif" width="500">
<img src="https://raw.githubusercontent.com/Kunzisoft/Android-SwitchDateTimePicker/master/art/demo1.gif" width="320">

## Donation

Donations will be used to create free and open source applications.

[![Donation Paypal](https://4.bp.blogspot.com/-ncaIbUGaHOk/WfhaThYUPGI/AAAAAAAAAVQ/_HidNgdB1q4DaC24ujaKNzH64KUUJiQewCLcBGAs/s1600/pay-with-paypal.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=KM6QMDAXZM3UU "Kunzisoft Paypal Donation")

<a href="bitcoin:1DSwXCk7Sob24sNsofywNoRQw2f5Qj5t2F"><img src="https://2.bp.blogspot.com/-K7-LKnSZd7c/WkvIKpLdmKI/AAAAAAAAAVs/-5LTimDq5IURMHwMmEP5VPTT53b2EUsswCLcBGAs/s1600/donate-with-bitcoin.png" alt="Kunzisoft Bitcoin" />Bitcoin wallet address : 1DSwXCk7Sob24sNsofywNoRQw2f5Qj5t2F</a>

[![Donation Liberapay](https://liberapay.com/assets/widgets/donate.svg)](https://liberapay.com/Kunzisoft/donate "Kunzisoft Liberapay Donation")

## Installation
Add the JitPack repository in your build.gradle at the end of repositories:
```
	allprojects {
		repositories {
			...
			maven { url "https://jitpack.io" }
		}
	}
```
And add the dependency
```
	dependencies {
	        compile 'com.github.Kunzisoft:Android-SwitchDateTimePicker:1.9'
	}
```

## Usage

### SimpleDateFormat for Day and Month
You can specify a particular [*SimpleDateFormat*](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html) for value of Day and Month with **setSimpleDateMonthAndDayFormat(SimpleDateFormat format)**
Warning, the format must satisfy the regular expression : **(M|w|W|D|d|F|E|u|\s)***
, for example *dd MMMM*

### 24 Hours mode
By default, time is in 12 hours mode, If you want a 24-hour display, use:
`dateTimeFragment.set24HoursMode(true);`
before the "show"

### Start with a specific view
For launch Dialog with a specific view, call :
`dateTimeFragment.startAtTimeView();`, `dateTimeFragment.startAtCalendarView();` or `dateTimeFragment.startAtYearView();`
before the "show"

### Define minimum and maximum
For just allow selection after or/and before dates, use :
`dateTimeFragment.setMinimumDateTime(Date minimum);`
and
`dateTimeFragment.setMaximumDateTime(Date maximum);`

### Style
You can customize the style to change color, bold, etc... of each element.
You need to use a Theme.AppCompat theme (or descendant) with SwitchDateTime's activity. (`compile 'com.android.support:appcompat-v7:25.1.0'` in gradle)

<img src="https://raw.githubusercontent.com/Kunzisoft/Android-SwitchDateTimePicker/master/art/screen2.jpg" width="320">

In your *styles.xml*, you can redefine each style separately, but you must keep each item, for example : change size of "year label"
```
<resources>
    <!-- Base application theme. -->
    <style name="MyAppCustomTheme" parent="Theme.AppCompat.Light">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

    <!-- SwitchDateTime style is independent, each element is optional-->
    <!-- Year Precise -->
    <style name="Theme.SwitchDateTime.DateLabelYear">
        <item name="android:textSize">58sp</item>
        <item name="android:textColor">#fff</item>
        <item name="android:textStyle">bold</item>
    </style>
</resources>

```
Styles elements : https://github.com/Kunzisoft/Android-SwitchDateTimePicker/blob/master/switchdatetime/src/main/res/values/styles.xml

#### AlertStyle
To customize the AlertDialog that is shown, use :
`void setAlertStyle(@StyleRes int styleId)`

### Sample
You can see
https://github.com/J-Jamet/Android-SwitchDateTimePicker/blob/master/sample/src/main/java/com/kunzisoft/switchdatetimesample/Sample.java
for complete sample.
```
// Initialize
SwitchDateTimeDialogFragment dateTimeDialogFragment = SwitchDateTimeDialogFragment.newInstance(
        "Title example",
        "OK",
        "Cancel"
);

// Assign values
dateTimeFragment.startAtCalendarView();
dateTimeFragment.set24HoursMode(true);
dateTimeFragment.setMinimumDateTime(new GregorianCalendar(2015, Calendar.JANUARY, 1).getTime());
dateTimeFragment.setMaximumDateTime(new GregorianCalendar(2025, Calendar.DECEMBER, 31).getTime());
dateTimeFragment.setDefaultDateTime(new GregorianCalendar(2017, Calendar.MARCH, 4, 15, 20).getTime());
// Or assign each element, default element is the current moment
// dateTimeFragment.setDefaultHourOfDay(15);
// dateTimeFragment.setDefaultMinute(20);
// dateTimeFragment.setDefaultDay(4);
// dateTimeFragment.setDefaultMonth(Calendar.MARCH);
// dateTimeFragment.setDefaultYear(2017);

// Define new day and month format
try {
    dateTimeFragment.setSimpleDateMonthAndDayFormat(new SimpleDateFormat("dd MMMM", Locale.getDefault()));
} catch (SwitchDateTimeDialogFragment.SimpleDateMonthAndDayFormatException e) {
    Log.e(TAG, e.getMessage());
}

// Set listener
dateTimeDialogFragment.setOnButtonClickListener(new SwitchDateTimeDialogFragment.OnButtonClickListener() {
    @Override
    public void onPositiveButtonClick(Date date) {
        // Date is get on positive button click
        // Do something
    }

    @Override
    public void onNegativeButtonClick(Date date) {
        // Date is get on negative button click
    }
});

// Show
dateTimeDialogFragment.show(getSupportFragmentManager(), "dialog_time");
```

#### Neutral button

<img src="https://raw.githubusercontent.com/Kunzisoft/Android-SwitchDateTimePicker/master/art/screen3.jpg" width="320">

To use with a neutral button, initialize with another parameter and implement the *OnButtonWithNeutralClickListener* :
```
SwitchDateTimeDialogFragment dateTimeDialogFragment = SwitchDateTimeDialogFragment.newInstance(
        "Title example",
        "OK",
        "Cancel",
        "Clean"
);

dateTimeFragment.setOnButtonClickListener(new SwitchDateTimeDialogFragment.OnButtonWithNeutralClickListener() {
    @Override
    public void onPositiveButtonClick(Date date) {
    }

    @Override
    public void onNegativeButtonClick(Date date) {
    }

    @Override
    public void onNeutralButtonClick(Date date) {
    }
});
```

## Bonus
You can follow the project live on https://www.livecoding.tv/kunzisoft/

## License

Copyright (c) 2016 JAMET Jeremy

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
