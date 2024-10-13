# AutoGenBook
AutoGenBook is a Python-based tool that automatically generates books using LLMs. It creates chapters, sections, and subsections recursively based on user-defined content and outputs the final book as a PDF using LaTeX.

## How to Use

### Getting and Setting Up the OpenAI API Key

This tool requires an OpenAI API key. Once you obtain the API key, click on the key icon on the left-hand menu in Google Colab and register it with the name `openai_api`.

### Running the Tool on Google Colab

Click the button below to open the tool in Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hooked-on-mas/AutoGenBook/blob/main/AutoGenBook.ipynb)

日本語で使用したい場合は以下のGoogle Colabを利用してください．

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hooked-on-mas/AutoGenBook/blob/main/AutoGenBookJP.ipynb)

## What’s Inside AutoGenBook

While you can dive into the code for all the details, I realize that it might be a bit hard to follow, so let me explain the basic idea and workflow behind the tool.

### Overview

Since ChatGPT has limitations on how much text it can generate at once, simply asking it to “write a textbook” results in only 1-2 pages of content. To overcome this, AutoGenBook recursively breaks down the structure of a book starting from the main topic or title. It goes from chapters → sections → subsections, and so on. This approach ensures that ChatGPT can generate meaningful, self-contained book for you without hitting its output limit.

Finally, the content for each subdivided section is generated using ChatGPT, and then output as a PDF.

### Workflow

Here’s an outline of the process. I've simplified it by only showing the flow up to the creation of subsections, but the same recursive structure continues for deeper levels.

```mermaid
graph TD
    N[Input specifications] --> A[Generate book title and overview<br>Generate chapter titles and overviews]
    A --> B[(Book title and overview)]
    A --> B1[(Chapter 1 title and overview)]
    A --> B2[(Chapter 2 title and overview)]
    B1 --> BB1[Generate sections for Chapter 1]
    B2 --> BB2[Generate sections for Chapter 2]
    BB1 --> C11[(Section 1.1's title, overview<br>and necessity of division)]
    BB1 --> C12[(Section 1.2's title, overview<br>and necessity of division)]
    BB2 --> C21[(Section 2.1's title, overview<br>and necessity of division)]
    BB2 --> C22[(Section 2.2's title, overview<br>and necessity of division)]
    C11 --> D11{Should it be devided?}
    C12 --> D12{Should it be devided?}
    C21 --> D21{Should it be devided?}
    C22 --> D22{Should it be devided?}
    D11 --> |Yes| E11[Generate subsections of Section 1.1]
    D11 --> |No| F11[Generate content of Section 1.1]
    E11 --> E111[(Subsection 1.1.1's title, overview<br>and necessity of division)]
    E11 --> E112[(Subsection 1.1.2's title, overview<br>and necessity of division)]
    E111 --> F111{Should it be devided?}
    E112 --> F112{Should it be devided?}
    F11 --> FF[(Content of Section 1.1)]
```
