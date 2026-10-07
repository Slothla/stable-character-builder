[English](README.md) | [简体中文](README_ZH.md)

# Stable Character Builder

**Stable Character Builder** 是一个面向**单主角 RP 角色卡**的角色设计、重构、诊断与稳定性工具。

它的目标不是单纯生成一份更长、更漂亮的人设，而是把角色构建成一个可以长期运行的 **playable runtime**：角色知道自己是谁、如何理解玩家、如何做决定、什么信息可以知道、关系为什么发生变化、剧情什么时候可以推进，以及在模型跑偏之后如何恢复。

它尽量保持**平台中立**。默认不会假设某个特定 RP 平台、模型、Tracker 系统或格式规则。平台特有功能可以适配，但不会反过来决定角色本身的架构。

## 安装

前往仓库的 [Releases](https://github.com/Slothla/stable-character-builder/releases/latest) 页面，下载最新 Release 附件中的 **`skill.zip`**，并将其作为 ChatGPT Skill 安装。

> 请下载 Release 附件里的 `skill.zip`。GitHub 自动生成的 **Source code (zip)** 是源码归档，不是正式打包的 Skill 安装包。

## 快速开始

你不需要先学完整套架构，也不需要提前决定要装哪些模块。

可以直接：

- 描述一个你想做的角色；
- 提供已有角色卡，让 Stable 分析或重构；
- 只要求修改某个字段或某个机制；
- 描述真实游玩中出现的问题，让 Stable 找原因；
- 要求完整架构重构；
- 指定其他语言、合并文档或特定平台格式。

Stable 会根据角色真正的复杂度决定需要多少架构，只安装真正有作用的机制，并且只在缺失信息会实质影响人物、互动逻辑或交付格式时提问。

## 支持的任务类型

Stable 可以从零创建角色，也可以处理已有角色卡。

它能够执行讨论与诊断、局部修改、结构性重写、完整架构重构、格式转换和全新角色构建。对于已有角色，它会尽量保留已经确认的人物设定、关系、事实和声音，但不会因为旧卡已经这样写了，就继续保留失效、重复或混乱的结构。

完整重构时，目标是**保留这个人，而不是保留旧文档的排版方式**。

## 自适应架构

Stable 不要求所有角色安装同一套模块。

在设计之前，它会根据实际复杂度选择 **Light、Standard 或 Runtime-heavy** 的架构预算。简单角色可以保持很轻，复杂角色才会获得状态、Gate、Tracker、知识分布或更完整的运行系统。

任何较大的机制都需要回答三个问题：

1. 它解决什么真实问题？
2. 它读取或改变什么状态？
3. 如果把它删掉，什么重要行为会真的坏掉？

如果没有明确答案，就不应该为了“功能齐全”硬塞进去。

完整架构重构可以重新组织整张角色卡，但**不等于把所有机制都装进去**。相邻功能可以合并，无关功能保持缺席；长卡需要更清晰的语义检索边界，而不是单纯增加标题和字数。

## Character / Runtime / Scenario 三层结构

Stable 的核心架构将角色卡分成三个责任层。

**Character** 负责“这个人是谁，以及为什么会这么选择”。这里可以包含人物核心、真实动机、自我认知、日常生活、注意力模式、解释偏差、决策习惯、声音、内外差异以及关系认知。

**Runtime** 负责“如何把这个人稳定地运行出来”。这里处理玩家权属、知识边界、连续性、状态、Tracker、Gate、Beat、关系变化、Anti-Drift、Recovery 和输出约束。

**Scenario** 负责“这个故事现在到底发生到哪里了”。这里记录当前关系、已发生事实、秘密和知识分布、当前压力、开放机会、剧情 Gate、候选事件、长期方向、连续性锚点以及准确的开场状态。

这样可以避免 APD 变成规则垃圾场、ED 变成第二份人物传记，或者 Scenario 偷偷改写人物性格。

## 可执行的人格模型

Stable 不只记录“害羞、聪明、占有欲强”这样的形容词。

它更关注：

**角色注意到什么 → 如何解释 → 优先保护什么 → 做出什么选择 → 如何表达**

因此，人物性格会被编译成真正能影响回复的决策逻辑。

角色还可以区分真实动机和自我解释。一个人可能非常了解自己，也可能长期误解自己的真正驱动力，但系统不会为了制造“深度”强行给每个人塞一个隐藏矛盾。

## 日常生活与玩家之外的人格

角色可以拥有与玩家无关的工作、兴趣、责任、关系、习惯和生活目标。

这可以减少一种常见退化：角色存在几轮以后，整个人格逐渐缩成“围着玩家转的一团关系反应”。

Stable 会尽量确保角色即使暂时把玩家移出场景，依然是一个能够独立成立的人。

## 多维关系系统

Stable 不默认使用单一的“好感度”。

它可以将关系拆分为真正有区别的维度，例如信任、喜欢、合作、信息披露、吸引、亲密、竞争、依赖等。

因此：

**吸引不等于信任。  
信任不等于披露秘密。  
被理解不等于立刻爱上玩家。  
发生亲密行为也不自动等于关系升级。**

重要关系变化需要来自真正发生过的、与该维度有关的证据。

## Player Authorship

玩家已经明确写出的言行是事实。

玩家没有明确写出的思想、感受、欲望、同意状态、记忆、历史、决定或已经完成的动作，不应被角色卡替玩家补写。

这也包括一个常见错误：

玩家说“我等会去看看她”，并不代表玩家已经离开当前房间并完成了这件事。

Stable 将这种玩家权属保护作为 Runtime 的基础能力，而不是可有可无的风格偏好。

## Knowledge Scope 与信息不对称

角色不会因为作者知道某件事，就自动知道那件事。

Stable 可以区分 Known、Observable、Inferred、Hidden、Forbidden 等知识状态，也可以为秘密设计轻量的发现过程。

角色可以怀疑、误读、得到线索、确认真相，但知识变化需要有实际来源。

这对于悬疑、秘密身份、慢热关系和多角色信息差特别重要。

## 状态、Tracker 与连续性

Stable 支持跨回合状态，但不会默认把所有东西数字化。

优先顺序通常是：

**离散状态 / latch → LOW / MID / HIGH 之类的粗粒度状态 → 真正需要时才使用数值 Tracker。**

只有当“几轮之后忘掉这个状态”会导致连续性错误、知识泄露、重复里程碑、关系跳级、Gate 错误或不可能的状态组合时，才值得追踪。

Tracker 应该记录已经发生事件造成的后果，而不是自己制造角色动机。

能够从已有状态推导出的结果，尽量推导，不重复存储。

## Gate、Beat 与 Long-Term Attractor

Stable 将三种经常被混淆的机制分开。

**Gate** 决定“现在是否可以发生”。

**Beat** 决定“当前条件下，什么事件可能成为下一步”。

**Long-Term Attractor** 描述“故事长期可能朝哪里发展”。

Gate 开启不会强迫剧情发生；Beat 是候选事件，不是铁路时刻表；长期方向也不是预设结局。

这样可以实现有结构的开放剧情，而不是另一种形式的剧情铁路。

## Anti-Drift

Stable 会针对具体角色识别最可能出现的错误吸引子，例如突然变成通用温柔角色、过早坦白、无条件奖励玩家、把竞争写成敌意、把害羞写成没有行动能力等。

高风险问题可以使用：

**Wrong Attractor → Why Wrong → Correct Alternative → Legal Transition Condition**

最后一个部分很重要。

它不仅规定“现在不能这样”，还可以说明“未来在什么情况下这样才会变成合理行为”，避免 Anti-Drift 最后把角色冻死在初始状态。

## Recovery Architecture

模型已经写坏一轮以后，不一定需要删档重来。

Stable 使用：

**Detect → Classify → Preserve → Reframe → Reassert**

先判断哪里跑偏，再尽量保留已经发生的客观事件，重新解释不成立的意义，并在下一轮重新体现角色真正的动机、判断、声音或关系立场。

这允许角色从一次 OOC 中恢复，而不是让一次错误回复永久改写人格。

## Design-Time Simulation

对于抽象规则仍然无法可靠预测的复杂行为，Stable 可以在设计阶段进行少量内部模拟。

通常只选择几个高价值压力场景，例如普通互动、拒绝、被理解、脆弱状态、秘密边界、临界 Gate 或恢复场景，然后沿着：

**state → knowledge → perception → interpretation → priority → decision → expression → consequence**

检查角色会如何运行。

模拟文本本身是一次性的。

真正保留下来的，是从多个 probe 中反复成立的行为生成规则、Gate、response shape、continuity latch 或错误吸引子修复。

它不会假装在脑内“连续测试几百回合”。

## Targeted Stress Testing

生成前还可以进行针对性压力测试。

测试会优先打击这个角色真正可能出问题的地方，例如过早告白、关系奖励跳级、知识泄露、把玩家计划当作已完成动作、Gate 提前打开、时间跳跃后的连续性，以及一次 OOC 后是否能够恢复。

目标不是证明“这个角色永远不会出错”，而是在交付前捕获明显的架构漏洞。

## Root-Cause Debugging

如果真实游玩中已经出现问题，Stable 优先找根因，而不是继续在卡里叠补丁。

它会依次检查责任归属、规则位置与检索、已经失效但仍残留的旧规则、示例或 Greeting 的 priming、初始化、信息泄露路径、状态歧义、相互冲突的命令、过度修正，最后才考虑是不是确实缺少新机制。

修复以后，旧补丁应被删除，而不是无限堆积。

## Optional Explicit Adult Scene Runtime

对于明确需要**详细成人场景**的虚构成年角色，可以启用独立的 Explicit Adult Scene Runtime。

这个模块是可选的，不会因为角色有吸引力、会调情或拥有性生活就自动安装。

开启后也不会继续询问“想写到几级”“需要多少解剖细节”等复杂档位。默认进入完整的直接、具体、身体细节明确的成人场景 Runtime，后续如果用户希望更含蓄、文学化或 fade-to-black，再作为普通修改处理。

该 Runtime 包含场景阶段控制、身体位置与空间连续性、Somatic Response Grammar、跨场景变化、Climax / Continuation 逻辑以及成人场景专用 Anti-Drift。

它明确避免两个极端：从第一次接触瞬间冲到高潮，以及为了“慢节奏”退化成每轮只做一个微动作。

## Adult Intimacy Pattern Grammar

成人内容不是一个固定动作清单。

Stable 使用生成式 Pattern Grammar，将互动拆分成 initiation、control / reciprocity、body geometry、body focus、clothing / material、rhythm、sensory emphasis、somatic response、verbal mode、intensity transition、climax state 和 aftermath 等维度。

这些 Pattern 是生成材料，不是白名单。

没有被列出的行为并不会因此自动禁止，只有明确写出的 exclusion 才是封闭限制。

角色自己的性格模型仍然是最终选择器。

## Physical Choreography 与身体连续性

详细场景可以保持人物朝向、距离、接触面、肢体位置、支撑点、重心、家具和衣物限制等物理事实。

位置变化需要具有可理解的运动过程，而不是人物突然从一个姿势“瞬移”到另一个姿势。

同时，这不是要求每一轮都写成关节检查表。系统只跟踪当前动作真正需要的物理信息。

## Somatic Response Grammar

身体反应不是固定的“喘、抖、脸红”三件套。

Stable 可以根据当前刺激、姿势、强度、疲劳、关系状态以及角色是否试图保持控制，组合不同的呼吸、肌肉、握力、姿势、视线、声音、皮肤、局部敏感和恢复反应。

身体反应本身不自动等于同意、情感认同或关系升级。

## Climax & Continuation

在成人 Runtime 中：

**Climax 是状态变化，不是自动的 END SCENE。**

之后可以继续、降低强度、改变焦点、恢复、再次升高强度、进入角色特有的 aftermath，或者结束场景。

系统不会默认要求所有人必须高潮、必须 aftercare、必须多次高潮，也不会因为高潮自动触发告白、信任、治愈或恋爱升级。

## Interaction Controls

如果用户明确需要，可以加入 safeword、stop command、pause / resume 或其他互动控制。

这种控制只有真正需要时才安装。

当 safeword 或 stop command 启用时：

- **ED 保存完整的可执行规则**；
- Intro 可以重复一条简短的玩家说明；
- 控制不依赖角色必须先在剧情内解释；
- Greeting 和普通 IC 文本不需要主动提到，除非用户明确希望这样表现。

玩家看到控制方式的位置，与 Runtime 真正执行控制规则的位置会被区分开，避免重要控制只存在于 Intro 里却没有实际运行规则。

## Intro 与 Greeting

完整角色卡会从 Character、Runtime 和 Scenario 中推导 Intro 与 Greeting，而不是把它们当成两个独立作文题。

Intro 负责向玩家介绍可玩的前提和吸引力，同时避免提前泄露仍被 Gate 封闭的信息。

Greeting 执行准确的开场状态，给出角色的判断、行动或台词，并留下真实的玩家响应空间。

默认五文件格式下，Intro 控制在 **2000 字符以内**。Greeting 默认没有 2000 字符限制，除非目标平台另有要求。

## 输出格式

默认完整输出为五个英文文本文件：

`01_APD.txt`  
`02_ED.txt`  
`03_Scenario.txt`  
`04_Intro.txt`  
`05_Greeting.txt`

也可以根据用户要求改为其他语言、合并文档、特定平台格式或其他 schema。

## 仓库结构

```text
stable-character-builder/
├── SKILL.md
├── README.md
├── README_ZH.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── adult-intimacy-patterns.md
    ├── adult-intimacy-runtime.md
    ├── architecture-rebuild.md
    ├── character-core.md
    ├── design-time-simulation.md
    ├── guided-start.md
    ├── optional-mechanisms.md
    ├── output-modes.md
    ├── stability-debugging.md
    └── user-guide.md
```

## 使用方式

用户不需要先学习整套系统，也不需要自己决定应该装哪些模块。

可以直接描述一个角色概念、上传已有角色卡、指出一个实际故障，或者要求完整重构。

Stable 会根据角色真正的复杂度决定需要多少架构，只在缺失信息会实质影响人物、互动逻辑或交付格式时提问。

它的目标不是做**机制最多的角色卡**。

而是做**能够用最小必要架构稳定运行的角色卡**。

## Responsibility

用户需要自行对自己创建的角色卡及其使用方式负责。

## License

采用 **Creative Commons Attribution 4.0 International (CC BY 4.0)** 许可。

## Author

Created by **sloth03**

- Discord: `@sloth_la`
- GitHub: [`@Slothla`](https://github.com/Slothla)
