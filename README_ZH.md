# Mathematica 编曲简化宏包
[![license](https://img.shields.io/badge/license-CC_BY_NC_SA-74c853.svg)](https://github.com/MuGemSt/Mathematica-Music-Pack/blob/main/LICENSE)
[![CI](https://github.com/MuGemSt/Mathematica-Music-Pack/actions/workflows/blank.yml/badge.svg?branch=main)](https://github.com/MuGemSt/Mathematica-Music-Pack/actions/workflows/blank.yml)
[![](https://img.shields.io/badge/bilibili-BV1r14y1G7E5-fc8bab.svg)](https://www.bilibili.com/video/BV1r14y1G7E5)
[![](https://img.shields.io/badge/cnblog-17191082-075db3.svg)](https://www.cnblogs.com/MuGem/p/17191082.html)

## 维护
```bash
git clone git@github.com:MuGemSt/Mathematica-Music-Pack.git
cd Mathematica-Music-Pack
```

## 用户手册
我们使用向量和数字来代替复杂的 SoundNote[] 系列函数。 经简化后的一首完整歌曲格式如下：

```txt
track1 = {
    {片段1参数},
    {片段1乐谱},

    {片段2参数},
    {片段2乐谱},

    ...

    {片段m参数},
    {片段m乐谱}
};

track2 = {
    {片段1参数},
    {片段1乐谱},

    {片段2参数},
    {片段2乐谱},

    ...

    {片段n参数},
    {片段n乐谱}
};

...

player[track1, 音色1, track2, 音色2, ...]
```

一个片段由参数域和乐谱域组成，参数域包含4个必要参数（音调、中心音、移调、速度）和一个可选参数（音量 或 音量变化）；其中参数域遵循以下规则：

<div align=center><b>表 1: 参数域格式</b><br></div>

| <div style="width:120px;">格式</div>           | 符号                                                                                                                                                 |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| *{m, c, s, t}*                                 | *m* 为大小调(0大调，1小调);<br>*c* 为中心音([0, 11]);<br>*s* 为移调(片段整体移动s个半音);<br>*t* 为速度(即乐谱左上角标记的一个四分音符所等于的数字); |
| *{m, c, s, t, v}*                              | *v* 为音量([0, 1]);                                                                                                                                  |
| *{m, c, s, t, {v<sub>s</sub>, v<sub>t</sub>}}* | 音量从 *v<sub>s</sub>* 渐变到 *v<sub>t</sub>*                                                                                                        |

<div align=center><b>表 2: 中心音表</b><br></div>

| C   | C#/Db | D   | Eb/D# | E   | F   | F#/Gb | G   | Ab/G# | A   | Bb/A# | B   |
| --- | ----- | --- | ----- | --- | --- | ----- | --- | ----- | --- | ----- | --- |
| 0   | 1     | 2   | 3     | 4   | 5   | 6     | 7   | 8     | 9   | 10    | 11  |

乐谱域由不同种类的音符组成：

<div align=center><b>表 3: 音符的输入格式</b><br></div>

| 音效                                  | 格式                                                                  | 标记                                                               |
| ------------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------ |
| <div style="width:50px;">休止符</div> | *{l}*                                                                 | *l* 为时值                                                         |
| 音符                                  | *{n, l}*                                                              | *n* 为音高                                                         |
| 和弦                                  | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l}*                            | *n<sub>k</sub>* 为和弦上各音符音高                                 |
| 跳音                                  | *{n, {l<sub>1</sub>, l<sub>2</sub>}}*                                 | *l<sub>1</sub>* 为时值, *l<sub>2</sub>* 为缩短后时值占真实时值比率 |
| 颤音                                  | *{{n<sub>1</sub>, n<sub>2</sub>}, l<sub>1</sub>, t<sub>n</sub>}*      | *t<sub>n</sub>* 为抖动次数                                         |
| 波音                                  | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l<sub>1</sub>, l<sub>2</sub>}* | *l<sub>2</sub>* 为琶音变化时值占真总时值比率                       |
| 延音                                  | <div style="width:150px;">*{背景音, 主题旋律}*</div>                  | 背景音可以是一个音符或一个和弦, 主题旋律可以由上述任何类型组成     |

根据以上规则，给出以下音效示例：

<div align=center>
    <b>表 4: 音效示例</b><br>
    <img width="605" src="https://user-images.githubusercontent.com/20459298/233112536-f5b900e8-8201-4e9b-9672-43f99b2979f3.PNG"/>
</div>

对于乐谱域的音符，12音模式使用起来并不方便，一旦调性固定，可将其转为7音模式：

<div align=center>
    <b>表 5: (左)12音模式 与 (右)7音模式</b><br>
    <img width="500" src="https://user-images.githubusercontent.com/20459298/233112569-3efd5cb1-87c3-44a6-b74b-357104055dd3.png"/>
</div>

可参考示例代码 _Demo_BWV-1079.nb_ 或浏览 <a href="https://MuGemSt.github.io/Mathematica-Music-Pack" target="_blank">我的Mathematica音乐库</a> 来弄清具体用法;<br>生成乐谱之前请先运行 _Mathematica-Music-Pack.nb_

另外，`e-piano.nb` 是一个编写于 Mathematica 上的钢琴键盘，可作为虚拟钢琴来弹奏。
