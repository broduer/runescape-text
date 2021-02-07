# RuneScape Text

[![Discord](https://discord.com/api/guilds/258167954913361930/embed.png)](https://discord.gg/WjEFnzC) [![Twitter Follow](https://img.shields.io/twitter/follow/peterthehan.svg?style=social)](https://twitter.com/peterthehan)

Convert text to a text image with [RuneScape](https://www.runescape.com/) chat effects.

<div align="center">
  <img src="https://raw.githubusercontent.com/peterthehan/runescape-text/master/assets/demo.png" title="Default styling" alt="Default styling" />
</div>

<div align="center">
  <img src="https://raw.githubusercontent.com/peterthehan/runescape-text/master/assets/demo.gif" title="Selling rune scimmy 15k" alt="Selling rune scimmy 15k" />
</div>

Refer to this wikiHow guide on [How to Write Text Effects on RuneScape](https://www.wikihow.com/Write-Text-Effects-on-Runescape).

## Table of contents

- [Install](#install)
  - [Globally](#globally)
  - [Locally](#locally)
- [Syntax](#syntax)
  - [Parameters](#parameters)
    - [Options](#options)
    - [WordWrapOptions](#wordwrapoptions)
  - [Return value](#return-value)
  - [Exceptions](#exceptions)
- [Help](#help)

## Install

### Globally

```
$ npm i -g runescape-text
```

```
$ runescape-text "wave:glow3: hello world"
```

### Locally

```
$ npm i runescape-text
```

```js
const fs = require("fs");
const getRuneScapeText = require("runescape-text");

async function main() {
  const string = "wave:glow3: hello world";
  const options = { showLogs: true };

  const { extension, buffer } = getRuneScapeText(string, options);

  fs.writeFileSync(`./runescape-text.${extension}`, await buffer);
}

main();
```

## Syntax

```js
getRuneScapeText(string, [options], [wordWrapOptions]);
```

### Parameters

| Parameter                           | Type     | Required | Default | Description                                                                           |
| ----------------------------------- | -------- | -------- | ------- | ------------------------------------------------------------------------------------- |
| string                              | `string` | Yes      | _none_  | Text to convert                                                                       |
| [options](#options)                 | `Object` | No       | `{}`    | Options to configure script behavior                                                  |
| [wordWrapOptions](#wordwrapoptions) | `Object` | No       | `{}`    | Options to configure [word-wrap](https://github.com/jonschlinkert/word-wrap) behavior |

#### Options

| Property         | Type      | Required | Default    | Description                                                    |
| ---------------- | --------- | -------- | ---------- | -------------------------------------------------------------- |
| version          | `string`  | No       | `"osrs"`   | Game version to use [0]                                        |
| color            | `string`  | No       | `"yellow"` | Color effect of the text [1]                                   |
| motion           | `string`  | No       | `"none"`   | Motion effect of the text [2]                                  |
| suffix           | `string`  | No       | `":"`      | String that should suffix each color and motion string         |
| replacement      | `string`  | No       | `""`       | String to replace characters the font does not support         |
| maxMessageLength | `number`  | No       | `280`      | Max message length allowed after the string has been sanitized |
| scale            | `number`  | No       | `2`        | Scale factor of the font (multiples of 16px) [3]               |
| fps              | `number`  | No       | `20`       | Frames per second to render GIFs at [4]                        |
| cycleDuration    | `number`  | No       | `3000`     | Duration of one cycle before the GIF loops                     |
| quality          | `number`  | No       | `100`      | Quality to render GIFs at [5]                                  |
| showLogs         | `boolean` | No       | `false`    | Determines whether to print runtime logs or not                |

[0] Must be: `osrs` or `rs3`.

[1] Must be: `yellow`, `red`, `green`, `cyan`, `purple`, `white`, `glow1`, `glow2`, `glow3`, `flash1`, `flash2`, or `flash3`.

[2] Must be: `none`, `wave`, `wave2`, `shake`, `scroll`, or `slide`.

[3] Impacts rendering times. Prefer integer values greater than or equal to 1, decimal values will render blurry text.

[4] Impacts rendering times. Prefer integer values less than or equal to 60.

[5] Impacts rendering times. More information [here](https://github.com/twolfson/gif-encoder#setqualityquality).

#### WordWrapOptions

Property information can be found [here](https://github.com/jonschlinkert/word-wrap#options). The defaults chosen by this module are listed below:

| Property | Default                  |
| -------- | ------------------------ |
| width    | `50`                     |
| indent   | `""`                     |
| newline  | `"\n"`                   |
| escape   | `(str) => str.trimEnd()` |
| trim     | `false`                  |
| cut      | `false`                  |

### Return value

The **return value** is an Object with the following properties:

| Property  | Type              | Description                            |
| --------- | ----------------- | -------------------------------------- |
| width     | `number`          | Image width                            |
| height    | `number`          | Image height                           |
| extension | `string`          | File extension, either: `png` or `gif` |
| buffer    | `Promise<Buffer>` | Promise resulting in an image buffer   |

### Exceptions

| Error                  | Description                                   |
| ---------------------- | --------------------------------------------- |
| `InvalidArgumentError` | Thrown if required string argument is missing |
| `TypeError`            | Thrown if argument type is unexpected         |
| `ValueError`           | Thrown if string is empty                     |
| `ValueError`           | Thrown if the parsed message string is empty  |

## Help

Visit for more help or information!

<a href="https://discord.gg/WjEFnzC">
  <img src="https://discord.com/api/guilds/258167954913361930/embed.png?style=banner2" title="Discord server invite" alt="Discord server invite" />
</a>
