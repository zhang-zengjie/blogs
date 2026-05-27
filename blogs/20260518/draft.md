> Have you ever [been trapped in  and ...这里wondered太轻了，我想表达：你是否曾经陷入。。。这种。。。。。的情况中，导致....following every traffic rule....] wondered what happens when following every traffic rule to the letter actually prevents you from making progress?
>
> During rush-hour in my hometown [不用“my hometown”，是否可以用“大城市”，或者繁忙地带等？], the answer becomes painfully clear. {The streets are packed, vehicles inch forward, and every maneuver is constrained not just by physics but by the web of traffic regulations. In such dense, dynamic environments, a paradox emerges:
>
> * If you strictly follow every rule, your vehicle may end up effectively immobilized, waiting endlessly for the “safe gap” to appear.
> * If you want to keep moving, you inevitably bend or temporarily violate some of these rules, stepping into gray areas that standard regulations never fully anticipated.}：用大括号{}括起来的内容需要简略化，可提一下，问题尤其严重于涉及“尤其是你赶时间的时候”
>
> This is the essence of the **rules–feasibility dilemma** [constraints-goal dilemma 是否更能被人接受一些？]: the tension between adhering to rules as absolute constraints and ensuring the system can actually function in real-world traffic.

Rules exist [are designed to] to guarantee safety. They are the necessary backbone that prevents unacceptable outcomes [它们用来约束人们的行为，同时也是。。。。的必要的backbone；这里要将rules和constraints挂上钩]. Their design [The design of rules] is deliberately conservative, often reflecting worst-case assumptions about human behavior, vehicle dynamics [改为physical dynamics?], and environmental conditions. Feasibility, on the other hand [我这里不想刻意而生硬地引入feasibility的概念，因为这个词对普通人不常见，如果上来直接就feasibility，太教科书，太生硬；我想更软一些，并由例子引出，比如说：“然而，当constraints过于保守的时候，一些比较。。。。。的任务就会遇到挑战；想象一下你赶着去机场，去医院，或者参加一个重要的商务谈判。。。。然而道路上。。。。”], demands that the system produces **effective, timely behavior**: cars need to move, traffic must flow, and human expectations of progress must be met. [介绍这个例子的时候说，well好吧，你可以选择等，但你无法控制别人采取，。。。当你看到你后面的车辆一个接一个地瞅准空隙。。。。的时候，你还能。。。。。吗？] [对了，这里有没有别的引用源或者什么说法之类的，就是说当。。。。。。的情况发生的时候，几乎总会有人打破规矩之类的？如果能有类似的权威说法的话，引用的话，我们的说法就非常strong了]The conflict is most acute in complex, dense, and highly interactive settings: follow all rules, and the system may stall; prioritize progress, and rules are bent, sometimes imperceptibly, sometimes more clearly. [这一自然段的末尾就要跟随前面的内容相应地修改一下]

In human driving, this tension is often resolved through social norms and implicit agreements. Drivers intuitively negotiate, yielding here, advancing there—a subtle choreography of compromise that traffic regulations implicitly tolerate. [也就是说，在。。。你在打赌他人的morality和respect] These soft norms are understood, audited, and interpreted by human agents, who can assume responsibility for outcomes.

[这里再加：在特定情况下，尤其是事态紧急的时候，常常考虑priority来解决，比如消防车、警车、救护车通常被赋予。。。。。的权限，普通车辆即使拥有通常先行权的时候也必须让路；这种情况显然只适用于。。。先行权只能被赋予极少数。。。。。普通人是无法享受到的]


But once we introduce ADAS or fully autonomous driving systems (ADS), the landscape changes entirely [这句话我们在改得“朴实”一些？比如：“但是，当开车的不是人，而是机器和算法。。。就changes entirely，这正是。。。ADAS 或者 ADS 的情形”]. Machines cannot rely on intuition, tacit social understanding, or moral judgment. Ambiguity that is easily navigated by humans becomes **algorithmically opaque**, difficult to attribute, and challenging to audit.

