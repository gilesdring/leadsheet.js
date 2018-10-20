# js-leadsheet #

This is a formatter for simple [lead sheets][WLS], and it currently supports creation
of chord boxes and annotation of changes over lyrics, as well as simple instrumental
chord sequences. It does what I need it to at the moment...

It's written as a node.js bin module for command line usage, but you can also import
``leadsheet.js`` directly to use client-side.

The concept was inspired by [Markdown][MD].

[WLS]: http://en.wikipedia.org/wiki/Lead_sheet "Link to article about lead sheets on wikipedia"
[MD]: http://daringfireball.net/projects/markdown/ "Link to Markdown on Daring Fireball"

## Examples ##

The following

    Title: My Song  
    Artist: Me  

    + Cref x,3,2,0,1,0 C  

    Verse 1=  
    This is my [Cref]song  
    It's not too [Dref]long

    Chorus =  
    So hear my [Eref]song  
    And now it's [Cref]gone  

Renders to

<html>
<style>.leadsheet { width: 210mm; padding: 20mm; } /* Page setup */.header { text-align: center; padding-bottom: 2em; }.title { font-size: 2em; font-weight: bold; }.artist { font-size: 1.5em; }.chords { text-align: center; padding-bottom: 2em; }.chord { display: inline; }.chordbox { width: 2cm; height: 2cm; }.chordbox text.fretmarker { font-size: 60%; font-style: italic; dominant-baseline: central; text-anchor: end; }.chordbox text.chordname { text-anchor: middle; }.chordbox circle.fretted { fill: black; stroke: black; }.chordbox circle.open { fill: none; stroke: black; }.chordbox line, .chordbox path { stroke-linecap: square; stroke: black; }.chordbox line.fret { }.chordbox line.nut { stroke-width: 2px; }.chordbox line.string { }.chordbox path.unplayed { }.stanza { padding-bottom: 2em; }.repeat { display: inline-block; float: right; font-style: italic; }.repeat:before { content: 'repeat x '; }.stanzaline { }.withchords { padding-top: 1em; }.stanzaname { font-style: italic; }.stanzaname:after { content: ':'; }.barsystem { border-left: 2px solid; margin: 0 0 1ex 0; }.bar { border-right: 2px solid; display: inline-block; width: 7em; padding: 0 1em; text-align: center; }.barelement { display: inline-block; padding: 0 5px; }.lyric { display: inline; }.chordref { width: 0; display: inline-block; position: relative; top: -1em; text-align: center; vertical-align: baseline; }.undefined { color: red; }</style>
<div class='leadsheet'>
  <div class='header'>
    <div class='title'>My Song</div>
    <div class='artist'>Me</div>
  </div>
  <div class='chords'>
    <div class='chord'><svg xmlns='http://www.w3.org/2000/svg' version='1.1' class='chordbox'><defs><circle id='open_eb569517-ff73-4b63-aa57-7fd230ff1b6c' class='open' cx='0' cy='-5' r='3'></circle><circle id='fretted_eb569517-ff73-4b63-aa57-7fd230ff1b6c' class='fretted' cx='0' cy='-5' r='2.5'></circle><path id='unplayed_eb569517-ff73-4b63-aa57-7fd230ff1b6c' class='unplayed' d='M -3 -8 l 6 6 m -6 0 l 6 -6'></path><line id='string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' class='string' x1='0' y1='0' x2='0' y2='40'></line><line id='fret_eb569517-ff73-4b63-aa57-7fd230ff1b6c' class='fret' x1='0' y1='0' x2='35' y2='0'></line><line id='nut_eb569517-ff73-4b63-aa57-7fd230ff1b6c' class='nut' x1='0' y1='0' x2='35' y2='0'></line></defs><g transform='translate(25,25)'><text class='chordname' x='17.5' y='-13'>C</text><use xlink:href='#nut_eb569517-ff73-4b63-aa57-7fd230ff1b6c' y='0'></use><use xlink:href='#fret_eb569517-ff73-4b63-aa57-7fd230ff1b6c' y='10'></use><use xlink:href='#fret_eb569517-ff73-4b63-aa57-7fd230ff1b6c' y='20'></use><use xlink:href='#fret_eb569517-ff73-4b63-aa57-7fd230ff1b6c' y='30'></use><use xlink:href='#fret_eb569517-ff73-4b63-aa57-7fd230ff1b6c' y='40'></use><use xlink:href='#string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='0'></use><use xlink:href='#unplayed_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='0' y='0'></use><use xlink:href='#string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='7'></use><use xlink:href='#fretted_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='7' y='30'></use><use xlink:href='#string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='14'></use><use xlink:href='#fretted_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='14' y='20'></use><use xlink:href='#string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='21'></use><use xlink:href='#open_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='21' y='0'></use><use xlink:href='#string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='28'></use><use xlink:href='#fretted_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='28' y='10'></use><use xlink:href='#string_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='35'></use><use xlink:href='#open_eb569517-ff73-4b63-aa57-7fd230ff1b6c' x='35' y='0'></use></g></svg></div>
  </div>
  <div class='stanzas'>
    <div class='stanza'>
      <div class='stanzaname'>Verse 1</div>
      <div class='stanzaline withchords'><div class='lyric'>This is my </div><div class='chordref'>C</div><div class='lyric'>song</div></div>
      <div class='stanzaline withchords'><div class='lyric'>It's not too </div><div class='chordref undefined'>Dref</div><div class='lyric'>long</div></div>
    </div>
    <div class='stanza'>
      <div class='stanzaname'>Chorus</div>
      <div class='stanzaline withchords'><div class='lyric'>So hear my </div><div class='chordref undefined'>Eref</div><div class='lyric'>song</div></div>
      <div class='stanzaline withchords'><div class='lyric'>And now it's </div><div class='chordref'>C</div><div class='lyric'>gone</div></div>
    </div>
  </div>
</div>
</html>
