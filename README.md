# GlideImagePicker
  
GlideImagePicker is a well-designed local image and video selector for Android. You can  
- Use it in Activity or Fragment
- Select images including JPEG, PNG, GIF and videos including MPEG, MP4 
- Apply different themes, including two built-in themes and custom themes
- Different image loaders
- Define custom filter rules
- More to find out yourself

![](image/screenshot_zhihu.png) 

## Download
Gradle:

```groovy
repositories {
    jcenter()
}

dependencies {
    compile 'com.github.arover:GlideImagePicker:1.0'
}
```

Check out [GlideImagePicker releases](https://github.com/arover/GlideImagePicker/releases) to see more unstable versions.

## ProGuard
```pro
-dontwarn com.bumptech.glide.**
```

## How do I use GlideImagePicker?
#### Permission
The library requires two permissions:
- `android.permission.READ_EXTERNAL_STORAGE`
- `android.permission.WRITE_EXTERNAL_STORAGE`

So if you are targeting Android 6.0+, you need to handle runtime permission request before next step.

#### Simple usage snippet
------
Start `ImagePickerActivity` from current `Activity` or `Fragment`:

```java
ImagePicker.from(MainActivity.this)
        .choose(MimeType.allOf())
        .countable(true)
        .maxSelectable(9)
        .addFilter(new GifSizeFilter(320, 320, Filter.kb(5)))
        .gridExpectedSize(getResources().getDimensionPixelSize(R.dimen.grid_expected_size))
        .restrictOrientation(ActivityInfo.SCREEN_ORIENTATION_UNSPECIFIED)
        .thumbnailScale(0.85f)
        .forResult(REQUEST_CODE_CHOOSE);
```
 
#### Themes
There are two built-in themes you can use to start `MatisseActivity`:
- `R.style.GlideImagePicker.Light` (light mode)
- `R.style.GlideImagePicker.Dark` (dark mode)  

And Also you can define your own theme as you wish.

#### Receive Result
In `onActivityResult()` callback of the starting `Activity` or `Fragment`:

```java
List<Uri> mSelected;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == REQUEST_CODE_CHOOSE && resultCode == RESULT_OK) {
        mSelected = Matisse.obtainResult(data);
        Log.d(TAG, "selected: " + mSelected);
    }
}
```

## License

    Copyright 2017 Arover Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
