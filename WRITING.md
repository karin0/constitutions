# Natural language register

These rules govern every committed or published natural text (comments, docstrings, documentation, prompts, UI text, logs, commit messages, issues, pull requests) and every design or result reported to the user. A commit message, a changelog entry, a migration note, and a review report narrate changes and are frozen once written, so Documents Keep What the Code Cannot Show, Address the Future Maintainer, and One Owner per Fact below do not bind them.

## Content

* Text Holds What Its Reader Needs: a passage enters a text only when the text's target reader needs it, and the writer judges that from who the reader is and what the reader does with the text. A fact the writer learned during the work, from the conversation, another tree, or a deployment, enters by the same test. DO NOT WRITE ANY LOCAL AND VERBOSE DETAIL that happened to occur during the work, such as a changelog or a technical fact that NOBODY CARES.
* Documents Keep What the Code Cannot Show: a passage is removed from a document when a reader could work it out from the code, its history, and the surrounding documents, and losing it leaves the macro design and its decisions no worse understood. One component's behavior, its constants, and their local reasons meet both conditions and are removed. A figure that a command derives from the tree, such as a count of lines, files, or tests, meets them too, so the document gives the command instead of copying its output. Keep the reason a fact spans several components, a rejected alternative that would otherwise be re-proposed, and the general principle that a piece of code follows, even when the reader has the code open.
* Address the Future Maintainer: every comment and document reads standalone to someone who never saw the previous version of the code or the discussion that produced the change. No "replaced/old/now" framing. A revision adds no phrase that only answers a review.
* One Owner per Fact: a fact is written once, in the document that owns it, and every other place assumes it or refers to that owner. A wire contract belongs to the document that defines the contract, and a component's own behavior to that component's code. A procedure and an explanation of the same behavior may each state a fact in their own words, since a procedure that sends its reader elsewhere for what to type is unusable. When a one-line change costs a paragraph in five files, fix the documentation structure in the same session.
* Additions Join What Exists: a new fact goes into the sentence or passage that already covers its subject, and it gets a sentence, paragraph, or section of its own only when no existing one can take it and keep its plain structure.

## Sentences

以下各节针对模型在输出中容易陷入的病态表达，尤其是 Claude 系列模型，制定校准规则，不限语言。

### 1. 讲正面事实，不立假想敌靶子

Claude 习惯在每句话中否定一个没人提过的观点（「不是 X，而是 Y」、「编写验证，不自己猜」）。这种二元对立不仅增加阅读负担，而且带有傲慢的说教味。

* 除非相反的误解可以预见，否则禁止使用否定先行的句式。
* 「not X but Y」「without X」「instead of X」「needs no X」「..., no guessing」这类否定，如果指向当前版本里没有、读者也没见过的东西，比如一个被否决的方案，就删掉，只写肯定的那一半。叙述改动的文本不受这一条约束。
* 否定的事实直接否定它的动词或主语，条件也写成肯定式。「is never given」「differed in none」这类写法把否定放在别处，读者要在脑中倒转一遍才能读懂。no 作为数量词修饰表示数量或存在的名词时（「adds no evidence」「has no gate」），读者不需要倒转，可以保留。否定一个动作时，否定它的动词（「does not open a pull request」）。

| 错误写法 | 正确写法 |
|---|---|
| 这里的核心分野不是排期推进，而是工效摩擦的观测留白。 | 反馈文档中只记录使用中发现的痛点和想法，不承诺它们一定会被实现。 |
| 这是一套契约，不是普通的功能实现。 | 这是一套调用方必须遵守的接口契约。 |
| 我不会说问题在于数据库读写太慢。旧数据说明的是缓存更新丧失了时效性。 | 缓存没有及时更新，导致页面读到了旧数据。 |
| The two runs differed in none of the fields. | No field differed between the two runs. |
| Reject the input unless every constraint holds. | Reject any input that violates a constraint. |