This blog sets out to explore this rules–feasibility dilemma [相应地改成constraint-goal dilemma？] from a systematic perspective: **what it truly means for system design, verification, and testing**,  and how we might begin to define, reason about, and expose such scenarios in ways that machines can understand—and humans can trust. 【pespective: 后面的内容有点太刻意了，我认为应当务实和Unbiased一些：比如"这个dilemma的现实语义是什么，它是由什么导致的？如何描述它？它是不可避免的？还是可以有效解决的？有些。。。。。。可能不像我们直觉所呈现的那样简单"】


### **Feasibility and the Limits of Strict Rules**[标题改为“冰山一角之下的。。。”]


Once we step beyond the abstract notion of rules, the challenge becomes concrete: **what does feasibility actually mean in the context of real-world driving, and why do rules alone often fall short?**

Traffic rules exist 【are designed 指定】 to ensure predictable and safe interactions. They are codified in laws, traffic codes, and functional safety standards such as ISO 26262, and are often reinforced in higher-level guidance like SAE driving automation levels. In theory, these rules should govern every maneuver: maintain safe following distances, yield according to right-of-way, respect speed limits, and so on. Under low-density conditions—empty roads, light traffic—these constraints are fully feasible. Vehicles can comply with all rules without ever compromising efficiency.

But in dense, crowded urban environments, strict adherence quickly becomes **impractical**. Consider a few typical conflicts:

* **Following distance:** Regulations may dictate a two-second gap between vehicles. In stop-and-go city traffic, maintaining this distance could leave a vehicle permanently trailing behind slower traffic.
* **Lane changes:** Yielding to every adjacent vehicle before merging might be safe in isolation but effectively prevents lane advancement.
* **Intersection priority:** Waiting for all other vehicles to clear before proceeding on a left turn may create gridlock.

The root causes of these conflicts are systemic: 【这里逻辑不全，过渡生硬，这里，我们实际上是想说：原因看上去很简单，就是rules在极端情况下太严格了，看似适当地放松rules就能解决问题（正如同冰山的一角）；然而对于一个复杂的交通系统来说，提供一个统一、一致、。。。。。。明确的标准来放松rules是个极其困难的问题，主要有如下的考量：】

1. **Environmental uncertainty and complexity** – Real-world traffic includes countless dynamic factors: unpredictable human drivers, cyclists, pedestrians, variable road conditions, and weather changes. Traditional SOTIF and ISO 26262 analyses assume a bounded, enumerable environment, but the boundaries here are inherently fuzzy. [这一点需要更正，不是uncertainty 和complexity，是“极端情况”的问题，法律法规所侧重的是cover“常规”或“普遍情况”；对于超出。。。。的极端情况，法律法规通常允许一定的灵活性，然而这种灵活性通常具有很强的主观性；不同的人对于这种“灵活性”发生条件的理解也是不同的]

2. **Static rules versus dynamic reality** – Most rules are static by design: a fixed car-following distance, a speed limit, a right-of-way principle. In high-density traffic, adhering rigidly to these rules may be infeasible; practical progress often requires **temporary, context-sensitive compromises**. 【这一点也需要修正；这一段的落脚点是“context”，也就是说，即使所有交通参与者对于法律法规的理解完全一致，比如他们从同一家驾校受训，经历过完全相同的课程，具有相同的mind-set和人格特性。。。。。（可以适当发挥），每个驾驶者所面临的situation，以及决策所基于的context也是不一样的；有些人。。。。。但有些人。。。。。。】

3. **Multi-agent interaction unpredictability** – Autonomous vehicles operate in ecosystems dominated by other agents. Safety is not only a property of individual vehicle behavior but emerges from the interplay between multiple actors. These interactions are nonlinear and stochastic. 【这一点也需要修正这个就是博弈问题的味道了；假设所有的交通参与者不但具有相同的。。。（如1 中提到的）而且具有完全相同的。。(如2中提到的)。。这非常接近。。中涉及的homogeneous multi-agent systems，但，在交通。。。进行的过程当中，众多的agent会遇到不同的平衡点；而这些平衡点对于扰动的反应。。。不同；例如，在不同的状态下，多智能体系统可能出现复杂的deadlock或者livelock现象。。。。。。这些。。。。。都是很难刻画和预测的】


