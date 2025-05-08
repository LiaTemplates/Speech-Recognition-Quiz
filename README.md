<!--
author:    André Dietrich
email:     liascript@web.de
version:   0.0.1
language:  en
narrator:  US English Female
comment:   Template for SpeechRecognition-powered quizzes in LiaScript
logo:      logo.jpg

@SpeechRecognition.support
<script modify="false" run-once>
// Vendor prefix
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SpeechRecognition) {
  "LIASCRIPT: > 'Speech Recognition' not supported in this browser. Try Chrome, Opera, or Edge.";
} else {
  "LIASCRIPT: > Your browser does support 'Speech Recognition' ..."
}
</script>
@end

@SpeechRecognition
<script>
// Vendor prefix
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SpeechRecognition) {
  alert('SpeechRecognition not supported. Try Chrome, Opera, or Edge.');
} else {
  const recognition = new SpeechRecognition();
  recognition.lang = '@0';
  recognition.interimResults = false;
  recognition.continuous = false;

  const solution = "@1".toLowerCase()
    .replace(/(\.|\?|\!|\,|\-|\;)/g," ")
    .replace(/[ ]+/g," ")
    .trim();

  recognition.onresult = ev => {
    let t = ev.results[0][0].transcript?.toLowerCase().trim() || '';
    if (t === solution) {
      send.lia("true");
    } else {
      send.lia("Please try again …",[],false);
    }
  };
  recognition.onerror = ev => send.lia("Error: "+ev.error,[],false);
  recognition.onend   = () => console.log('Speech recognition ended.');
  recognition.start();
}
"LIA: wait"
</script>
@end

@SpeechRecognition.withFeedback
<script>
// Vendor prefix
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SpeechRecognition) {
  alert('SpeechRecognition not supported. Try Chrome, Opera, or Edge.');
} else {
  const recognition = new SpeechRecognition();
  recognition.lang = '@0';
  recognition.interimResults = false;
  recognition.continuous = false;

  const solution = "@1".toLowerCase()
    .replace(/(\.|\?|\!|\,|\-|\;)/g," ")
    .replace(/[ ]+/g," ")
    .trim();

  recognition.onresult = ev => {
    let t = ev.results[0][0].transcript?.toLowerCase().trim() || '';
    if (t === solution) {
      send.lia("true");
    } else {
      send.lia(t,[],false);
    }
  };
  recognition.onerror = ev => send.lia("Error: "+ev.error,[],false);
  recognition.onend   = () => console.log('Speech recognition ended.');
  recognition.start();
}
"LIA: wait"
</script>
@end
-->

# Speech-Recognition-Quiz Template

                          --{{0}}--
The **SpeechRecognition** API lets you convert spoken words into text right in the browser—no server calls needed. Modern Chromium-based browsers (Chrome, Edge, Opera) support it; Firefox and Safari currently do not.

__Try it on LiaScript:__

https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/Speech-Recognition-Quiz/main/README.md

__See the project on Github:__

https://github.com/liaTemplates/Speech-Recognition-Quiz

                         --{{1}}--
Like with other LiaScript templates, there are three ways to integrate this feature into your project, but the easiest way is to copy the import statement into the header of your LiaScript course.

                           {{1}}
1. Load the latest macros via (this might cause breaking changes)

   `import: https://raw.githubusercontent.com/LiaTemplates/Speech-Recognition-Quiz/refs/heads/main/README.md`

   or the current version 0.0.1 via:

   `import: https://raw.githubusercontent.com/LiaTemplates/Speech-Recognition-Quiz/refs/tags/0.0.1/README.md`

2. __Copy the definitions into your Project__

3. Clone this repository on GitHub

## 1. `@SpeechRecognition.support`

This macro runs once at load time and reports whether the API is available in your learner’s browser.

`@SpeechRecognition.support`

@SpeechRecognition.support

## 2. Language Codes