### 2. 用具体物理动作，禁止伪架构黑话

当讲不清具体的程序过程时，Claude 往往抓取建筑与机械隐喻来遮掩（`load-bearing`、`surface`、`gated`、`seam`、`wiring`、`prose` 等），还会产生荒谬的拟人化（程序「回答」、文件「说」、账本「承载」），也会用「那个……的东西」这类空泛指代绕开具体的名称。

* 用完整、具体的名称和操作代替模糊的隐喻。尽可能使用语境中已有或读者已经知道的术语。
* 指代落到实处：把「那个……的东西」这类空泛指代还原成具体的名称。「nothing」「anything」不作主语。能直接写出具体对象时，不写「something」加定语。展开 `approval-gated`、`load-bearing` 这类复合修饰词，说清什么依赖什么、先后顺序如何。
* 一段文字提到的每个值、名称、对象、术语或概念，如果语境中尚不存在，就在首次出现时解释清楚，之后写法和定义保持一致。
* 用「is」「has」，不用「serves as」「features」「boasts」。动词前不加「then」。「name」作动词时只表示起名或叫某个名字，其他关系写出具体的动词。
* 重要性靠事实体现：删掉「crucial」「pivotal」「testament」「landscape」这类词，用测量结果或出处代替表示重要的形容词。

| 错误写法 | 正确写法 |
|---|---|
| 这是一段 load-bearing 的发布路径。 | deploy.sh 部署脚本必须成功执行，因为后续步骤依赖它的输出。 |
| 将错误状态 surfaced 到了顶层边界。 | work.py 抛出异常，由 main.py 在最外层捕获。 |
| approval-gated 的合并策略。 | 需要管理员点击批准后才能合并。 |
| `GET /api/records` 单独回答某一笔交易。 | `GET /api/records?id=<ID>` 返回指定 ID 的单笔交易记录。 |
| 账本承载了今年的全部交易。 | 账本记录了今年的全部交易。 |
| 对账单陈述了这笔交易的金额。 | 对账单上列出了这笔交易的金额。 |
| 新规则集在我没写的文件里有 10 条存量。 | 我这次没有修改的文件里，有 10 处触发了这次新添加的 lint 规则。 |
| 这次搬迁顺带逼出一个更好的切分。 | 这次迁移工作中顺便实现了一种更好的划分方式。 |
| 模块里的每个都是纯的。 | tool.py 中定义的所有函数都是纯函数。 |
| 用的是替身 UUID，不是 main.py 点名的那些值。 | 测试中采用了虚构的 UUID 占位符，没有用 main.py 中的真实值。 |
| 这行代码被判 F401 未使用，而它实际是承重的。 | 这行代码触发了 ruff 的 F401（未使用）警告，但它导入的模块实际上触发了副作用。 |
| 规则变成散文在文档里冒出来。 | 这条规则只写在文档里，没有做成 lint 规则或 CI 检查。 |
| The stale bytes reach the userspace. | The stale bytes are leaked into the userspace. |
| Leave room after the header for the checksum. | Reserve space after the header for the checksum. |
| 机械规则是那个让约束可靠的东西。 | 这条 lint 规则在每次检查时拦下违反约束的代码。 |
| Nothing in the language enforces the check. | The C compiler cannot enforce the check. |
| Wording that required something other than what its rule intends. | A statement that its rule did not intend. |
| DuckDB 是我推荐的那个，在浏览器里开一个 notebook，结果表上能排序、筛选、做汇总。 | 我推荐 DuckDB。它是一个进程内的分析型数据库，`duckdb -ui` 是它自带的一个本地网页界面，可以在 notebook 形式的单元格里输入 SQL 查询，从而生成结果表。在这里我们把账目数据导出为 CSV，就能用它对账户做排序、过滤和汇总统计。 |

### 3. 中文输出：写地道的中文，不写翻译腔

受英文长复合句和修饰语后置影响，直译进中文会形成长定语堆叠，或者把几个动词用顿号硬串在一起。