[这里转折生硬，还需要补充一个逻辑转折，那就是“在测试中捕捉这些。。。。也是很困难的”]

Concretely, conventional testing and verification approaches struggle in dynamic, interactive scenarios. A city intersection during peak hours is not just a high-volume case—it is a **space of emergent complexity**. Safety boundaries and feasibility limits are context-dependent: a two-second gap may be safe on a highway, but in congested city traffic, it could make progress impossible. Conventional test success metrics—collision-free operation, rule compliance—assume that the system can always reach the goal given enough time. This assumption fails in real urban scenarios where human drivers frequently adopt aggressive or opportunistic maneuvers to maintain progress. 

The implication is profound: **rules effectively become “soft constraints” in dense, interactive environments**. While some rules must remain inviolable to preserve safety, others can tolerate limited, context-aware relaxation. This distinction is rarely codified in standards, yet it is essential for autonomous systems to function effectively. Defining which rules can be softened, under what conditions, and in ways that a machine can interpret, audit, and reason about, is a challenge that remains largely underexplored.

In short, the real-world traffic environment exposes the tension between the idealized rigidity of rules and the operational necessity of progress. Feasibility is no longer a secondary concern—it is an intrinsic property of safety in practice. Recognizing this is the first step toward a structured exploration of **how rules can be treated as soft constraints without compromising the ultimate safety objectives**.


### **Real-World Compromises Through the SOTIF Lens**（可以修改为：“SOTIF：一个。。。的镜头”）

[不管。。。。。，毫无疑问的是，无论如何 牺牲rules来妥协feasibility，安全都是不可。。。。的；因此  一个。。。。。的角度/工具是 SOTIF，。。。。。]

From the perspective of ISO/PAS 21448, SOTIF is concerned with **safety beyond functional faults**—the hazards that emerge even when a system functions as intended. The rules–feasibility dilemma sits squarely in this domain, yet it is far from trivial to categorize.

Consider the perspective of traditional functional safety under ISO 26262: the system is designed to operate within defined constraints, and safety is judged primarily by the absence of collisions or functional faults. The implicit assumption is that feasibility is guaranteed: given enough time or nominal traffic conditions, the system will successfully complete its maneuvers. Edge cases may be considered, but they are typically [recognized as] rare or enumerated scenarios.

SOTIF extends this view by addressing **unknown or unintended hazards**, emphasizing scenario-based testing, environment characterization, and functional verification under “reasonable foreseeable conditions.” However, dense urban traffic introduces a new level of complexity:

* The boundary of what constitutes a hazard becomes **context-dependent**.
* Multi-agent interactions are nonlinear and stochastic.
* Environmental and human behavior variables cannot be fully enumerated.

In other words, crowded traffic scenarios cannot be easily classified as simple edge cases or rare occurrences—they are **emergent, high-complexity situations**. Within SOTIF’s conceptual framework, determining whether a scenario represents a hazard or non-hazard is nontrivial because it depends on several **interdependent variables**. Key variables include:

1. **Behavior of surrounding human drivers (NPCs)** – Their aggressiveness, hesitation, or rule compliance directly affects whether following strict rules leads to safe progress or system stagnation.
2. **Traffic density and flow dynamics** – The spatial-temporal distribution of vehicles defines the operational feasibility envelope; small changes in density can shift the system from feasible to gridlocked.
3. **Vehicle dynamics and capabilities** – Braking performance, acceleration limits, and sensor ranges determine how safely a system can operate within reduced gaps or opportunistic maneuvers.
4. **Environmental conditions** – Road friction, visibility, and weather affect both the safety margins and the practical feasibility of maneuvers.
5. **Temporal constraints** – Human expectations of travel time introduce implicit urgency, which, while not codified in rules, influences which rules are temporarily deprioritized.
6. **Rule hierarchy and flexibility** – Some rules are legally or functionally inviolable (e.g., speed limits in hazardous conditions), while others (like exact following distance) may tolerate limited, context-sensitive relaxation.

