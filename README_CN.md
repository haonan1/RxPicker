## RxPicker

基于 RxJava 的 Android 图片选择器.

## 特征

1. 与 RxJava 结合,支持响应式得到选择图片结果
2. 支持单/多选图片
3. 兼容 Android 7.0
4. 支持自定义 `RxPickerImageLoader`



## Demo


## 预览图


## 使用

1.添加 gradle 引用

```
compile 'com.caimuhao:rxpicker:1.0.0'
```

2.继承 `RxPickerImageLoader` 创建自定义的图片加载

```
public class GlideImageLoader implements RxPickerImageLoader {

  @Override public void display(ImageView imageView, String path, int width, int height) {
    Glide.with(imageView.getContext())
        .load(path)
        .error(R.drawable.ic_preview_image)
        .centerCrop()
        .override(width, height)
        .into(imageView);
  }
}
```

3.初始化 `RxPicker`

```
RxPickerManager.getInstance().init(new GlideImageLoader());
```

4.使用

- 图片单选
```
RxPicker.of().start(this).subscribe(new Action1<List<ImageItem>>() {
        @Override public void call(List<ImageItem> images) {
          // 得到结果
        }
      });
```

- 图片多选

```
RxPicker.of()
          .single(false)
          .camera(true)
          .limit(3)
          .start(this)
          .subscribe(new Action1<List<ImageItem>>() {
            @Override public void call(List<ImageItem> images) {
              //  得到结果

            }
          });
```