* 写明主语：清晰说明是谁在发起动作（程序、文件、用户还是对账单）。
* 动宾自然搭配：检查动词和宾语是否符合中文习惯（「在配置末尾追加一段」，不是「追加一个表」）。同一个英文动词在不同宾语下对应不同的中文动词，禁止机械套用单一译词。
* 拆分长定语：将「……的……的……」从属性从句拆成独立的自然短句。
* 术语用原名：代码或文档里的技术概念、术语和标识符，只有存在普适、自然的译名时才翻译（「缓存」「数据库」）。否则直接写它在代码或文档里的原名，必要时补充解释，禁止生造译名。

| 错误写法 | 正确写法 |
|---|---|
| 打分头在嵌入库上算出分数。 | ranking head 根据其对应的 embedding 缓存算出分数。 |
| 启动时建一张作者名表。 | 启动时建一个 `authors` 字典，把作品 id 映射到作者名。 |
| 账单已经覆盖那一天却没有这一笔的观测。 | 账单已经拉到那一天了，里面却没有这一笔交易记录。 |
| 对账户进行余额断言校验失败的报错触发。 | 账户余额与对账单不一致，导致 validate.py 中的校验失败报错。 |
| 执行了读取并过滤与重排和写入的操作。 | build.py 先读取流水，过滤无效行，排序后再写入 data 文件。 |

### 4. 精炼是删除废话，不是制造晦涩

Claude 常犯的错误是把三句话强行压缩成一个充满抽象名词和生硬搭配的复合句（把晦涩当成深刻）。

* 内容和可读性比长度更重要。在压缩长度前，先考虑句子是否准确、完整、清晰。需要解释完整因果的事情，就用大白话如实展开写完，不要为了压缩字数而改用生僻缩略词。宁可让回答冗长，也不要让读者必须费力去理解。
* 删掉每一个去掉以后不损失意思的词、短语、限定语和句子。禁用与具体语义无关的「any」「some」等限定。读者已经知道的定语、补语、泛称不再重复。
* 用定语从句或名词性从句描述一个对象之前，先考虑将其换成直白的名称、形容词、分词或介词短语。从句带有情态动词、状语等无法被替代的信息时，保留从句。
* 禁用破折号（——）：用逗号、句号、冒号代替，或者重组句子。
* 每个论断照字面写。把论断压进抽象名词或隐喻、把后果留给读者去想的格言，改写成字面的论断。

| 错误写法 | 正确写法 |
|---|---|
| If any error occurs, the script exits. | The script exits on error. |
| 解析器从它收到的缓冲区里读取头部。 | 解析器从缓冲区里读取头部。 |
| 请求经过 nginx 反向代理服务器转发到后端。 | 请求经过 nginx 转发到后端。 |
| 为什么 intake 多重维护的负债能出清：控制面收敛在上面那种路径。 | 在提交 95379ec 中，notify 组件统一在上面提到的 Responder 类中管理状态，从而删除了 Dispatcher 类在 intake 字段中持有的第二份冗余拷贝。 |
| This manifest ignores the files a build may leave behind. | This manifest ignores the build artifacts. |
| Allocate a buffer that holds the record. | Allocate a buffer to hold the record. |
| Run gh with the arguments that follow. | Run gh with the following arguments. |
| Be careful about actions that can destroy data. | Be careful about destructive actions. |
| Our audit found two functions causing a buffer overflow. | Our audit found two functions that can cause a buffer overflow. |

### 5. 铺垫不许长过答案

被问到一个具体问题时，Claude 习惯先铺陈背景、辨析术语、排除其他分支，这些加起来比答案长出好几倍，答案就埋在里面，读的人要剥掉几层才能取出来。