Each of these variables is **non-deterministic and often partially observable**, creating a multidimensional space where hazards cannot be assigned fixed labels. In practice, this means:

* A scenario may be **hazardous under one combination** of human driver behaviors and traffic density, yet completely safe under another.
* Traditional SOTIF quadrants—unknown hazard, known safe, known hazardous—cannot unambiguously classify such scenarios.
* The system’s classification is **contingent**, dependent on a constellation of external and internal factors that interact dynamically.

This is the crux of the difficulty: the rules–feasibility trade-off cannot be fully codified in static specifications. It is **inherently context-dependent**, with key variables spanning the operational environment, human behavior, vehicle dynamics, and temporal demands. Any attempt to classify hazards without explicitly modeling these factors will either under-approximate risk or over-constrain the system, preventing feasible operation.

In short, the challenge in a SOTIF framework is not the absence of standards—it is the **difficulty of anchoring emergent scenarios within those standards**, because the hazard status depends on variables that are dynamic, interdependent, and only partially observable. Identifying these variables is the first step toward systematic modeling, testing, and eventual specification of rules–feasibility trade-offs in autonomous driving systems.


### **A Formal Perspective on the Safety–Feasibility Trade-off** [Anchoring ...... using/from a formal......]


SOTIF highlights the importance of addressing **unknown or unintended hazards**[这里，我们是否应该改为 hidden variables？因为上面SOTIF的讨论中，我们已经导出，SOTIF], but it stops short of prescribing exactly how to handle the trade-offs between strict rule adherence and operational feasibility. To reason systematically about this dilemma, we must step into a **formal perspective** 【改成：a ....way is to ..... in a formal perspective,.....】: a way to describe rules, feasibility, and the context-dependent trade-offs between them in explicit, analyzable terms.

At its core, we can think of a driving system 【要指明所有traffic system，也就是互动的多driving的环境是一个动态系统】 as operating within a **specification space** defined by:

* State: observable variables that .... the state of .....e.g., velocity, position.......
* **Context (C):** 【hidden】 Variables that influence how R and F interact—traffic density, behavior of surrounding drivers, vehicle dynamics, environmental conditions, and temporal pressures, as identified in the previous section 【明显这里要修正：variables不是context，context是由variables描述的，context应当是variables的assignment，一个context就是一次变量的赋值，context由变量来描述，此外，要指出context的可能空间】.

* **Rules (R):** Constraints that are designed to preserve safety under any reasonably foreseeable condition. [既然是formal，要指出它是 state sequence -> {true, false}]
* **Feasibility (F):** Constraints that ensure the system can achieve progress and perform effective maneuvers in real-world conditions.[既然是formal，要指出它是 state sequence -> {true, false}]


Formally, we can frame the problem as:

> For a given context (C), find a feasible policy (π) that satisfies safety-critical rules (R_s) while maximizing operational feasibility (F), recognizing that some non-critical rules (R_n) may need to be relaxed or treated as **soft constraints**. 【这里要修正，应该是对于给定context集中的context的取值，找到一个policy s->s, 使得其生成的所有可能的state sequence s_0, s_1, ..... 使得R和F都为true】


The challenge is that **R and F are not independent** [这里要点名为什么它们是不independent的，因为它们是coupled，它们依赖共同的context variables].【存在某些context情形会导致。。。。。。】在这种情况下 Strict adherence to R in dense or dynamic contexts may violate F, leading to system stagnation or degraded traffic flow. Conversely, prioritizing F may require temporary, controlled violations of R, creating a complex boundary between safe and unsafe operation. 


Here, **soft constraints** are explicit: rules whose violation does not directly compromise safety but may be necessary to maintain feasibility.【根据上面的更改，这里我们可以更清楚地说明了，soft constraints意味着部分Rules不再被处理为true和false了，而是被弱化为 -> [0,1]，然后从optimization的角度，希望它越接近1越好，但不强制它为1；】 The key is **context-dependent relaxation**: the same rule may be rigid in one scenario and temporarily soft in another, depending on C.

