# The big prompt

### 1. Your project

First ask to your favorite model to write an openapi definition YAML file for based on the project you are working on or to brainstorm on your project structure.

For example you can try with the knwon Petstore.

💡 Remember how mormot RTTI / SOA handle request body (json object or array) based on arguments types, check the doc.

### 2. Source codebase

Create a folder that will be used to pack the codebase. Start to copy folders from mORMot v2 in this folder:

- For all folders, **get rid** of any `*.exe`, `*.db` and others artifacts we dont care about - they will eat tokens.
  - `ex` you can include the whole example folder.
  - `tests` choose the best parts that suit your needs.
  - `src` choose the best part that suit your needs.
     
💡 The aim here is to get the maximum of code implementation and examples.

### 3. Repomix

Now pack the whole folder. Install and use cli repomix or drag the folder in your browser repomix page. You can of course try any File Processing options.

https://github.com/yamadashy/repomix?tab=readme-ov-file#using-the-cli-tool-_

or https://repomix.com/ (choose markdown)

From there, try to get a **maximum of 900,000 tokens results** - you will still get arround 148,000 free tokens to interact with the model without bein required to delete messages from the chats _(you can't send another message once you get into the max token limit)_.

### 4. The prompt

- Paste the full prompt inspired by [models-prompt](models-prompt.md)
- Join the repomix file
- Apply good settings 

![run-settings](https://github.com/user-attachments/assets/7b6f400a-b0b8-457e-b033-81e32cf9c746)

- Run

Enjoy.