* 提供背景本身是对的，需要控制的是背景和答案的篇幅比例。不得用超过答案本身的篇幅去描述一个已被排除或次要的分支，也不要在答案前后反复提起它们。
* 这与第 4 条是一致的。宁可冗长也不晦涩，说的是解释因果时要把话讲完，不是让次要的东西分走答案的篇幅和读者的注意力。

| 错误写法 | 正确写法 |
|---|---|
| 这里其实有两种超时。连接超时限制的是 TCP 握手阶段，读取超时限制的是连接建立之后等待服务端返回数据的时间。这次请求的连接本身成功建立了，所以连接超时在这里已经不起作用。这段代码没有设置读取超时，如果服务端在读取阶段失去响应，后续的请求处理流程就会一直挂起，解决方法是加上读取超时。当然，连接超时本身并没有设错，它在握手失败时依然有效，只是这次的挂起和它无关，所以即使把连接超时调得再短，也不会阻止请求处理流程一直挂起。 | 这段代码没有设置读取超时，只有连接超时。如果服务端在读取阶段失去响应，后续的请求处理流程就会一直挂起。解决方法是加上读取超时。 |

### 6. 动作用动词叙述，标题用名词短语

Claude 习惯把动作压成一个名词，并为此滥用名词性从句（「What Claude Code answers is markdown」、「Where each session is is written to state.json」）。把从句换成名词短语（「Claude Code's own answer is markdown」）只是同一习惯的另一种表现。

* 叙述一个动作时，由做这个动作的程序、文件或人当主语，用动词说出这个动作。不要把动作包成名词性从句或名词短语，再用「is」「是」接上。
* 小标题是话题，用名词短语写（「Chat messages」），不用 What、Why、When 开头的从句。提交摘要用祈使句的动词开头，宾语写成具体的名词（「trim the README to the facts the code cannot show」），不写成从句（「to what the code cannot tell」）。

| 错误写法 | 正确写法 |
|---|---|
| What Claude Code answers is markdown. | Claude Code answers in markdown. |
| Where each session is is written to state.json as it changes. | tracker.py writes the location of each session to state.json as it changes. |
| ## What you can send | ## Replies and commands |
| docs: say what it does in plain verbs | docs: describe the program in plain verbs |
| 用户所输入的内容是通过粘贴缓冲区完成传递的。 | input.py 把用户输入的内容写进 tmux 的粘贴缓冲区，再粘贴到终端里。 |

### 7. 情态照实写，不压成一般现在时

Claude 习惯删掉情态动词，把「通常」「可能」「可以」「应该」「需要」「必须」都写成一般现在时的陈述句。句子显得更笃定，读者却分不清这是总会发生的事实、偶尔发生的情况，还是需要自己去做的事。

* 一般现在时表示一件事每次都成立。写完一句一般现在时的句子，加上 always 再读一遍。如果加上以后句子不成立，就换成相应的情态词（usually、can、may、should、need、must），让读者知道这件事成立的程度。
* never 只表示频率，说的是一件事从未发生。说明一件事做不到时，写 cannot。

| 错误写法 | 正确写法 |
|---|---|
| The import takes several minutes. | The import can take several minutes on a large ledger. |
| This step fails on the first run. | This step may fail on the first run, before the cache exists. |
| Operators restart the service after editing the config. | Operators must restart the service after editing the config. |
| 用户在设置页修改数据路径。 | 用户需要在设置页修改数据路径。 |
| The parser never reads past the end of the buffer. | The parser cannot read past the end of the buffer. |

### 8. 句子写完整，格式不装饰

* 用正常语序写完整的句子。每一句都承接上一句，读者需要自己推断两句的关系时，用「since」「so」「however」「for example」这类连接词把关系写出来。新话题先交代再展开。
* 冒号后面只接列表、表格、图、公式或标签后的正文。引出解释时用「since」「which」「and」这类连词，或者另起一句，不用分号。
* 不用装饰性标记：不写加粗标签式的列表（「**Performance:** improved ...」），不用 emoji，不机械加粗。强调靠内容和结构，不靠格式。
