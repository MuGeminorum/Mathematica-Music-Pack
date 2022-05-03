# mathmusic_macro

[![license](https://img.shields.io/github/license/george-chou/mathmusic_macro.svg)](https://github.com/george-chou/mathmusic_macro/blob/master/LICENSE)
[![CI](https://github.com/george-chou/mathmusic_macro/workflows/CI/badge.svg?branch=master)](https://github.com/george-chou/mathmusic_macro/actions)

A macro package for simplifying composition on Mathematica

## User manual

We use vectors and numbers to replace complicated SoundNote functions. A complete song has many sections, its format is as follow:

```
song = {
    {info of paragraph 1},
    {paragraph 1},

    {info of paragraph 2},
    {paragraph 2},

    ...

    {info of paragraph n},
    {paragraph n},
};
```

One section consists of an info part and a note part, the info part includes 4 required params(tonality, central note, transposition, tempo) and one optional param(volume number or volume change vector); While the note part contains melodies and chords. The info part follows below format rules:

<div align=center><b>Table 1: Info part format</b><br></div>

| Format                                         | Remark                                                                                                                                                             |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| *{m, c, s, t}*                                 | *m* is 0(major) or 1(minor); *c* is central note integer([0, 11]); *s* is transposition(Aborted function, usually = 0); *t* is tempo(the number = a quarter note); |
| *{m, c, s, t, v}*                              | *v* is volume;                                                                                                                                                     |
| *{m, c, s, t, {v<sub>s</sub>, v<sub>t</sub>}}* | *v<sub>s</sub>* is volume at the beginning; *v<sub>t</sub>* is volume at the end.                                                                                  |

The central note list is as follow:
<div align=center><b>Table 2: Central note list</b><br></div>
| C   | C#/Db | D   | Eb/D# | E   | F   | F#/Gb | G   | Ab/G# | A   | Bb/A# | B   |
| --- | ----- | --- | ----- | --- | --- | ----- | --- | ----- | --- | ----- | --- |
| 0   | 1     | 2   | 3     | 4   | 5   | 6     | 7   | 8     | 9   | 10    | 11  |

The note part has melodies and chords, which consists of different kinds of notes:

<div align=center><b>Table 3: Input formats of notes</b><br></div>

| Effect   | Format                                                                | Remark                                                                         |
| -------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Rest     | *{l}*                                                                 | *l* is beat number;                                                            |
| Tone     | *{n, l}*                                                              | *n* is note number;                                                            |
| Chord    | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l}*                            | *n<sub>k</sub>* are note numbers of the chord;                                 |
| Staccato | *{n, {l<sub>1</sub>, l<sub>2</sub>}}*                                 | *l<sub>1</sub>* is beat number, *l<sub>2</sub>* is the ratio of real duration; |
| Vibrato  | *{{n<sub>1</sub>, n<sub>2</sub>}, l<sub>1</sub>, t<sub>n</sub>}*      | *t<sub>n</sub>}* is trill number;                                              |
| Arpeggio | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l<sub>1</sub>, l<sub>2</sub>}* | *l<sub>2</sub>* is  the ratio of real duration;                                |
| Tenuto   | *{bottom notes, {top notes}}*                                         | Bottom notes can be tones or chords, top note can be any above type.           |

With these rules, we can get a concise format of notes.

<div align=center>
    <b>Table 4: Sound effect demos</b><br>
    <img width="605" src="https://george-chou-github-io.vercel.app/covers/mathmusic_macro/t3.PNG"/>
</div>

For notes in the note part, using 12-note scheme is unfriendly to us, it can be transferred into 7-note scheme from _C_ to _B_ once the tonality is fixed:

<div align=center>
    <b>Table 5: Note scheme</b><br>
    <img width="500" src="https://george-chou-github-io.vercel.app/covers/mathmusic_macro/t1.png"/>
</div>

Please refer to the demo code _Demo_BWV-1079.nb_ or visit our song library <https://mathmusic.vercel.app> for more details; Before compiling songs, please run the macro package first.

Besides, the `e-piano.nb` is a piano keyboard UI code, you can play it as a virtual piano on software.