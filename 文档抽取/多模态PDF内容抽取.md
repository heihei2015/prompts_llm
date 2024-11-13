# 视觉语言大模,抽取PDF内容

参考公众号文章[强烈推荐！一条OCR Prompt复杂布局PDF秒变Markdown，表格跨页也不惧](https://mp.weixin.qq.com/s/3jcedVr6PatYD424WC3jpg)

```markdown
You are tasked with transcribing and formatting the content of a file into markdown. Your goal is to create a well-structured, readable markdown document that accurately represents the original content while adding appropriate formatting and tags.


Follow these instructions to complete the task:

1. Carefully read through the entire file content.

2. Transcribe the content into markdown format, paying close attention to the existing formatting and structure.

3. If you encounter any unclear formatting in the original content, use your judgment to add appropriate markdown formatting to improve readability and structure.

4. For tables, headers, and table of contents, add the following tags:
   - Tables: Enclose the entire table in [TABLE] and [/TABLE] tags. Merge content of tables if it is continued in the next page.
   - Headers (complete chain of characters repeated at the start of each page): Enclose in [HEADER] and [/HEADER] tags inside the markdown file.
   - Table of contents: Enclose in [TOC] and [/TOC] tags

5. When transcribing tables:
   - If a table continues across multiple pages, merge the content into a single, cohesive table.
   - Use proper markdown table formatting with pipes (|) and hyphens (-) for table structure.

6. Do not include page breaks in your transcription.

7. Maintain the logical flow and structure of the document, ensuring that sections and subsections are properly formatted using markdown headers (# for main headers, ## for subheaders, etc.).

8. Use appropriate markdown syntax for other formatting elements such as bold, italic, lists, and code blocks as needed.

10. Return only the parsed content in markdown format, including the specified tags for tables, headers, and table of contents.
```

## 中英对照
```markdown
您的任务是将文件内容转录并格式化为 markdown。您的目标是创建一个结构良好、可读性强的 markdown 文档，该文档准确表示原始内容，同时添加适当的格式和标签。

请按照以下说明完成任务：

1. 仔细阅读整个文件内容。

2. 将内容转录为 markdown 格式，密切关注现有的格式和结构。

3. 如果您在原始内容中发现任何不清楚的格式，请自行判断添加适当的 markdown 格式以提高可读性和结构。

4. 对于表格、标题和目录，请添加以下标签：
- 表格：将整个表格括在 [TABLE] 和 [/TABLE] 标签中。如果表格内容在下一页继续，请合并表格内容。
- 标题（在每页开头重复的完整字符串）：括在 markdown 文件内的 [HEADER] 和 [/HEADER] 标签中。
- 目录：用 [TOC] 和 [/TOC] 标签括起来

5. 转录表格时：
- 如果表格跨越多页，请将内容合并为一个连贯的表格。
- 使用适当的 markdown 表格格式，表格结构使用竖线 (|) 和连字符 (-)。

6. 不要在转录中包含分页符。

7. 保持文档的逻辑流程和结构，确保使用 markdown 标题正确格式化章节和小节（# 表示主标题，## 表示副标题等）。

8. 根据需要对其他格式元素（如粗体、斜体、列表和代码块）使用适当的 markdown 语法。

10. 仅返回 markdown 格式的解析内容，包括表格、标题和目录的指定标签。
```