SpeechRecognition uses [BCP-47 language tags](https://www.rfc-editor.org/rfc/bcp/bcp47.txt). Common examples:

* **en-US**: American English
* **en-GB**: British English
* **de-DE**: German (Germany)
* **fr-FR**: French (France)
* **es-ES**: Spanish (Spain)
* **zh-CN**: Mandarin Chinese (Simplified)
* **ja-JP**: Japanese
* **ar-SA**: Arabic (Saudi Arabia)

You can look up others at [IANA Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry).

## 3. Macro Usage

### `@SpeechRecognition(lang, phrase)`

The `[[!]]` syntax is used to create generic quizzes in LiaScript.
As with all quizzes in LiaScript, you can add hints and a solution and more settings to it, if you want to.
The two parameters that you need to provide are the language code and the phrase you want the learner to say.

- **lang**: BCP-47 code
- **phrase**: expected text (punctuation is ignored)

``` markdown
[[!]]
@SpeechRecognition(en-US,Hello world)
```

**Result:**

[[!]]
@SpeechRecognition(en-US,Hello world)

    {{1}}
<section>

In order to remove the default solution button, you can add the `data-solution-button="off"` attribute to the quiz.
This will hide the solution button and only show the quiz itself.

``` markdown
<!-- data-solution-button="off" -->
[[!]]
@SpeechRecognition(en-US,Hello world)
```

**Result:**

<!-- data-solution-button="off" -->
[[!]]
@SpeechRecognition(en-US,Hello world)

</section>

          --{{2}}--
For more information on quizzes and their settings, please refer to the LiaScript documentation:

{{2}} https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/docs/master/README.md#Further-Settings

### `@SpeechRecognition.withFeedback(lang, phrase)`

          --{{0}}--
This macro works the same way as the one above, but it returns the actual transcript on mismatch.
This is useful for providing feedback to learners.

``` markdown
<!-- data-solution-button="off" -->
[[!]]
@SpeechRecognition.withFeedback(fr-FR,Bonjour le monde)
```

**Result:**

<!-- data-solution-button="off" -->
[[!]]
@SpeechRecognition.withFeedback(fr-FR,Bonjour le monde)

## 4. Examples in Different Languages

Say "Good morning" in American English.

[[!]]
@SpeechRecognition(en-US,`Good morning`)

---

What about "Good morning" in German? 

[[!]]
@SpeechRecognition(de-DE,`Guten Morgen`)

---

French (with feedback): Please say "Je m'appelle Claude".

[[!]]
@SpeechRecognition.withFeedback(fr-FR,`Je m'appelle Claude`)

---

How are you in Spanish?

[[!]]
@SpeechRecognition(es-ES,`Cómo estás?`)

---

Mandarin Chinese, please say "你好世界" (Nǐ hǎo shìjiè).


[[!]]
@SpeechRecognition.withFeedback(zh-CN,`你好世界`)

## Implementation

                        --{{0}}--
If you want to minimize loading effort in your LiaScript project, you can also copy this code and paste it into your main comment header, but this is the entire implementation.

``` html
@SpeechRecognition.support
<script modify="false" run-once>
// Vendor prefix
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SpeechRecognition) {
  "LIASCRIPT: > 'Speech Recognition' not supported in this browser. Try Chrome, Opera, or Edge.";
} else {
  "LIASCRIPT: > Your browser does support 'Speech Recognition' ..."
}
</script>
@end

@SpeechRecognition
<script>
// Vendor prefix
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SpeechRecognition) {
  alert('SpeechRecognition not supported. Try Chrome, Opera, or Edge.');
} else {
  const recognition = new SpeechRecognition();
  recognition.lang = '@0';
  recognition.interimResults = false;
  recognition.continuous = false;

  const solution = "@1".toLowerCase()
    .replace(/(\.|\?|\!|\,|\-|\;)/g," ")
    .replace(/[ ]+/g," ")
    .trim();

  recognition.onresult = ev => {
    let t = ev.results[0][0].transcript?.toLowerCase().trim() || '';
    if (t === solution) {
      send.lia("true");
    } else {
      send.lia("Please try again …",[],false);
    }
  };
  recognition.onerror = ev => send.lia("Error: "+ev.error,[],false);
  recognition.onend   = () => console.log('Speech recognition ended.');
  recognition.start();
}
"LIA: wait"
</script>
@end

@SpeechRecognition.withFeedback
<script>
// Vendor prefix
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SpeechRecognition) {
  alert('SpeechRecognition not supported. Try Chrome, Opera, or Edge.');
} else {
  const recognition = new SpeechRecognition();
  recognition.lang = '@0';
  recognition.interimResults = false;
  recognition.continuous = false;

  const solution = "@1".toLowerCase()
    .replace(/(\.|\?|\!|\,|\-|\;)/g," ")
    .replace(/[ ]+/g," ")
    .trim();

  recognition.onresult = ev => {
    let t = ev.results[0][0].transcript?.toLowerCase().trim() || '';
    if (t === solution) {
      send.lia("true");
    } else {
      send.lia(t,[],false);
    }
  };
  recognition.onerror = ev => send.lia("Error: "+ev.error,[],false);
  recognition.onend   = () => console.log('Speech recognition ended.');
  recognition.start();
}
"LIA: wait"
</script>
@end
```