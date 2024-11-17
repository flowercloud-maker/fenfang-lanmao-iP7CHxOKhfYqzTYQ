[合集 \- 玩转Streamlit(9\)](https://github.com)[1\.什么是Streamlit10\-11](https://github.com/wang_yb/p/18458062)[2\.『玩转Streamlit』\-\-环境配置10\-17](https://github.com/wang_yb/p/18471660)[3\.『玩转Streamlit』\-\-架构和运行机制10\-22](https://github.com/wang_yb/p/18492213)[4\.『玩转Streamlit』\-\-多页应用10\-25](https://github.com/wang_yb/p/18502232):[wgetCloud机场](https://tabijibiyori.org)[5\.『玩转Streamlit』\-\-页面布局10\-31](https://github.com/wang_yb/p/18516928)[6\.『玩转Streamlit』\-\-登录认证机制11\-05](https://github.com/wang_yb/p/18527320)[7\.『玩转Streamlit』\-\-文本与标题组件11\-07](https://github.com/wang_yb/p/18531821)[8\.『玩转Streamlit』\-\-数据展示组件11\-13](https://github.com/wang_yb/p/18543687)9\.『玩转Streamlit』\-\-图像与媒体组件11\-16收起
`Streamlit`中的图像与媒体组件，主要是`st.image`、`st.audio`和`st.video`。


它们是专为在`Streamlit Web`应用程序中嵌入和展示多媒体内容而设计的，这些组件不仅丰富了应用程序的呈现形式，还极大地提升了用户体验和互动性。


# 1\. st.image


`st.image`函数用于在`Streamlit`应用程序中展示图像内容，增强视觉呈现效果。


比如，在数据可视化的场景中，通过`st.image`展示数据分析结果，如柱状图、折线图等；


在项目展示时，也可以通过在项目中嵌入产品图片、示意图等，提升用户理解。


它的主要参数有：




| **名称** | **类型** | **说明** |
| --- | --- | --- |
| image | numpy.ndarray / \[numpy.ndarray] / BytesIO / str / \[str] | 要显示的图像，也可以指定一个图像URL或URL列表 |
| caption | str/\[str] | 图像标题，如果显示多幅图像，应当是字符串列表 |
| width | int / None | 图像宽度，None表示使用图像自身宽度 |
| clamp | bool | 是否将图像的像素值压缩到有效域（0\~255），仅对字节数组图像有效 |
| channels | "RGB" / "BGR" | 图像通道类型 |
| output\_format | "JPEG" / "PNG" / "auto" | 图像格式 |
| use\_container\_width | bool | 如果设置为True，则使用列宽作为图像宽度 |


## 1\.1\. 使用示例


展示本地图像文件，通过`image`参数接受PIL图像对象，`caption`参数为图像添加标题，


`width`参数设置了图像的显示宽度。



```
import streamlit as st
from PIL import Image

# 读取本地图像文件
image = Image.open("path/to/your/image.jpg")

# 使用st.image展示图像，并设置标题和宽度
st.image(image, caption="这是一张本地图片", width=300)

```

![](https://img2024.cnblogs.com/blog/83005/202411/83005-20241116193515472-1673960141.png)


展示`URL`图像，并使用`use_column_width`参数使图像宽度自适应`Streamlit`列的宽度。



```
# 图像URL
image_url = "http://xxx.com/xxx.jpeg"

# 使用st.image展示URL图像，并设置使用列宽
st.image(
    image_url,
    use_column_width=True,
    caption="这是一张网络图片",
)

```

![](https://img2024.cnblogs.com/blog/83005/202411/83005-20241116193515448-473608419.gif)


图片的宽度会随着浏览器窗口的大小自适应变化。


# 2\. st.audio


`st.audio`函数用于在`Streamlit`应用程序中嵌入音频内容，为数据分析结果添加声音效果，增强表现力。


它的主要参数有：




| **名称** | **类型** | **说明** |
| --- | --- | --- |
| data | str / bytes / BytesIO / numpy.ndarray / file | 要播放的音频数据，可以是字节码流、numpy.ndarray或打开的文件 |
| format | str | 音频文件的MIME类型，如'audio/ogg'、'audio/mp3'等 |
| start\_time | int / float / timedelta / str / None | 指定音频播放的起始时间 |
| sample\_rate | int / None | 音频的采样率，播放音频时，通常不需要直接设置这个参数 |
| end\_time | int / float / timedelta / str / None | 指定音频播放的结束时间 |
| loop | bool | 是否循环播放音频 |
| autoplay | bool | 是否自动播放音频 |


## 2\.1\. 使用示例


播放本地音频文件，`autoplay`参数设置为`True`，使音频自动播放。



```
import streamlit as st

# 打开本地音频文件
audio_file = open("path/to/your/audio.mp3", "rb")
audio_bytes = audio_file.read()

# 使用st.audio播放音频，并自动播放
st.audio(
    audio_bytes,
    format="audio/mp3",
    autoplay=True,
)

```

![](https://img2024.cnblogs.com/blog/83005/202411/83005-20241116193515357-1143094667.png)


运行之后会自动播放。


和`st.image`一样，音频也可以传入URL，直接播放在线的音频。


# 3\. st.video


`st.video`函数用于在`Streamlit`应用程序中嵌入视频内容，通过视频展示分析结果的特点或分析过程。


它的主要参数有：




| **名称** | **类型** | **说明** |
| --- | --- | --- |
| data | str / bytes / BytesIO / numpy.ndarray / file | 要播放的视频数据，可以是URL字符串、字节码流、numpy.ndarray或打开的文件 |
| format | str | 视频文件的MIME类型，如'video/mp4'，默认值为'video/mp4' |
| start\_time | int / float / timedelta / str / None | 视频开始播放的时间 |
| subtitles | str / bytes / Path / io.BytesIO / dict | 视频字幕数据 |
| end\_time | int / float / timedelta / str / None | 视频结束播放的时间 |
| loop | bool | 是否循环播放视频 |
| autoplay | bool | 是否自动播放视频 |
| muted | bool | 是否静音播放 |


## 3\.1\. 使用示例


播放本地视频文件, 通过`start_time`和`end_time`参数设置了视频播放开始和结束的时间（秒）。



```
import streamlit as st

# 打开本地视频文件
video_file = open('path/to/your/video.mp4', 'rb')
video_bytes = video_file.read()

# 使用st.video播放视频，并设置标题和开始时间
st.video(
    video_bytes,
    format="video/mp4",
    start_time=5,
    end_time=10,
)

```

运行之后，视频加载后停在`5s`的位置，点击播放，播放到`10s`时自动停止。


![](https://img2024.cnblogs.com/blog/83005/202411/83005-20241116193515452-511804789.gif)


# 4\. 总结


总之，`st.image`、`st.audio`和`st.video`这三个组件共同构成了Streamlit中强大的多媒体展示工具集。


它们各自专注于图像、音频和视频的展示与播放，通过丰富的参数设置和灵活的嵌入方式，为开发者提供了极大的便利和创意空间。


无论是构建数据可视化应用、产品展示页面还是在线教育平台，这些组件都能帮助开发者轻松实现多媒体内容的嵌入与呈现。


