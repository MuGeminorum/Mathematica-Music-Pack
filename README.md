# Mathematica Music Package 编曲简化宏包
[![license](https://img.shields.io/badge/license-CC_BY_NC_SA-74c853.svg)](https://github.com/Genius-Society/mathematica_music_pack/blob/main/LICENSE)
[![Netlify Status](https://api.netlify.com/api/v1/badges/4c303588-a7e2-4cb8-bd82-e32aa5c831e5/deploy-status)](https://mathmusic.netlify.app)
[![bilibili](https://img.shields.io/badge/bilibili-BV14krgYJEJU-fc8bab.svg)](https://www.bilibili.com/video/BV14krgYJEJU)

A macro package for simplifying composition on Mathematica

## Maintenance 维护
```bash
git clone git@github.com:Genius-Society/mathematica_music_pack.git
cd mathematica_music_pack
```

## User manual 用户手册
We use vectors and numbers to replace complicated SoundNote[] functions. A complete song has many sections, its format is as follow:
我们使用向量和数字来代替复杂的 SoundNote[] 系列函数。 经简化后的一首完整歌曲格式如下：
```txt
track1 = {
    {params of section 1}, (*{片段1参数}*)
    {notes  of section 1}, (*{片段1乐谱}*)

    {params of section 2}, (*{片段2参数}*)
    {notes  of section 2}, (*{片段2乐谱}*)

    ...

    {params of section m}, (*{片段m参数}*)
    {notes  of section m}  (*{片段m乐谱}*)
};

track2 = {
    {params of section 1}, (*{片段1参数}*)
    {notes  of section 1}, (*{片段1乐谱}*)

    {params of section 2}, (*{片段2参数}*)
    {notes  of section 2}, (*{片段2乐谱}*)

    ...

    {params of section n}, (*{片段n参数}*)
    {notes  of section n}  (*{片段n乐谱}*)
};

...

player[track1, soundfont1, track2, soundfont2, ...]
(*player[track1, 音色1, track2, 音色2, ...]*)
```

One section consists of an info part and a note part, the info part includes 4 required params(tonality, central note, transposition, tempo) and one optional param(volume number or volume change vector); While the note part contains melodies and chords. The info part follows below format rules:
一个片段由参数域和乐谱域组成，参数域包含4个必要参数（音调、中心音、移调、速度）和一个可选参数（音量 或 音量变化）；其中参数域遵循以下规则：

<div align=center><b>Table 1: Param part format (表 1: 参数域格式)</b><br></div>

| <div style="width:120px;">Format 格式</div>    | Remark 符号                                                                                                                                                                                                                                                                                      |
| :--------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| *{m, c, s, t}*                                 | *m* is 0(major) or 1(minor) 为大小调(0大调，1小调);<br>*c* is central note integer 为中心音 ([0, 11]);<br>*s* is transposing(The whole piece moves up s semitones) 为移调(片段整体移动s个半音);<br>*t* is tempo(the number = a quarter note) 为速度(即乐谱左上角标记的一个四分音符所等于的数字); |
| *{m, c, s, t, v}*                              | *v* is volume 为音量 ([0, 1]);                                                                                                                                                                                                                                                                   |
| *{m, c, s, t, {v<sub>s</sub>, v<sub>t</sub>}}* | Volume fades from *v<sub>s</sub>* to *v<sub>t</sub>* (音量从 *v<sub>s</sub>* 渐变到 *v<sub>t</sub>*)                                                                                                                                                                                             |

The central note list is as follow:

<div align=center><b>Table 2: Central note list (表 2: 中心音表)</b><br></div>

|   C   | C#/Db |   D   | Eb/D# |   E   |   F   | F#/Gb |   G   | Ab/G# |   A   | Bb/A# |   B   |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|   0   |   1   |   2   |   3   |   4   |   5   |   6   |   7   |   8   |   9   |  10   |  11   |

The note part has melodies and chords, which consists of different kinds of notes: 乐谱域由不同种类的音符组成：

<div align=center><b>Table 3: Input formats of notes (表 3: 音符的输入格式)</b><br></div>

| Effect        | Format                                                                | Remark                                                                                                                                    |
| :------------ | :-------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| Rest 休止符   | *{l}*                                                                 | *l* is duration (为时值);                                                                                                                 |
| Tone 音符     | *{n, l}*                                                              | *n* is note value (为音高);                                                                                                               |
| Chord 和弦    | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l}*                            | *n<sub>k</sub>* are chord note values (为和弦上各音符音高);                                                                               |
| Staccato 跳音 | *{n, {l<sub>1</sub>, l<sub>2</sub>}}*                                 | *l<sub>1</sub>* is real duration (为时值), *l<sub>2</sub>* is duration ratio (为缩短后时值占真实时值比率);                                |
| Vibrato 颤音  | *{{n<sub>1</sub>, n<sub>2</sub>}, l<sub>1</sub>, t<sub>n</sub>}*      | *t<sub>n</sub>* is trill number (为抖动次数);                                                                                             |
| Arpeggio 波音 | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l<sub>1</sub>, l<sub>2</sub>}* | *l<sub>2</sub>* is duration ratio (为琶音变化时值占真总时值比);                                                                           |
| Tenuto 延音   | *{bottom note, top notes}*                                            | Bottom note can be a tone or a chord, top notes consist of any above type. 背景音可以是一个音符或一个和弦, 主题旋律可以由上述任何类型组成 |

With these rules, we can get a concise format of notes. 根据以上规则，给出以下音效示例：

<div align=center>
    <b>Table 4: Sound effect demos (表 4: 音效示例)</b><br>
    <img width="605" src="https://user-images.githubusercontent.com/20459298/233112536-f5b900e8-8201-4e9b-9672-43f99b2979f3.PNG"/>
</div>

For notes in the note part, 12-note scheme is unfriendly to us, it can be transferred into 7-note scheme once the tonality is fixed:
对于乐谱域的音符，12音模式使用起来并不方便，一旦调性固定，可将其转为7音模式：

<div align=center>
    <b>Table 5: The 12-note scheme(left) & 7-note scheme(right) 表 5: (左)12音模式 与 (右)7音模式</b><br>
    <img width="500" src="https://user-images.githubusercontent.com/20459298/233112569-3efd5cb1-87c3-44a6-b74b-357104055dd3.png"/>
</div>

Please refer to the demo code _Demo_BWV-1079.nb_ or visit our song library <https://mathmusic.netlify.app> for more details; Before compiling songs, please run the macro package first.
可参考示例代码 _Demo_BWV-1079.nb_ 或浏览 <a href="https://mathmusic.netlify.app" target="_blank">我的Mathematica音乐库</a> 来弄清具体用法; 生成乐谱之前请先运行 _mathematica_music_pack.nb_

Besides, the `e-piano.nb` is a piano keyboard UI, you can play it as a virtual piano on Mathematica.
另外，`e-piano.nb` 是一个编写于 Mathematica 上的钢琴键盘，可作为虚拟钢琴来弹奏。