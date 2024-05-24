---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides, markdown enabled
title: Intro to AI
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true

---

# Intro to AI

<!--
slides notes
-->

---

# Table of Contents
- 1. Intro to AI
  - 1.1 What are intelligence?
  - 1.2 history of AI
  - 1.3 Basic categories of AI
  - 1.4 AI research Pathways
- 2. LLMs
  - 2.1 classical AI
  - 2.2 NLP
  - 2.3 Applications of LLM
  - 2.4 classical models behind LLMs
    - 2.4.1 Transformer
    - Pros vs Cons

---

# source
[什么是大模型？一文读懂大模型的基本概念](https://xie.infoq.cn/article/c73d7cd6c89fa88279e6e0afe)

[MOOC - 人工智能基础](https://www.icourse163.org/course/NUDT-1466045161)

[人工智能(AI)定义、原理及应用简介](https://zhuanlan.zhihu.com/p/646163153)

[浙大团队撰写75页科学语言大模型综述，全面梳理Sci-LLMs最新研究进展](https://zhuanlan.zhihu.com/p/681078251)

---

# 1.1 What are intelligence?
## **Intelligence**:
  the capacity for abstraction, logic, understanding, self-awareness, learning, emotional knowledge, reasoning, planning, creativity, critical thinking, and problem-solving. It can be described as the ability to perceive or infer information; and to retain it as knowledge to be applied to adaptive behaviors within an environment or context.
 **AI**: Machines mimicking human intelligence.

---

# 1.2 history of AI
AI development timeline.

Tree of LLM.

---

# 1.3 Basic Content of AI

**Machine Learning**: Algorithms that learn from data. 

**Neural Networks**: Brain-inspired systems for pattern recognition.

**Deep Learning**: Complex neural networks for advanced tasks.


**Computer Vision**: ...

**Natural Language Processing**: ...

---

# 2. LLMs

## 2.1 Classical AI

**Symbolic AI**: Early AI focused on rules and logic.

**Expert Systems**: AI that mimics decision-making of a human expert.

---

## 2.2 NLP (Natural Language Processing)

---

## 2.3 Applications of LLMs

**Chatbots**: Conversational agents (e.g., virtual assistants).

**Content Creation**: Generating articles, stories, and more.

**Education**: Personalized learning and tutoring.

---

## 2.4 Classical Models Behind LLMs

### 2.4.1 Transformer
**Transformer**: Model architecture enabling powerful language models.
**Key Feature**: Attention mechanism to focus on important parts of input.

### Pros vs Cons
- **Pros**:
  - Highly effective for language understanding.
  - Scalable to massive datasets.
- **Cons**:
  - Requires significant computational resources.
  - Can produce biased or incorrect outputs.




---

# At the end - Example
## Prompt
System prompt:
```md
Now you are a colour palette generator, and you should respond to text prompts.
I will give you one or two short sentences or phrases to describe the object,
in which I may specify the number of colours you should generate and I may add
more restrictions. Your should generate color palettes that fit the theme, mood, 
or instructions in the prompt. You should generate between 2 to 8 colours 
unless I tell you otherwise. You could check some websites like Pinterest or
U.S. brand colours, BrandColors, or wikipedia on Pantone colour chart. Give
the most official colour ever possible. You don"t need to explain anything,
just give the output.
## Desired format ##
- **output**: `<Json array of string>`
You need to return a Json array of string in Python, where each string is a
hexadecimal colour code for your chosen colour.
```

---
## Fine-tuning
&emsp; With multiple-shot:
```
## Examples ##
Q: Mcdonald's sign colours
A: '["#FFC72C", "#DA291C"]'

Q: rainbow
A: '["#FF0000", "#FF7F00", "#FFFF00", "#00FF00", "#0000FF", "#4B0082", "#9400D3"]'
```

---

## Invoke OpenAI API:
```python {2|3-7|8-12|all}{lines:true}
api_key = dotenv_values(".env")["OPENAI_API_KEY"]
    client = OpenAI(api_key=api_key)
    message_lst = [{"role": "system",
                      "content":f"{system_prompt}"},
                    {"role": "system",
                      "content":f"{fine_tuning_prompt}"}]
    message_lst.append({"role": "user", "content": f"{prompt}"})
    response = client.chat.completions.create(
        messages=message_lst,
        model="gpt-3.5-turbo-0125",
        max_tokens=200,
    )
    return response.choices[0].message.content
```

## Result:
```python
["#FDE87A", "#FFC679", "#FFA87D", "#F3959D", "#A9C8C8", "#93A2A9"]
```

## Render through IPython
<div style="display: flex;"><div style="background-color: #FDE87A; width: 100px; height: 100px;"></div><div style="background-color: #FFC679; width: 100px; height: 100px;"></div><div style="background-color: #FFA87D; width: 100px; height: 100px;"></div><div style="background-color: #F3959D; width: 100px; height: 100px;"></div><div style="background-color: #A9C8C8; width: 100px; height: 100px;"></div><div style="background-color: #93A2A9; width: 100px; height: 100px;"></div></div>

---
# Project:
+ chatBox
  1. take in files
  2. chatBox asks input to create your own resume
  3. take in resume to produce cover letter
     1. based on resume + jd  
  4. deploy the app to the web
