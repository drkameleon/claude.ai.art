<h1 align="center">
    Claude.ai
</h1>

<p align="center">
     <i>A clean & intuitive,<br>Anthropic Claude API wrapper for Arturo</i> 
     <br><br>
     <img src="https://img.shields.io/github/license/drkameleon/claude.ai.art?style=for-the-badge">
    <a href="https://github.com/arturo-lang/arturo" style="text-decoration: none; display: inline-block;"><img src="https://img.shields.io/badge/language-Arturo-6A156B.svg?style=for-the-badge" alt="Language"/></a>
</p>


--- 
 
<!--ts-->

* [What does this package do?](#what-does-this-package-do)
* [How do I use it?](#how-do-i-use-it)
* [API Reference](#api-reference)
* [Type Reference](#type-reference)
* [License](#license)   

<!--te-->
 
---

### What does this package do?

This package provides a clean wrapper around [Anthropic's Claude API](https://www.anthropic.com/api), allowing you to easily integrate Claude's capabilities into your Arturo applications. It handles all the API communication, message formatting, and response parsing, providing both low-level access to the full API and convenient high-level methods for common use cases.

### How do I use it?

First, make sure you have an API key from Anthropic. Then simply `import` the package and initialize a client:

```red
import "claude"!

; Initialize with your API key (defaults to Sonnet 4.6)
claude: to :claudeAPI @["sk-your-api-key"]!

; Ask a simple question
answer: claude\ask "What is the capital of France?"
print answer

; Have a more complex conversation
response: claude\chat [
    createMessage "user" "What's quantum computing?"
    createMessage "assistant" "Quantum computing uses quantum mechanics..."
    createMessage "user" "Can you explain qubits?"
]

; Use custom parameters
response: claude\chat
  .temperature: 0.9
  .maxTokens: 2000
  .system: "You are a creative writing expert"
[
    createMessage "user" "Write a creative story"
]
```

#### Model Selection

By default, the client uses **Claude Sonnet 4.6**. You can select a different model family at initialization using attributes:

```red
; Use Claude Opus 4.6
claude: to .opus :claudeAPI @["sk-your-api-key"]!

; Use Claude Haiku 4.5
claude: to .haiku :claudeAPI @["sk-your-api-key"]!
```

> [!TIP]
> You can also change the model at any time after initialization using `setModel`, or override it per-request via the `.model` attribute on `chat`.

### API Reference

#### `claudeAPI`

##### Description

The main client class for interacting with Claude's API.

##### Initialization

<pre>
<b>to</b> <i>:claudeAPI</i> [<ins>key</ins> <i>:string</i>]
</pre>

**Attributes**

| Option | Type | Description |
|----|----|----|
| opus | :logical | Use Claude Opus 4.6 |
| haiku | :logical | Use Claude Haiku 4.5 |

> [!NOTE]
> If neither `.opus` nor `.haiku` is specified, the client defaults to **Claude Sonnet 4.6** (`claude-sonnet-4-6`).

##### Methods

###### `chat`

Send messages to Claude and get responses.

<pre>
<b>chat</b> <ins>messages</ins> <i>:block</i>
</pre>

**Attributes**

| Option | Type | Description |
|----|----|----|
| model | :string | Specify Claude model to use (default: claude-sonnet-4-6) |
| system | :string | Specify system message |
| temperature | :floating | Set temperature (0.0-1.0) |
| maxTokens | :integer | Set max tokens for response |
| topP | :floating | Set top_p value (0.0-1.0) |
| topK | :integer | Set top_k value |

**Returns**
- *:dictionary* - The complete API response

###### `ask`

Simplified method for single-turn questions.

<pre>
<b>ask</b> <ins>question</ins> <i>:string</i>
</pre>

**Returns**
- *:string* - Claude's response text

###### Configuration Methods

- `setModel [model :string]` - Set default model
- `setMaxTokens [tokens :integer]` - Set default max tokens
- `setTemperature [temp :floating]` - Set default temperature
- `setTopP [topP :floating]` - Set default top_p

### Type Reference

#### `message`

##### Description

Represents a single message in a conversation.

##### Usage

```red
msg: createMessage "user" "Hello, Claude!"
```

or

```red
msg: to :message ["user" "This is my message"]
```

##### Fields
- `role` - Either "user" or "assistant"
- `content` - The message content

<hr/>

### License

MIT License

Copyright (c) 2026 Yanis Zafirópulos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
