
### Get developer settings

```
adb shell settings get global development_settings_enabled
```

### Show touches

```
adb shell content insert --uri content://settings/system --bind name:s:show_touches --bind value:i:1

adb shell settings put system show_touches 1
```

### Screencap
```
adb shell screencap -p /sdcard/screenshot.png
```

### Data types
```
adb shell 'am broadcast -a org.example.app.sp.PUT --es key string --es value "hello world!"'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key boolean --ez value true'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key float --ef value 3.14159'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key int --ei value 2015'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key long --el value 9223372036854775807'
```

### Open URL
```
adb shell am start -a android.intent.action.VIEW -d URL
```