# AutoGenBook
AutoGenBook 是一个基于 Python 的工具，使用 LLM（大型语言模型）自动生成书籍。根据用户指定的内容，递归地生成章节、小节，并最终通过 LaTeX 以 PDF 格式输出。

## 使用方法

### 获取和设置 OpenAI API 密钥

此工具需要 OpenAI 的 API 密钥。获取密钥后，请点击 Google Colab 左侧菜单中的钥匙图标，并以 `openai_api` 的名称注册。

![image](https://github.com/user-attachments/assets/64e3ad1b-9eb9-4746-8485-e3318e269573)

### 在 Google Colab 上运行工具

点击以下按钮在 Google Colab 上打开工具：

[![在Colab中打开](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hooked-on-mas/AutoGenBook/blob/main/AutoGenBookCN.ipynb)

## 教科书示例

可以在这里以 PDF 格式查看生成的教科书示例“线性代数与机器学习：从理论到实践”：

[前往Google Drive](https://drive.google.com/file/d/1n3lnKkex9fLdmMoXYENnE52Au0XH9dkz/view?usp=sharing)

## AutoGenBook 的内容

尽管详细内容可在程序中查看，但以下是简单的想法和处理流程。

### 基本思路

由于 ChatGPT 的输出量有限，即使请求“生成教科书”，也只能输出 1-2 页的内容。因此，以书的主题或标题为起点，递归地将其划分为大标题（章）、中标题（节）、小标题（项）等独立部分。这种方法使得我们可以在不受 ChatGPT 输出量限制的情况下自动生成书的整体结构。最终，每个小区块的内容将通过 ChatGPT 生成并以 PDF 格式输出。

这种方法类似于人在编写书籍或论文时，先制定章节结构再开始实际撰写内容，属于自然的思路。

### 处理流程

下图展示了大致的处理流程，其中部分相同的步骤已省略，且分割流程仅至小标题的生成为止。

```mermaid
graph TD
    N[输入需求] --> A[生成书籍标题及概要<br>生成章节标题及概要]
    A --> B[(书籍标题及概要)]
    A --> B1[(第1章标题及概要)]
    A --> B2[(第2章标题及概要)]
    B1 --> BB1[生成第1章的小节]
    B2 --> BB2[生成第2章的小节]
    BB1 --> C11[(1.1节标题及概要<br>是否需分割)]
    BB1 --> C12[(1.2节标题及概要<br>是否需分割)]
    BB2 --> C21[(2.1节标题及概要<br>是否需分割)]
    BB2 --> C22[(2.2节标题及概要<br>是否需分割)]
    C11 --> D11{需要分割吗？}
    C12 --> D12{需要分割吗？}
    C21 --> D21{需要分割吗？}
    C22 --> D22{需要分割吗？}
    D11 --> |是| E11[生成1.1节项]
    D11 --> |否| F11[生成1.1节内容] 
    E11 --> E111[(1.1.1项标题及概要<br>是否需分割)]
    E11 --> E112[(1.1.2项标题及概要<br>是否需分割)]
    E111 --> F111{需要分割吗？}
    E112 --> F112{需要分割吗？}
    F11 --> FF[(1.1节内容)]
```

### 实际生成的文本结构

以下是实际输出的约 12 页书籍的文本结构。箭头从 book 指向的 1、2、3、4 表示章节，其下方为小节，再下方为小标题。这些节点包含章节和小节的标题及概要信息。用红色圆点表示的末端节点则包含正文内容信息。
![section_structure.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/178972/256d643c-fef6-3872-d894-ea2efd487932.png)