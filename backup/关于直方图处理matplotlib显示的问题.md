https://github.com/matplotlib/matplotlib/issues/7221/

`matplotlib`的`imshow`有时会显示错误的图片，而`ski.io.imread`不会。原因是pyplot会对图片进行直方图处理再输出。

```python
plt.imshow(histogram_original_images[i], vmin=0, vmax=255, cmap='gray')
```

解决方案如上所示，手动规定灰度值的最大值和最小值。这里有一个知识点：图像的灰度级的值，可以有多种表示方式，常见的是uint8和float。uint8即映射到0 ~ 255，float即映射到0 ~ 1。因此，imshow在处理图像时默认会以其中最低值到最高值映射到白色和黑色对应的灰度，并输出。这种方式带来的问题就是在对如下图片处理时会出现异常结果：


![image](https://github.com/aldehyde-rcho/aldehyde-rcho.github.io/assets/72068339/7a47c9bd-56b3-4728-ba8c-634ed9330931)

![image](https://github.com/aldehyde-rcho/aldehyde-rcho.github.io/assets/72068339/2eddfdbc-e329-4767-82ac-a5e78380c1b8)

后者为错误显示的图像。原因也很简单，看直方图就一目了然。