This formalization clarifies the **core difficulty**: we lack a systematic way to encode context-dependent trade-offs into specifications. Traditional approaches either:

1. Treat all rules as hard constraints, resulting in overly conservative behavior and frequent system stagnation.
2. Use heuristic thresholds to determine when rules can be relaxed, without explicit reasoning about context or emergent interactions.

In practice, this gap has profound implications for **verification and validation**. Without formal semantics capturing these trade-offs, test coverage remains blind to dense, interactive scenarios where feasibility and rules collide. Conversely, introducing context-aware specifications allows us to:

* Explicitly model how R and F interact across different scenarios.
* Identify the variables (C) that influence whether a rule can be safely relaxed.
* Generate **semantic coverage-driven test cases** that explore the emergent space of dense traffic interactions.

In essence, formal specification provides a **language to expose and reason about the trade-off**, rather than hiding it behind heuristics or ad hoc design choices. It transforms the problem from an ambiguous, context-sensitive tension into a **structured space** where the system designer can identify, quantify, and systematically test safety–feasibility compromises.

在结束的时候，我们要指明，这个Perspective可以帮助我们更好地描述和定义问题的边界，但无法解决。。。。真正。。。的问题；通过上面。。。。可以看到。。。。。【关键要指明这个context 变量在现实建模中是极其难以刻画的(nontractable)，因为它不但描述了动态的环境变化，还描述了所有智能体之间的interaction mode(这个词合适吗？有更合适的吗？)】从。。。。可以看出，根本问题就在于这个context variables，它和上一节SOTIF中。。。。。。描述的是一致的。这个context variables 刻画了某个agent是如何"understand" 一个situation的。【在这里，合适的地方点一下“semantics”，也就是context space其实描述了agent 对环境semantics的最大表达】如果说所有的state描述了agent能够看到的。。。。。那么这些context variables 就。。。了智能体能如何理解。。。以及理解到什么程度；关于“看到”和“理解”之间的区别和联系请看[这一篇blog](link)。


### **The Core Challenges in Resolving the Trade-off**【标题需要修改，你看这样行不行？“Context Space, the 冰山在海面下的部分”你有更好的建议吗？】


Recognizing the rules–feasibility dilemma and formalizing it through R, F, and C is only the beginning 【相应地需要改，因为我们上面分别从SOTIF和formal的角度来分析了问题到底源自哪里；因此这里应该改成“定位到context space”只是个开始】. The real challenge lies in **understanding and managing the complexity of the variables** that determine how, when, and which rules can be softened without compromising safety.

接下来的意思很好，但我们要紧扣context space了，如果可以的话，可以适时的时候点一点“semantics”

Several intertwined difficulties make this problem particularly thorny:

1. **Partial observability of context variables** – Key determinants such as the behavior of surrounding human drivers, traffic dynamics, or environmental conditions are rarely fully observable. A system may perceive a gap in traffic as safe, while subtle nuances in driver intent could render it hazardous. This uncertainty limits the ability to make deterministic decisions purely based on rules or feasibility metrics.

2. **Dynamic and emergent interactions** – Feasibility is not a static property. A maneuver that is feasible at one moment may become impossible milliseconds later due to interactions with other agents. Nonlinear and stochastic behaviors in multi-agent traffic create emergent outcomes that are difficult to predict or bound in advance.

3. **Context-dependent rule hierarchies** – Not all rules are equal. Some, like collision avoidance or adherence to critical safety regulations, are **hard constraints**, inviolable under any circumstance. Others, such as precise following distance or lane positioning in dense traffic, may be treated as **soft constraints**. Determining which rules can be softened, to what extent, and under which conditions is a **system-level judgment**, complicated by both legal frameworks and operational considerations.

4. **Specification vs. validation gap** – Traditional formal specifications assume a well-defined problem space. Yet, the context-dependent trade-offs between rules and feasibility defy static enumeration. Testing and validation approaches must contend with a vast, combinatorial scenario space where the emergent interactions of C variables produce unpredictable outcomes.

