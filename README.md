# mathmusic_macro

[![license](https://img.shields.io/github/license/george-chou/mathmusic_macro.svg)](https://github.com/george-chou/mathmusic_macro/blob/master/LICENSE)
[![Github All Releases](https://img.shields.io/github/downloads/george-chou/mathmusic_macro/total.svg)](https://github.com/george-chou/mathmusic_macro/releases)
[![GitHub release](https://img.shields.io/github/release/george-chou/mathmusic_macro.svg)](https://github.com/george-chou/mathmusic_macro/releases/latest)

A macro package for simplification of composition on Mathematica

## USER MANUAL

For tonal modifying operation, numbers are more convenient than note symbols in Mathematica. There is a one-to-one correspondence between notes and integers shown as the left form below.

<div align=center>
    <b>Table 1: Note scheme</b><br>
    <img width="605" src="cover/t1.png"/>
</div>

The 12-note scheme presents all the notes in a simple format, which is unfriendly to us, while people are used to 7 letters from `C` to `B` once the tonality is certain. The key is to find a map from the 7-note scheme to the 12-note scheme so that people can operate an inconvenient way.

We show inputting formats of different effects in the form below.

<div align=center>
    <b>Table 2: Input formats</b><br>
    <img width="605" src="cover/t2.PNG"/>
</div>

With these rules, we can get a concise format of notes.

<div align=center>
    <b>Table 3: Simplified codes for effects</b><br>
    <img width="605" src="cover/t3.PNG"/>
</div>

We save those notes as vectors, let the computer to estimate their types with the accordance of their inputting formats.

At this time, we can change this score paragraph into whichever tonality you want by replacing the first and the second variate in the function. And you can move the whole song up or down by altering the third variable. But this is still limit for those songs within parts in different tonalities. So, I tried to expend the song vector, let them hold not only one paragraph and the information of each paragraph was previously reserved. The new format of the song is like this.

<div align=center>
    <b>Figure 1: Song format</b><br>
    <img width="605" src="cover/t4.PNG"/>
</div>

The information includes the tonality of the paragraph(major or minor and central note), the offset of the paragraph and the speed while paragraph itself contains notes. I took advantage of this occasion, added some new properties such as volume and volume gradient.

The volume linearly decreases with notes. Information part temporarily contains these properties, its input format follows the rules below.

<div align=center>
    <b>Table 4: Information formats</b><br>
    <img width="605" src="cover/t5.PNG"/>
</div>

For more details, please refer to the demo code `Demo_BWV-1079.nb`; Before compiling songs, please run the macro package first.