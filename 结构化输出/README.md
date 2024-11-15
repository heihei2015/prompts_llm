# 输出结构化内容的注意事项

- 不同模型对prompt格式的偏好不同
  - GPT和Gemini更喜欢markdown
  - Claude更喜欢XML
- 关于流式
  - 界面上需要快速响应的场景
  - XML,Json,等需要标签闭合的场景不太适合流式
  - 可以考虑Jsonl、markdown、bulletlist、自定义格式等可以边输出边解析的格式
- 使用方法
  - 将下面的OUTPUTINSTRUCTIONS拼接到原始prompt中即可，建议放到输入之前
  - 如果还是有边缘场景，再增加一个EXAMPLE约束，给三五个示例：输出示例，或者是输入-输出示例
    - 可以在prompt中拼接
    - 也可以通过role=user,role=assistant来组织
  - 使用Prefill技巧，比如"接下来输出markdown:","接下来输出json:"
    - 可以在prompt中拼接
    - 也可以通过role=user,role=assistant来组织
  - 如果还是不行，先通过prompt确保输出范围可控，再到代码中增加正则表达式兜底
  - 最后再不行就要考虑重试和界面报错
  - 工程上还能做的事情
  - 虑使用更小的temperature
  - 使用logit_bias参数严格控制输出范围和概率