5. **Balancing conservatism with progress** – Conservative designs that rigidly enforce all rules may preserve safety in theory but fail in practice due to system stagnation. Conversely, aggressive relaxation of rules may maintain progress but increase risk exposure. This tension highlights that the **trade-off itself is a first-class object of design and validation**, not merely a byproduct of system behavior.

Given these challenges, a key principle emerges: **even if we cannot fully resolve the trade-off, we must ensure that testing and validation explicitly expose it**. The goal is not to guarantee a perfect solution—because perfect foresight is impossible in dynamic, dense, human-dominated environments—but to provide transparency about where, why, and under which conditions rules may be temporarily compromised.

【注意在这里我们不要过度吹嘘formal methods，因为formal methods在这里仅起到形式化的作用】

Formal methods, while not a panacea, play a critical role here. By representing rules, feasibility constraints, and context variables in a formal semantics, we can:

* Map the boundaries where rules and feasibility conflict.
* Identify which context variables are most influential.
* Systematically explore scenario spaces to **stress-test context-dependent trade-offs**.
* Enable reproducible, auditable reasoning about situations that might otherwise remain opaque or misclassified.

In essence, the challenge is not primarily technological—it is **epistemological**. The difficulty lies in **defining, exposing, and reasoning about the limits of safe, feasible operation** in environments that are partially observable, stochastic, and interactive. Addressing this challenge requires a combination of formal reasoning, rigorous testing, and scenario-driven exploration.


### **Conclusion and Invitation for Discussion** 【这里小标题也改一下；改什么呢？请你帮我建议一下】


The tension between rules and feasibility is not a peripheral concern—it lies at the heart of **real-world driving safety**. As we have seen, traffic rules provide essential guarantees, but strict adherence can make progress impossible in dense, interactive environments. Conversely, operational feasibility often requires **context-dependent relaxation** of certain rules, highlighting that safety is not a fixed, absolute property—it is **emergent and context-dependent**.

This realization raises the core question we began with:

> Should feasibility be part of the specification, even if it means temporarily relaxing some rules?

From a practical standpoint, the answer is nuanced. Some rules are inviolable and must remain hard constraints. Others can be formally identified as **soft constraints**, whose temporary relaxation maintains feasibility without compromising critical safety. The challenge lies in **defining, modeling, and testing these trade-offs**, particularly in environments characterized by dense traffic, stochastic interactions, and partial observability.

Standards like ISO 26262 and ISO/PAS 21448 (SOTIF) provide invaluable guidance. They define the boundaries of functional and behavioral safety, offer structured approaches for hazard identification, and emphasize scenario-based verification. Yet, as we have argued, the **rules–feasibility trade-off exists at the intersection of context-dependent variables**—driver behavior, traffic flow, environmental conditions, temporal pressures, and vehicle capabilities—making it difficult to fully classify scenarios within traditional SOTIF quadrants.

Here, **formal verification and semantic modeling** become indispensable. By explicitly encoding rules, feasibility constraints, and context variables in a formal framework, we can:

* Systematically explore scenarios where rules and feasibility collide.
* Identify which variables drive trade-offs and under what conditions.
* Expose context-dependent hazards that might otherwise remain hidden.
* Provide a reproducible, auditable foundation for testing and validation.

This approach naturally leads to **semantic coverage–driven testing**. By mapping the space of context-dependent trade-offs, we can prioritize testing on scenarios that are most likely to trigger compromises between rules and feasibility. This ensures that autonomous systems are evaluated not only for collision avoidance but also for **realistic operational performance** in dense, interactive traffic.

Ultimately, the key insight is that **safety cannot be guaranteed solely by hard constraints**. It emerges from a careful balance between rules and feasibility, informed by context, formal reasoning, and rigorous testing. By embracing this perspective, we move closer to designing autonomous systems that are not only technically safe but operationally viable in the complex realities of the road.

We would love to hear your thoughts: How does your team approach the **rules–feasibility trade-off**? Which rules do you treat as soft constraints, and how do you validate them in dense, interactive scenarios? Sharing these experiences will enrich our collective understanding and help the industry navigate one of the most challenging aspects of autonomous driving safety.
