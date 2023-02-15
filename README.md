# Mathematica-Music-Pack

[![license](https://img.shields.io/github/license/george-chou/Mathematica-Music-Pack.svg)](https://github.com/george-chou/Mathematica-Music-Pack/blob/master/LICENSE)
[![CI](https://github.com/george-chou/Mathematica-Music-Pack/workflows/CI/badge.svg?branch=master)](https://github.com/george-chou/Mathematica-Music-Pack/actions)

A macro package for simplifying composition on Mathematica

## User manual

We use vectors and numbers to replace complicated SoundNote[] functions. A complete song has many sections, its format is as follow:

```
song = {
    {info part of section 1},
    {note part of section 1},

    {info part of section 2},
    {note part of section 2},

    ...

    {info part of section n},
    {note part of section n}
};
```

One section consists of an info part and a note part, the info part includes 4 required params(tonality, central note, transposition, tempo) and one optional param(volume number or volume change vector); While the note part contains melodies and chords. The info part follows below format rules:

<div align=center><b>Table 1: Info part format</b><br></div>

| <div style="width:120px;">Format</div>         | Remark                                                                                                                                                                      |
| ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| *{m, c, s, t}*                                 | *m* is 0(major) or 1(minor);<br>*c* is central note integer([0, 11]);<br>*s* is transposition(Aborted function, usually = 0);<br>*t* is tempo(the number = a quarter note); |
| *{m, c, s, t, v}*                              | *v* is volume([0, 1]);                                                                                                                                                      |
| *{m, c, s, t, {v<sub>s</sub>, v<sub>t</sub>}}* | Volume fades from *v<sub>s</sub>* to *v<sub>t</sub>*                                                                                                                        |

The central note list is as follow:

<div align=center><b>Table 2: Central note list</b><br></div>

| C   | C#/Db | D   | Eb/D# | E   | F   | F#/Gb | G   | Ab/G# | A   | Bb/A# | B   |
| --- | ----- | --- | ----- | --- | --- | ----- | --- | ----- | --- | ----- | --- |
| 0   | 1     | 2   | 3     | 4   | 5   | 6     | 7   | 8     | 9   | 10    | 11  |

The note part has melodies and chords, which consists of different kinds of notes:

<div align=center><b>Table 3: Input formats of notes</b><br></div>

| Effect   | Format                                                                | Remark                                                                     |
| -------- | --------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Rest     | *{l}*                                                                 | *l* is duration;                                                           |
| Tone     | *{n, l}*                                                              | *n* is note value;                                                         |
| Chord    | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l}*                            | *n<sub>k</sub>* are chord note values;                                     |
| Staccato | *{n, {l<sub>1</sub>, l<sub>2</sub>}}*                                 | *l<sub>1</sub>* is real duration, *l<sub>2</sub>* is duration ratio;       |
| Vibrato  | *{{n<sub>1</sub>, n<sub>2</sub>}, l<sub>1</sub>, t<sub>n</sub>}*      | *t<sub>n</sub>* is trill number;                                           |
| Arpeggio | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l<sub>1</sub>, l<sub>2</sub>}* | *l<sub>2</sub>* is duration ratio;                                         |
| Tenuto   | *{bottom note, top notes}*                                            | Bottom note can be a tone or a chord, top notes consist of any above type. |

With these rules, we can get a concise format of notes.

<div align=center>
    <b>Table 4: Sound effect demos</b><br>
    <img width="605" src="https://picrepo.netlify.app/Mathematica-Music-Pack/t3.PNG"/>
</div>

For notes in the note part, 12-note scheme is unfriendly to us, it can be transferred into 7-note scheme once the tonality is fixed:

<div align=center>
    <b>Table 5: The 12-note scheme(left) & 7-note scheme(right)</b><br>
    <img width="500" src="https://picrepo.netlify.app/Mathematica-Music-Pack/t1.png"/>
</div>

Please refer to the demo code _Demo_BWV-1079.nb_ or visit our song library <https://mathmusic.netlify.app> for more details; Before compiling songs, please run the macro package first.

Besides, the `e-piano.nb` is a piano keyboard UI, you can play it as a virtual piano on Mathematica.