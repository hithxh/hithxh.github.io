---
title: 从零构建大语言模型 (LLM from Scratch)
date: 2025-12-30
tags: [LLM]
---


> "用乐高拼出一架飞机，远比坐在头等舱里飞行更让人兴奋！"

大语言模型（Large Language Model, LLM）的出现引发了全世界对AI的空前关注。无论是ChatGPT、DeepSeek还是Qwen，都以其惊艳的效果令人叹为观止。然而，动辄数百亿参数的庞大规模，使得它们对个人设备而言不仅难以训练，甚至连部署都显得遥不可及。

本文将带你深入理解LLM的核心原理，从零开始构建一个完整的语言模型。我们将参考以下优秀的学习资源：

- 📺 [Andrej Karpathy: Let's build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- 🎓 [Stanford CS336: Language Modeling from Scratch](https://stanford-cs336.github.io/spring2025/)
- 🔧 [MiniMind](https://github.com/jingyaogong/minimind) - 2小时完全从0训练26M参数的GPT
- 📚 [Mini-LLM](https://github.com/WKQ9411/Mini-LLM) - 100-200M参数的迷你模型复现项目

