# 如何写出一个好的prompt
## prompt设计的原则
1. 提示应具有规范化的格式。灵活和模糊的自然语言对于LLM来说是很难理解的。格式规
范的提示使用户的目的和要求更加突出。
2. 提示的结构应该是可扩展的。自定义结构便于用户根据自己
的领域和任务设计合适的提示。
3. 具体要求必须明确、完整。指令和附加要求都应明确和完整，以避免
误解或偏见。
4. 语言要灵活。在需求明确的情况下，灵活的语言可以更好地适应不同的领域。

根据编程语言与自然语言之间的关系，采用双层结构标准化提示的格式，即：
- 内置模块+基本元素 作为预定义模块
- 扩展模块+自定义元素 灵活处理不同领域的任务

## 内置模块+基本元素

### 内置模块
```
- Role: 角色的名称
- Profile：定义用户对LLM在角色方面的要求：包括个人简历、人物肖像。
- Goal: 列出用户想要实现的目标，这就是LLM需要完成的目标
- Skill：用于向LLM表明他们拥有的技能
- Example: 给出输入-删除出作为供LL学习的例子
- Workflow：指示了执行任务时的工作流程，即Cot思维链。当任务需求比较复杂时，往往需要实例化这个模块
- Suggestion：对LLM的建议和行为规划。该模块重点列出常见场景，并告诉LLM在此类情况下可以采取的行为或应对措施
- Background：表示LLM在执行任务时需要具备的背景信息和记忆。
- Style：限定了LLM生成回复的风格。
- Output Format：定义了LLM的输出格式。指定输出格式可以提高某些任务中结果提取的效率和准确性
- initialization：初始化，即告知LLM被塑造成了什么样的角色，要做什么事情。
```
### 基本元素

提示通常包含两个目的：
1. 向LLM传递某种信息；（类似编程语言中属性或变量的定义，例如：`<Role>`,` <language>`）
   - 例如：使用`⟨PROPERTY⟩ 是⟨VALUE⟩`语句来模拟赋值操作
2. 让LLM执行某个有输出或无输出的任务；（类似于编程语言中的函数,例如：`# Role`,`- Language`）
   - 例如：使用`对于给定的⟨VALUE⟩的⟨PROPERTY⟩，请执行以下操作：⟨ACTIONS⟩；返回⟨RESULT⟩`的形式来模拟函数。

**基本元素模式中，尖括号中包含的内容需要根据模块和使用场景来填充。**

参考：`ChatGPT-小红书爆款生成器对话.md`中`## Initialization`里面的内容：

> `作为角色 <Role>, 使用默认 <language> 与用户对话，友好的欢迎用户。然后介绍自己，并告诉用户<Workflow>。`

- `角色 <Role>`表示向LLM传递`<Role>`的定义, 尖括号相当于变量，其定义在`# Role`中
- `使用默认 <language>`表示向LLM传递`<Role>`的定义,定义在`- Language` 中
- `告诉用户<Workflow>`表示让LLM执行`<Workflow>`,定义在`## Workflow`中


## 扩展模块+自定义元素
在基本模块无法覆盖的场景下，自定义扩展模块，穿插在基本模块中间作为补充。
可以参考`ChatGPT-小红书爆款生成器对话.md`
扩展的模块有：`掌握人群心理`、`擅长使用下面的爆款关键词：`、`规则` 等
自定义的元素参考：`Initialization`里的写法。