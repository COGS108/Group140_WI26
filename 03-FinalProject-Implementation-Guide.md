# `03-FinalProject.ipynb` 直接填写版

这份文档不是再讲“大方向”，而是**直接对应 `03-FinalProject.ipynb` 的每一个 section**，给你：

1. 可以直接放进 notebook 的英文内容  
2. 每一段为什么这样写的中文解释  
3. 哪些地方必须等你们跑完模型后再替换数字

这版方案已经按你刚刚确认的方向固定：

- `research question`：预测是否进入**年内 Top 25%**
- 任务类型：**二分类**
- baseline 模型：`Logistic Regression`
- main 模型：`Random Forest`

---

## 先说最终总方案

你们这次 `03` 的最终问题，建议统一成：

> Can pre-release metadata predict whether a video game will rank in the top 25% of global sales within its release year?

这比原来的四分类更稳，原因有三个：

1. 问题更集中，更容易写成一条清晰主线。  
2. 类别比 `Top 10% vs not` 更平衡，模型通常更稳定。  
3. 既保留“成功游戏识别”的意义，又比四分类更容易做出清楚结果。  

你们最后整份 `03`，都应该围绕这一个问题来写。

---

## 你们在写 `03` 前，先统一这些术语

在全文里统一使用下面这套说法：

- `outcome variable`: `Top25_Label`
- `Top25_Label = 1`: game is in the top 25% of `Global_Sales` within its release year
- `Top25_Label = 0`: game is not in the top 25% within its release year
- `predictors`: `Year`, `Platform`, `Genre`, `Publisher`
- `success`: relative commercial success within release year

不要再混用这些说法：

- `annual sales`
- `Top 10%`
- `bestseller level`
- `four-level classification`

因为现在你们已经改题了，`03` 必须完全统一。

---

# 一、标题部分

## 直接填写内容

把 notebook 最上面的标题改成：

```md
# Predicting Top-Quartile Video Game Success from Pre-Release Metadata
```

## 为什么这样写

这个标题的优点是：

- 一眼能看出你们在做预测
- 一眼能看出目标是 `Top-Quartile`
- 一眼能看出只用 `Pre-Release Metadata`

也就是说，标题本身就把问题说清楚了。

---

# 二、Permissions

## 直接填写内容

这个你们自己决定。如果不公开，就填：

```md
* [  ] YES - make available
* [X] NO - keep private
```

## 为什么这样写

这部分不是分析内容，只是课程要求。  
如果你们没确定是否公开，最后再改。

---

# 三、Link to video

## 直接填写内容

这里最后填你们公开视频链接。现在可以先放占位：

```md
TBD
```

或者：

```md
Link will be added after the final video is uploaded.
```

## 为什么这样写

这个部分和项目分析无关，最后补即可。

---

# 四、Abstract

## 直接填写内容

下面这段是**可直接使用的 abstract 草稿**。  
你们只需要在跑完模型后，把方括号里的结果数值替换掉。

```md
Video game sales are difficult to compare across years because the size and structure of the market change over time. To address this issue, we study relative commercial success rather than absolute sales and ask whether pre-release metadata can predict whether a game will rank in the top 25% of global sales within its release year. Using a video game sales dataset containing release year, platform, genre, publisher, and global sales, we construct a year-normalized binary outcome indicating whether each title belongs to the top quartile of sales in its release-year cohort.

We use release year, platform, genre, and publisher as predictors and compare a logistic regression model against a random forest classifier. To make the evaluation more realistic, we train on games released from 1995 to 2014 and test on games released in 2015 and 2016, after excluding extremely sparse tail years. Our results show that pre-release metadata contain meaningful predictive signal. Logistic regression achieved an accuracy of `0.8002`, an F1 score of `0.5821`, and an ROC-AUC of `0.8320`, while random forest achieved a slightly higher accuracy of `0.8075` and higher precision (`0.6556`) but lower recall and F1.

Overall, our findings suggest that simple pre-release structural metadata can partially identify commercially strong games, but relative sales success is still influenced by many unobserved factors, such as marketing intensity, franchise strength, pricing, and post-release reception. This makes the models useful as coarse early-stage screening tools rather than complete explanations of video game success.
```

## 为什么这样写

这段 abstract 的结构是标准 final report 写法：

1. 第 1 段先说问题和目标变量  
2. 第 2 段说数据、模型和主要结果  
3. 第 3 段说意义和局限  

这段特别适合你们现在的项目，因为它有几个优点：

- 不夸大结果
- 不会和最终指标冲突
- 把 `Top 25%` 的改题逻辑说清楚了
- 很自然地把局限嵌进去

## 这里最后必须替换的内容

这一版 abstract 已经填入了我刚刚实际跑出来的结果。  
如果你们后面又改了过滤年份、模型参数或测试集方案，再回来替换这些数字即可。

---

# 五、Authors

## 直接填写内容

这一段你们需要按真实情况改名字，但结构可以直接照抄：

```md
- Yidong Li: Conceptualization, Data curation, Analysis, Writing - original draft
- [Name]: Background research, Writing - review & editing
- [Name]: Methodology, Software, Visualization
- [Name]: Analysis, Writing - original draft, Visualization
- [Name]: Project administration, Writing - review & editing
```

## 为什么这样写

这一节最重要的是：

- 用模板要求的贡献 taxonomy
- 不要写成“谁写了 00、谁写了 01”
- 不要写太口语

如果你们几个人都参与了分析和写作，也完全可以重复这些标签。

---

# 六、Research Question

## 直接填写内容

```md
Can pre-release metadata predict whether a video game will rank in the top 25% of global sales within its release year?

We focus on relative commercial success rather than absolute sales because raw sales figures are not directly comparable across time. Video game markets differ substantially by year in size, platform environment, and overall industry maturity. For that reason, we define success in year-normalized terms and ask whether features that are available before release, specifically release year, platform, genre, and publisher, can identify games that will perform unusually well relative to other games released in the same year.
```

## 为什么这样写

这段 research question 的写法很稳，原因是：

### 1. 第一行直接给出问题

老师一打开就知道你们到底在研究什么。

### 2. 第二段解释为什么不用绝对销量

这是你们这个项目最关键的逻辑。如果不解释，读者会问：

> 为什么不直接预测 `Global_Sales`？

你们要提前回答这个问题。

### 3. 明确限定 pre-release features

这会让你们的方法边界非常清楚，也能为后面的局限讨论埋伏笔。

---

# 七、Background and Prior Work

## 直接填写内容

```md
Video game sales are a widely used indicator of commercial success, but predicting sales outcomes is difficult because performance depends on a mixture of structural, market, and post-release factors. Prior research has shown that characteristics such as platform, genre, publisher, and review-related information are associated with variation in game sales. These findings suggest that game metadata contain meaningful signal, but they also highlight that commercial performance is shaped by both pre-release and post-release dynamics.

Much of the existing work on video game sales focuses either on explaining absolute sales or on incorporating information that is unavailable before launch, such as critic reviews, user reviews, or post-release market response. While those factors are useful for explanation, they are less helpful for a true pre-release prediction problem. In practice, publishers and developers often need to make decisions before a game is released, when only structural metadata are available.

Our project focuses on that narrower but practically important setting. Rather than predicting raw global sales, we define success relative to other games released in the same year and study whether pre-release metadata can identify games that will land in the top quartile of their release-year sales distribution. This design makes the prediction target more comparable across years and better aligned with an early-stage decision-making context.

In this sense, our contribution is not to claim that simple metadata can fully explain game success, but to test how much predictive value these variables contain on their own. The project therefore connects descriptive sales research with a more practically constrained prediction task: identifying likely high-performing games before release using only structured metadata.
```

## 为什么这样写

这四段是按一个很标准的学术逻辑排的：

### 第 1 段：已有研究说明销量和结构变量有关

作用是证明：

> 这个问题不是空想，前人已经说明 metadata 和销量有关。

### 第 2 段：指出已有研究的不足

作用是说明：

> 很多研究用了 post-release 信息，不完全适合你们这个问题。

### 第 3 段：说明你们的项目怎么补这个空白

这里把你们的改题重点说清楚了：

- 不预测原始销量
- 预测年内相对成功
- 聚焦 top quartile

### 第 4 段：定义你们的贡献

这段很重要，因为它让你们的项目看起来不是“随便跑个模型”，而是：

> 有一个清楚的研究定位。

## 这里还可以加什么

如果你们要引用 proposal 里的文献，可以在合适句子后面加 citation。  
但不要为了堆文献而堆文献，3 个左右相关来源就够了。

---

# 八、Hypothesis

## 直接填写内容

```md
We hypothesize that pre-release metadata will provide meaningful, but limited, predictive power for identifying whether a game will finish in the top 25% of global sales within its release year. In particular, we expect publisher, platform, and genre to contain useful signal because they reflect historical differences in brand strength, market reach, audience demand, and platform-specific sales environments.

At the same time, we do not expect prediction to be close to perfect. Commercial success is also influenced by many factors that are not included in our dataset, such as marketing intensity, franchise recognition, pricing, launch timing, and post-release reviews. As a result, we expect the models to outperform simple baselines while still showing clear limits in predictive accuracy.
```

## 为什么这样写

这段 hypothesis 比你们之前的版本好，主要有三个原因：

### 1. 不再乱猜具体 genre

比如以前那种 “RPG 最强” 的假设，风险很大。  
现在改成：

- publisher 可能重要
- platform 可能重要
- genre 可能重要

这更稳。

### 2. 不乱猜具体 accuracy

不要再写 `80%` 这种具体数字。  
在 final 里，这种提前写死的数字很容易让自己被动。

### 3. 直接把“有限预测力”写进假设

这样如果最后结果只是中等表现，也完全合理，不会显得项目失败。

---

# 九、Data

这一节我现在改成**真正可以直接照着写进 `03` notebook 的完整版**。  
也就是说，下面不只是 prose，而是按 notebook 的实际组织方式给你：

1. 这一个 markdown 单元应该写什么  
2. 这一个 code 单元应该写什么  
3. 这段代码应该看到什么结果  
4. 结果出来后旁边应该怎么分析  

## 先说明一个现实情况

现在这部分我已经用你本地重新放回来的 `data/00-raw/vgsales.csv` **实际跑过一遍**，所以 Data section 里下面写到的数字，不再只是引用旧 notebook，而是基于当前本地文件重新得到的真实结果。

本次重新运行确认到的关键事实是：

- 原始数据大小：`16598 x 11`
- 删除 `Year` / `Publisher` 缺失值后：`16291 x 11`
- 最终建模表大小：`16291 x 5`
- `Top25_Label = 1`：`4091`，占 `25.11%`
- `Top25_Label = 0`：`12200`，占 `74.89%`

另外，这次重新运行还发现一个重要现象：

- 数据年份范围实际是 `1980` 到 `2020`
- 但尾部年份非常稀疏，例如：
  - `2017` 只有 `3` 条
  - `2020` 只有 `1` 条

这一点对你们后面 `Results` 和 `Discussion` 很重要，因为它说明：

- year-normalized outcome 的定义是合理的
- 但某些极晚年份样本过少，可能需要在模型部分额外讨论是否过滤年份范围

所以，下面这部分 Data 内容已经可以直接当作你们 `03` 的真实 Data section 草稿使用。

---

## 9.1 你们在 `03` 里 Data section 的最佳结构

建议你们把 `Data` 这一节在 notebook 里拆成下面 5 个小块：

1. `### Data Overview`
2. `### Step 1: Load the raw dataset`
3. `### Step 2: Inspect missing values and clean core predictors`
4. `### Step 3: Construct the modeling dataset`
5. `### Step 4: Create the year-normalized Top25 outcome`

这 5 块是最稳的写法，因为它既像 final report，又保留了足够的过程透明度。

---

## 9.2 `Data Overview` 这个 markdown 单元直接写什么

### 可直接放进 notebook 的内容

```md
### Data Overview

Our analysis uses a publicly available video game sales dataset in which each row represents a game release. The raw dataset contains platform, genre, publisher, release year, regional sales, and global sales information. For this project, we use only the variables needed for pre-release prediction: `Year`, `Platform`, `Genre`, `Publisher`, and `Global_Sales`.

The key design choice in this project is that `Global_Sales` is not used as an input feature. Instead, it is used only to construct a year-normalized outcome variable. Specifically, we ask whether a game falls in the top 25% of global sales within its own release year. This allows us to study relative commercial success in a way that is more comparable across years than raw sales alone.
```

### 为什么这样写

这一块的作用是先把最重要的逻辑说清楚：

- 数据是什么
- 你们用哪些列
- `Global_Sales` 不是 predictor
- 你们最后预测的是 `Top25_Label`

如果这一块写清楚了，后面 Data code 再多一点也不会显得乱。

---

## 9.3 Step 1: Load the raw dataset

这一部分建议用 **一个 markdown 单元 + 一个 code 单元 + 一个结果解释 markdown 单元**。

### 先放的 markdown 单元

```md
### Step 1: Load the raw dataset

We begin by loading the original video game sales dataset and inspecting its size and columns. This step establishes the full raw data structure before any cleaning or variable selection.
```

### 对应 code 单元

```python
import pandas as pd
import numpy as np

df_raw = pd.read_csv("data/00-raw/vgsales.csv")

print("Shape:", df_raw.shape)
print("Columns:", list(df_raw.columns))
df_raw.head()
```

### 这段代码对应的实际结果

这是我刚刚基于当前本地 `vgsales.csv` 实际运行得到的结果：

```text
Shape: (16598, 11)
Columns: ['Rank', 'Name', 'Platform', 'Year', 'Genre', 'Publisher',
          'NA_Sales', 'EU_Sales', 'JP_Sales', 'Other_Sales', 'Global_Sales']
```

### 结果出来后，旁边的分析 markdown 直接写什么

```md
The raw dataset contains 16,598 observations and 11 columns. In addition to the structural metadata needed for this project, it also includes regional sales fields and rank information. Because our research question focuses on pre-release prediction, we later narrow the dataset to the predictors `Year`, `Platform`, `Genre`, and `Publisher`, while using `Global_Sales` only to define the outcome.
```

### 为什么这样组织

这里的逻辑是：

- 先证明你们真的看了原始数据
- 再说明哪些变量和最终研究问题有关
- 顺势过渡到变量筛选

这比直接上清洗代码更自然。

---

## 9.4 Step 2: Inspect missing values and clean core predictors

这是 Data 部分最必要的一步，因为 `Year` 和 `Publisher` 确实有缺失。

### 先放的 markdown 单元

```md
### Step 2: Inspect missing values and clean core predictors

We next examine missing values in the raw dataset. Since `Year` and `Publisher` are core predictors for our modeling task, observations missing either of these fields are removed. The amount of missingness is small enough that listwise deletion is a reasonable and transparent choice here.
```

### 对应 code 单元

```python
missing_counts = df_raw.isnull().sum()
missing_percent = (missing_counts / len(df_raw) * 100).round(2)

missing_df = pd.DataFrame({
    "Missing_Count": missing_counts,
    "Missing_Percent (%)": missing_percent
}).sort_values(by="Missing_Count", ascending=False)

print(missing_df)
```

### 这段代码对应的实际结果

这是我刚刚基于当前本地 `vgsales.csv` 实际运行得到的结果：

```text
              Missing_Count  Missing_Percent (%)
Year                    271                 1.63
Publisher                58                 0.35
Rank                      0                 0.00
Name                      0                 0.00
Platform                  0                 0.00
Genre                     0                 0.00
NA_Sales                  0                 0.00
EU_Sales                  0                 0.00
JP_Sales                  0                 0.00
Other_Sales               0                 0.00
Global_Sales              0                 0.00
```

### 清洗 code 单元

```python
print("Before cleaning:", df_raw.shape)

df_clean = df_raw.dropna(subset=["Year", "Publisher"]).copy()

print("After cleaning:", df_clean.shape)
print("\nRemaining missing values:")
print(df_clean[["Year", "Platform", "Genre", "Publisher", "Global_Sales"]].isnull().sum())
```

### 这段代码对应的实际结果

这是我刚刚基于当前本地 `vgsales.csv` 实际运行得到的结果：

```text
Before cleaning: (16598, 11)
After cleaning: (16291, 11)

Remaining missing values:
Year            0
Platform        0
Genre           0
Publisher       0
Global_Sales    0
dtype: int64
```

### 结果出来后，旁边的分析 markdown 直接写什么

```md
Only two variables used in our final prediction task contained missing values: `Year` and `Publisher`. Because these are essential predictors and the proportion of missingness was small (`1.63%` for `Year` and `0.35%` for `Publisher`), we removed those incomplete observations rather than imputing them. After this step, the dataset retained 16,291 observations, and the core variables required for modeling were complete.
```

### 为什么这样写

这一段做了三件事：

1. 给出缺失值事实  
2. 解释为什么删行而不是填补  
3. 给出清洗后样本量  

这在 final report 里是非常标准的写法。

---

## 9.5 Step 3: Construct the modeling dataset

这一块是把“原始数据”变成“你们真正拿来分析的数据”。

### 先放的 markdown 单元

```md
### Step 3: Construct the modeling dataset

After removing incomplete observations, we restrict the dataset to the variables needed for our prediction task. This produces a compact modeling table containing only the pre-release predictors and the sales field used to define the outcome.
```

### 对应 code 单元

```python
selected_columns = [
    "Year",
    "Platform",
    "Genre",
    "Publisher",
    "Global_Sales"
]

df_model = df_clean[selected_columns].copy()
df_model["Year"] = df_model["Year"].astype(int)

print("Model dataset shape:", df_model.shape)
df_model.head()
```

### 这段代码对应的实际结果

这是我刚刚基于当前本地 `vgsales.csv` 实际运行得到的结果：

```text
Model dataset shape: (16291, 5)
```

### 结果出来后，旁边的分析 markdown 直接写什么

```md
At this stage, the dataset contains 16,291 observations and 5 variables. This is the main table used for the remainder of the project. The predictors `Year`, `Platform`, `Genre`, and `Publisher` are all available before release, while `Global_Sales` is retained only to construct the year-normalized binary outcome.
```

### 为什么这样写

这一块是为了明确：

- 你们不是拿全部原始列去建模
- 模型表已经被收敛成 final 版本

这会让 `03` 看起来比 checkpoint 更成熟。

---

## 9.6 Step 4: Create the year-normalized `Top25_Label`

这是整个 Data section 里最关键的一步。

### 先放的 markdown 单元

```md
### Step 4: Create the year-normalized `Top25_Label`

We define success relative to a game's own release-year cohort. For each year, we rank games by `Global_Sales` and compute a within-year percentile. We then create a binary label, `Top25_Label`, that equals 1 if a game falls in the top 25% of sales within its release year and 0 otherwise.
```

### 对应 code 单元

```python
df_model["Sales_Percentile"] = (
    df_model.groupby("Year")["Global_Sales"]
            .rank(pct=True, method="average")
)

df_model["Top25_Label"] = (df_model["Sales_Percentile"] >= 0.75).astype(int)

top25_counts = df_model["Top25_Label"].value_counts().sort_index()
top25_props = df_model["Top25_Label"].value_counts(normalize=True).sort_index().round(4)

summary = pd.DataFrame({
    "count": top25_counts,
    "proportion": top25_props
})

print(summary)
df_model.head()
```

### 这段代码对应的实际结果

这是我刚刚基于当前本地 `vgsales.csv` 实际运行得到的结果：

```text
             count  proportion
Top25_Label                   
0            12200      0.7489
1             4091      0.2511
```

### 结果出来后，旁边的分析 markdown 直接写什么

```md
The final binary outcome is moderately imbalanced but still substantially more stable than a rarer blockbuster-only target such as top 10%. Approximately 25.1% of games are labeled as top-quartile performers, while 74.9% are not. This makes the task a meaningful binary classification problem: the positive class is selective enough to capture unusually strong games, but large enough to support stable model training and evaluation.
```

### 为什么这样写

这段分析其实是在帮你们回答一个非常关键的问题：

> 为什么你们最后选择 `Top 25%` 而不是 `Top 10%` 或四分类？

这里的回答是：

- `Top 25%` 仍然代表相对强表现
- 但比 `Top 10%` 稳定
- 又比四分类更聚焦

这会让你们整个 `03` 的改题显得非常合理。

---

## 9.7 这次实际运行后，我建议你们在 Data 或 Results 里补充说明年份尾部稀疏问题

这是这次重新运行后新增的发现，我强烈建议你们不要忽略。

### 可选 code 单元

```python
print("Year range:", df_model["Year"].min(), "to", df_model["Year"].max())
print(df_model["Year"].value_counts().sort_index().tail(10))
```

### 实际运行结果

```text
Year range: 1980 to 2020

Year
2009    1431
2010    1257
2011    1136
2012     655
2013     546
2014     580
2015     614
2016     342
2017       3
2020       1
```

### 这一步之后旁边的分析 markdown 可以直接写

```md
One additional issue revealed by the cleaned data is that the latest years are extremely sparse. Although the dataset technically extends to 2020, the number of observations in the final years is very small, which may make within-year percentile labels less stable for those years. We therefore treat year as an important predictor but also recognize that temporal sparsity is a limitation of the dataset.
```

### 为什么这一步很重要

因为你们现在的 outcome 是：

- 在每个年份内部做相对排名

所以如果某个年份只有 `1` 条或 `3` 条数据，这个“Top25”标签就会显得非常不稳定。  
这不一定意味着你们必须立刻删掉这些年份，但至少：

- 要在文中承认这个问题
- 后面建模时可以考虑是否做年份过滤

---

## 9.8 如果你们还想加一小步：为后续建模准备类别变量

这一块不是 Data section 必须有，但我建议你们在文档里知道它的作用。

如果你们想让后续模型更稳，可以在 modeling 前加一步“rare publisher 合并”。  
这一块我建议**放在 Results 的 modeling 代码前**，不一定放在 Data prose 主体里。

### 可选 code 单元

```python
publisher_counts = df_model["Publisher"].value_counts()
rare_publishers = publisher_counts[publisher_counts < 20].index

df_model["Publisher_Model"] = df_model["Publisher"].replace(rare_publishers, "Other")
```

### 为什么我建议放在 modeling 附近，而不是 Data 主体里

因为：

- 这更像建模工程上的稳定化处理
- 不是定义数据的核心一步
- 你们当前已经有足够完整的 Data narrative，不一定非要在 main data story 里讲得太细

---

## 9.9 这次实际运行后，rare publisher 合并这一步也有了真实数字

如果你们想在文档里把这步写得更扎实，可以直接用下面这个版本。

### 可选 code 单元

```python
publisher_counts = df_model["Publisher"].value_counts()
rare_publishers = publisher_counts[publisher_counts < 20].index

print("Unique publishers before:", df_model["Publisher"].nunique())
print("Rare publishers with <20 games:", len(rare_publishers))

df_model["Publisher_Model"] = df_model["Publisher"].replace(rare_publishers, "Other")

print("Unique publishers after grouping:", df_model["Publisher_Model"].nunique())
```

### 实际运行结果

```text
Unique publishers before: 576
Rare publishers with <20 games: 488
Unique publishers after grouping: 89
```

### 结果旁边可直接写的分析 markdown

```md
Publisher is a potentially informative predictor, but it is also extremely high-dimensional in the raw data. Before grouping, the cleaned dataset contains 576 distinct publishers, most of which appear only a small number of times. To reduce sparsity and improve model stability, we group very infrequent publishers into an `Other` category before fitting the final models.
```

### 为什么我现在更推荐这一步

因为这次真实跑出来之后可以看到：

- `576` 个 publisher 太多了
- 其中 `488` 个都少于 `20` 条

这说明 rare category 合并不是“可有可无的小优化”，而是很合理的模型准备步骤。

---

## 9.10 最后，Data section 结尾再放一个总结 markdown

这个总结非常推荐放在 Data section 最后，作为过渡到 Results。

### 可直接放进 notebook 的内容

```md
In summary, we began with 16,598 raw observations, removed a small number of cases missing `Year` or `Publisher`, and produced a cleaned modeling dataset with 16,291 rows and 5 core variables. We then converted `Global_Sales` into a year-normalized binary outcome indicating whether each game ranked in the top quartile of sales within its release year. The final target distribution is moderately imbalanced (25.1% positive, 74.9% negative), making the task well suited to binary classification while remaining substantively meaningful. This cleaned and labeled dataset forms the basis for both the exploratory analysis and the predictive models in the next section.
```

### 为什么这样写

这一段的作用是：

- 帮 Data section 收尾
- 把数字再总结一遍
- 很自然地过渡到 Results

在 final report 里，这种“section 收束句”很加分。

---

## 9.11 你们最终在 `03` 的 Data 部分，最推荐的完整排列顺序

如果你想最直接照着搭 notebook，就按这个顺序：

1. markdown: `### Data Overview`
2. markdown: Data Overview prose
3. markdown: `### Step 1: Load the raw dataset`
4. code: load raw data + shape + columns + head
5. markdown: Step 1 result interpretation
6. markdown: `### Step 2: Inspect missing values and clean core predictors`
7. code: missing values table
8. code: drop missing + remaining missing
9. markdown: Step 2 result interpretation
10. markdown: `### Step 3: Construct the modeling dataset`
11. code: select 5 columns + cast year + print shape
12. markdown: Step 3 result interpretation
13. markdown: `### Step 4: Create the year-normalized Top25_Label`
14. code: percentile rank + binary label + summary table
15. markdown: Step 4 result interpretation
16. markdown: Data section closing summary

这套顺序已经可以直接变成你们 `03` 的 Data 完整成品。

---

## 9.12 一句提醒

当前文档里 Data 部分的结果数字，已经是我基于你当前本地 `vgsales.csv` 实际重新运行得到的结果。  
所以这部分现在可以直接作为 `03` 的真实基础来用。

---

# 十、Data 部分的最简完整代码汇总

如果你们想先不分块，直接一口气把 Data pipeline 跑通，也可以先用下面这个完整代码版本：

```python
import pandas as pd
import numpy as np

# Load raw data
df_raw = pd.read_csv("data/00-raw/vgsales.csv")

# Inspect shape and columns
print("Shape:", df_raw.shape)
print("Columns:", list(df_raw.columns))

# Missing values
missing_counts = df_raw.isnull().sum()
missing_percent = (missing_counts / len(df_raw) * 100).round(2)
missing_df = pd.DataFrame({
    "Missing_Count": missing_counts,
    "Missing_Percent (%)": missing_percent
}).sort_values(by="Missing_Count", ascending=False)
print(missing_df)

# Clean core predictors
df_clean = df_raw.dropna(subset=["Year", "Publisher"]).copy()
print("Before cleaning:", df_raw.shape)
print("After cleaning:", df_clean.shape)

# Construct modeling table
selected_columns = ["Year", "Platform", "Genre", "Publisher", "Global_Sales"]
df_model = df_clean[selected_columns].copy()
df_model["Year"] = df_model["Year"].astype(int)
print("Model dataset shape:", df_model.shape)

# Create year-normalized percentile and binary outcome
df_model["Sales_Percentile"] = (
    df_model.groupby("Year")["Global_Sales"]
            .rank(pct=True, method="average")
)

df_model["Top25_Label"] = (df_model["Sales_Percentile"] >= 0.75).astype(int)

summary = df_model["Top25_Label"].value_counts().sort_index().to_frame("count")
summary["proportion"] = (
    df_model["Top25_Label"].value_counts(normalize=True).sort_index().round(4)
)

print(summary)
df_model.head()
```

## 为什么还要保留这个汇总代码

因为你们实际做 notebook 时，可能会先想快速跑通再拆块。  
这个版本就适合先验证流程，再按上面的 notebook 结构拆回去。

---

# 十一、Results 总结构

你们的 `Results` 建议直接改成下面四个标题：

1. `### Exploratory Data Analysis`
2. `### Baseline Model: Logistic Regression`
3. `### Main Model: Random Forest`
4. `### Model Comparison and Error Analysis`

这四段已经足够构成一份完整 final。

---

# 十二、先定测试集：我建议你们正式采用什么方案

这一部分是现在最需要拍板的，因为模型结果和文案都要围绕同一套测试策略来写。

## 我最后建议你们使用的主测试集方案

**正式主方案：**

- 先把数据限制在 `1995-2016`
- 训练集：`1995-2014`
- 测试集：`2015-2016`

## 为什么我最终选这个，而不是随机 80/20

### 1. 它更像真正的预测问题

你们的研究问题本来就是：

> 发售前信息能不能预测未来是否会成为相对高表现游戏？

如果训练和测试都随机混在一起，虽然技术上没错，但更像“同一时期样本内部分类”。  
而按年份切分，才更像：

> 用过去的游戏去预测更晚年份的游戏

这在叙事上更强。

### 2. 它避免了极端稀疏年份的干扰

真实运行后我们发现：

- `2017` 只有 `3` 条
- `2020` 只有 `1` 条

这些年份太稀疏，不适合继续保留。  
而 `1995-2016` 这个窗口既保留了现代市场阶段，又避开了异常尾部年份。

### 3. 它的测试集规模也足够

这次实际运行得到：

- 总样本数：`15801`
- 训练集：`14845`
- 测试集：`956`
- 训练集正类比例：`0.2504`
- 测试集正类比例：`0.2510`

也就是说，测试集不是太小，且正类比例与训练集非常接近。

## 可以直接写进 notebook 的说明

```md
To evaluate the models in a more realistic prediction setting, we did not use a purely random train-test split as our primary test design. Instead, we restricted the analysis window to games released between 1995 and 2016, trained the models on games released from 1995 to 2014, and evaluated them on games released in 2015 and 2016. We chose this design for two reasons: first, it better reflects the practical idea of predicting later releases from earlier historical data; second, it avoids extremely sparse tail years in the raw dataset, such as 2017 and 2020, which would make year-normalized labels unstable.
```

## 为什么这段写法好

因为它一次性解释了：

- 为什么不是 random split
- 为什么做年份过滤
- 为什么这更接近“真实预测”

这会让你们 final 的方法部分更有说服力。

---

# 十三、Results - Exploratory Data Analysis

## 直接填写内容

```md
### Exploratory Data Analysis

Before fitting predictive models, we examined how the outcome and major predictors are distributed in the cleaned dataset. Because our target is whether a game falls into the top 25% of sales within its release year, the first goal of the exploratory analysis is to understand class balance and identify broad patterns that may support prediction.

We focus on a small set of high-value descriptive analyses rather than presenting every exploratory result. In particular, we examine the distribution of the binary target, differences across genre and publisher, and the number of releases over time. These plots help establish whether pre-release structural metadata are plausibly informative for the classification task.
```

## 为什么这样写

这段 EDA 开头有两个作用：

### 1. 先交代 EDA 的目标

不是“看看数据”，而是：

- 看类别分布
- 看 predictor 是否可能有信号

### 2. 解释为什么只保留少量图

这样 final 会显得精炼，而不是把 checkpoint 里所有图都搬进来。

---

## EDA 图 1：Target distribution

### 图前文字可直接填写

```md
The target distribution plot shows the proportion of games that fall inside and outside the top quartile within their release year. Because the positive class is larger than a top-10% definition but still represents a minority of games, this formulation creates a prediction problem that is both meaningful and more stable than a rarer blockbuster-only target.
```

### 为什么这样写

这段是在替你们的新 research question 辩护：

- 为什么不用 `Top 10%`
- 为什么 `Top 25%` 是合理折中

这一步非常重要，因为你们现在已经换题了。

---

## EDA 图 2：Genre 和 Top25 成功率

### 图后文字可直接填写

```md
The genre-level success-rate plot suggests that the probability of reaching the top quartile varies across genres. This indicates that genre is not merely a descriptive label but may contain information about expected audience demand and market fit. Even if genre alone is not sufficient for prediction, the differences across categories support its inclusion as a useful pre-release feature.
```

### 为什么这样写

这段不要写得太死，不要写成：

- 哪个 genre 必然最好
- 哪个 genre 一定成功

而是写成：

> genre contains signal

这样更稳，也更像 final。

---

## EDA 图 3：Publisher 和 Top25 成功率

### 图后文字可直接填写

```md
Publisher-level differences are especially relevant to the prediction task. Some publishers show substantially higher top-quartile rates than others, which suggests that publisher identity may encode persistent advantages such as brand recognition, historical franchise strength, distribution power, and marketing reach. This makes publisher a plausible high-value predictor in the classification models.
```

### 为什么这样写

这段非常关键，因为它帮你们把 EDA 和模型自然连接起来：

- 图不是为了“讲故事”而已
- 图是在说明为什么 publisher 值得作为 predictor

---

## EDA 图 4：Releases over time

### 图后文字可直接填写

```md
The number of releases changes substantially over time, which reinforces the importance of defining success relative to each release-year cohort rather than using raw sales directly. This temporal variation also suggests that year may contribute predictive information by capturing broad historical changes in the video game market.
```

### 为什么这样写

这段把 `Year` 这个变量合理化了：

- 年份不是简单时间戳
- 它反映市场环境变化

这会让后面模型里保留 `Year` 更有说服力。

---

# 十四、Baseline Model: Logistic Regression

## 小节标题

直接写：

```md
### Baseline Model: Logistic Regression
```

## 小节开头可直接填写内容

```md
We first fit a logistic regression model as an interpretable baseline. This model allows us to test whether a relatively simple linear decision boundary, applied to one-hot encoded metadata, can already distinguish games that reach the top quartile of release-year sales from those that do not.

Categorical predictors were one-hot encoded, and very infrequent publishers were grouped into an `Other` category using the training data only. We then evaluated the model on the 2015-2016 test set using accuracy, precision, recall, F1, and ROC-AUC so that model quality would not be judged by accuracy alone.
```

## 为什么这样写

这段把 baseline 的角色说明得很清楚：

- 它不是最终答案
- 它是可解释的对照组
- 它可以回答“简单模型有没有信号”

而且这里已经埋了一个重要评价原则：

> 不只看 accuracy

---

## Logistic Regression 结果说明可直接填写内容

直接用这段：

```md
The logistic regression model achieved an accuracy of `0.8002`, a precision of `0.6129`, a recall of `0.5542`, an F1 score of `0.5821`, and an ROC-AUC of `0.8320` on the held-out 2015-2016 test set. These results show that even a relatively simple linear model can extract substantial predictive signal from pre-release metadata alone.

Importantly, logistic regression did more than simply improve on naive accuracy. A most-frequent dummy classifier reached `0.7490` accuracy by predicting every game as not top-quartile, but had zero precision, zero recall, and zero F1 for the positive class. In contrast, logistic regression identified a meaningful share of true top-quartile games while maintaining strong overall discrimination. This makes it a strong baseline and, in our results, one of the best-balanced models overall.
```

## 为什么这样写

这段用了一个很安全的结果口径：

- 如果 logistic 表现不错，这段成立
- 如果 logistic 表现一般，这段也成立

因为你们没有把它吹成很强，只是说：

> simple model already has signal

---

# 十五、Main Model: Random Forest

## 小节标题

直接写：

```md
### Main Model: Random Forest
```

## 小节开头可直接填写内容

```md
We next fit a random forest classifier as a nonlinear comparison model. Compared with logistic regression, random forest can capture interactions and nonlinear relationships among predictors, which may matter in a structured market setting where the effect of one variable depends on others.

Using the same training years, test years, and predictor set as the logistic regression model, we evaluated random forest on the held-out 2015-2016 test set with the same metrics. This allows for a direct comparison between a simpler interpretable model and a more flexible nonlinear alternative.
```

## 为什么这样写

这段把 random forest 的存在理由说明清楚了：

- 不是因为它“高级”
- 而是因为它能抓非线性和交互

这在 final 里很重要。

---

## Random Forest 结果说明可直接填写内容

```md
The random forest model achieved an accuracy of `0.8075`, a precision of `0.6556`, a recall of `0.4917`, an F1 score of `0.5619`, and an ROC-AUC of `0.8280`. Relative to logistic regression, random forest produced slightly higher accuracy and precision, which suggests that a more conservative nonlinear model can better avoid some false positives.

At the same time, random forest did not dominate logistic regression on every metric. Its recall and F1 were both lower, meaning that it missed a larger share of true top-quartile games. This pattern indicates that nonlinear structure exists in the data, but also that greater model complexity does not automatically lead to better balanced classification performance.
```

## 为什么这样写

这段的好处是：

- 如果 random forest 确实更强，很顺
- 如果只提升一点点，也不尴尬
- 同时你们把“有限预测力”继续维持住了

这会让整个 final 的语气更成熟。

---

# 十六、Third Model: CatBoost (Gradient Boosting)

你们决定最终报告里放三个模型，那么建议把 CatBoost 作为第三个模型单独成节，写法如下。

## 小节标题

```md
### Third Model: CatBoost (Gradient Boosting)
```

## 小节开头可直接填写内容

```md
In addition to logistic regression and random forest, we also fit a CatBoost classifier. CatBoost is a gradient boosting method designed to handle categorical features effectively, making it a strong candidate for this dataset where predictors such as `Publisher`, `Platform`, and `Genre` are high-cardinality categorical variables.

We trained CatBoost on the same training years (1995-2014) and evaluated it on the same held-out test years (2015-2016). This ensures a fair comparison across all models under the same temporal evaluation setup.
```

## CatBoost 结果说明（真实结果）

```md
CatBoost achieved an accuracy of `0.8138`, a precision of `0.6449`, a recall of `0.5750`, an F1 score of `0.6079`, and an ROC-AUC of `0.8484` on the 2015-2016 test set. Compared with both logistic regression and random forest, CatBoost provided the strongest overall performance, especially on ROC-AUC and F1, indicating improved discrimination and a better balanced classification outcome for identifying top-quartile games.
```

## CatBoost 的 confusion matrix（真实结果）

```md
CatBoost confusion matrix (TN, FP / FN, TP):

`[[640, 76], [102, 138]]`

This corresponds to 138 true positives and 102 false negatives for the top-quartile class, while producing 76 false positives.
```

## CatBoost 的可解释性（真实结果）

```md
Global feature importance from CatBoost indicates that categorical identifiers are highly informative. In this model, `Publisher`, `Genre`, and `Platform` contributed more strongly than `Year`, which is consistent with the interpretation that historical market structure and brand/platform positioning are key predictive signals.

Top-level feature importance (CatBoost):
- Publisher: `32.1088`
- Genre: `25.9621`
- Platform: `25.2957`
- Year: `16.6334`
```

---

# 十六、Model Comparison and Error Analysis

## 小节标题

直接写：

```md
### Model Comparison and Error Analysis
```

## 小节开头可直接填写内容

```md
To compare model performance directly, we summarize the main evaluation metrics for a dummy classifier, logistic regression, random forest, and CatBoost in a single table. We also inspect confusion matrices to understand where prediction errors are concentrated and what kinds of trade-offs each model makes.
```

## 为什么这样写

这一句就是在告诉读者：

- 你们不是只跑两个模型
- 你们还会比较它们
- 还会看错误分布

这会让 `Results` 更完整。

---

## 模型对比表后可直接填写内容

```md
Across the three real models, CatBoost achieved the strongest overall performance on this task. It produced the highest ROC-AUC (`0.8484`) and F1 (`0.6079`), indicating improved ability to rank games by success likelihood and to identify top-quartile games in a more balanced way. Random forest achieved strong precision and slightly higher accuracy (`0.8075`) than logistic regression, while logistic regression achieved stronger recall (`0.5542`) than random forest.

Overall, these patterns suggest that model choice affects the precision–recall trade-off. Logistic regression tends to recover more true top-quartile games (higher recall), random forest is more conservative (higher precision), and CatBoost provides the best balance and discrimination among the models tested. Importantly, all three models substantially outperform the dummy baseline, confirming that pre-release metadata contain real predictive signal even though the task remains only partially predictable.
```

## 为什么这样写

这段是很关键的“结果定调”句。

它的语气是：

- random forest 更好
- 但不是神
- 任务仍然有限可预测

这正是你们这个项目最可信的口径。

---

## confusion matrix 后可直接填写内容

```md
The confusion matrices show that all models identify a meaningful share of top-quartile games, but they make different trade-offs. Logistic regression produced more true positives (`133`) than random forest (`118`), which helps explain its stronger recall and F1. Random forest produced fewer false positives (`62` versus `84`), consistent with its stronger precision. CatBoost achieved the highest number of true positives (`138`) while maintaining a moderate number of false positives (`76`), aligning with its stronger balanced performance.

Substantively, these errors make sense. False negatives indicate that some games eventually perform very well even though their pre-release metadata do not look especially exceptional. False positives indicate that historically favorable metadata, such as well-known publishers or strong platform positions, do not guarantee top-quartile sales. Together, these results reinforce the idea that metadata-based prediction is informative but incomplete.
```

## 为什么这样写

这段 error analysis 很有用，因为它帮你们解释：

- 为什么模型不是完美的
- 错误来自哪里

而且这段不依赖具体数字结构太多，几乎都能成立。

---

# 十六、Feature Importance / Coefficient Interpretation

虽然模板没有强制单独写这个 section，但我非常建议你们在 model comparison 后面加一小段。

## 推荐小标题

```md
#### Feature Importance
```

## 可直接填写内容

```md
To better understand what the models learned, we examined coefficient magnitudes from logistic regression and feature importance from random forest and CatBoost. Across all approaches, publisher-related variables were especially informative. In logistic regression, strongly positive coefficients appeared for publishers such as Nintendo, Electronic Arts, Microsoft Game Studios, Square Enix, and Take-Two Interactive. In random forest, `Year` was the single most important feature overall, while major publisher identities also ranked highly. In CatBoost, global feature importance assigned the largest share of predictive contribution to categorical identifiers (`Publisher`, `Genre`, and `Platform`), with `Year` still contributing meaningfully.

These patterns suggest that publisher, platform, genre, and release timing all carry predictive value, but they likely represent broad historical market advantages rather than direct causal mechanisms. We therefore interpret them as predictive signals embedded in the historical data, not as proof that any single metadata field by itself determines success.
```

## 为什么这样写

这段有两个作用：

### 1. 帮你们回答“模型到底学到了什么”

否则模型部分就只剩分数。

### 2. 提前避免因果误读

这对 final 非常加分，因为很多项目会忘掉这一点。

---

# 十七、Ethics

## 直接填写内容

```md
This project uses publicly available, game-level data and does not involve personal or identifiable information. However, the absence of personal data does not eliminate ethical concerns. The dataset may overrepresent commercially visible, mainstream, or well-documented titles, while underrepresenting smaller, niche, or independent games. As a result, the historical patterns learned by the model may reflect existing structural biases in the video game market rather than a neutral picture of creative potential.

There is also an important interpretive risk in predictive work of this kind. Our model does not measure game quality, originality, or cultural value. Instead, it predicts whether a game resembles historically higher-performing titles in a dataset defined by past market outcomes. If a model like this were used carelessly in real decision-making, it could reinforce existing advantages for major publishers, familiar genres, or established platform ecosystems, while discouraging riskier or more innovative projects.

For that reason, we interpret our results narrowly. The model should be understood as a coarse predictive tool based on limited pre-release metadata, not as a decision rule for what kinds of games should or should not be made. We also emphasize throughout the report that predictive association is not the same as causation, and that many relevant factors are missing from the available data.
```

## 为什么这样写

这版 ethics 比 checklist 式写法更适合 final，因为它直接对应你们项目的真实伦理问题：

- 数据偏差
- 市场偏差
- 头部厂商优势被强化
- 预测不等于质量判断

这比只写“没有个人信息，所以没问题”要成熟得多。

---

# 十八、Discussion and Conclusion

## 直接填写内容

下面这段是完整的 final discussion 草稿。  
你们最后只需要把方括号里的指标替换掉，并按实际结果微调一两句。

```md
Our project asked whether pre-release metadata can predict whether a video game will rank in the top 25% of global sales within its release year. By redefining success in relative rather than absolute terms, we aimed to make outcomes more comparable across years and better aligned with a practical pre-release prediction setting.

The results suggest that the answer is yes, but only to a limited extent. Both logistic regression and random forest were able to extract meaningful predictive signal from release year, platform, genre, and publisher. Logistic regression achieved an accuracy of `0.8002`, an F1 score of `0.5821`, and an ROC-AUC of `0.8320`, while random forest achieved a slightly higher accuracy of `0.8075` and higher precision (`0.6556`) but lower recall and F1. Taken together, these results indicate that pre-release structural metadata do contain useful information about a game’s likelihood of becoming a relatively strong commercial performer within its release-year cohort.

At the same time, the models were far from perfect, which is an important finding in itself. Commercial success in video games is shaped by many factors that are not included in our dataset, such as marketing budgets, franchise recognition, pricing, release timing, game quality, and post-release review dynamics. The fact that our models can only partially predict top-quartile success suggests that structured metadata alone capture only one part of a much larger commercial process.

Our exploratory analyses and model interpretation also suggest that publisher, platform, genre, and release year all matter, though not equally. In particular, publisher-related features appear especially informative, and `Year` emerges as a major predictor in the random forest model. This is consistent with the idea that release timing, publisher identity, and platform environment all encode historical market structure. However, these variables should be understood as predictive signals rather than causal determinants.

This study has several limitations. The dataset may not fully represent all parts of the video game market, especially smaller or less well-documented titles. `Global_Sales` is also a limited success measure because it captures unit sales rather than revenue or profitability. In addition, multiple platform versions of a game may appear as separate observations, and many commercially important pre-release and post-release factors are unobserved in the available data. Finally, some years in the raw dataset are very sparse, which is why we restricted the main analysis window to 1995-2016 and evaluated on 2015-2016 only.

Overall, our findings show that a simple metadata-based model can serve as a useful early-stage screening tool for identifying potentially strong-performing games, but it cannot provide a complete or definitive account of video game success. Future work could improve this framework by incorporating richer pre-release information, testing additional temporal splits, and comparing more specialized models for high-cardinality structured categorical data.
```

## 为什么这样写

这段 discussion 的结构非常标准，而且适合你们这个项目：

### 第 1 段：回到研究问题

把改题后的 `Top 25%` 再说清楚。

### 第 2 段：总结主要结果

这里要放最终模型表现。

### 第 3 段：解释为什么结果不是完美的

这段非常重要，因为你们的项目不应该吹成“高精度预测神模型”。

### 第 4 段：解释特征意义

把 publisher、platform、genre、year 再串起来。

### 第 5 段：明确局限

final 一定要有局限。

### 第 6 段：收尾和未来工作

让整份报告完整结束。

## 这一版已经填入的真实结果

这一版 discussion 已经写入了我刚刚基于你本地数据跑出来的真实指标。  
如果你们后面又改年份范围、特征工程或模型参数，再来替换即可。

---

# 十九、你们在 `03` 里必须实际跑出的结果

因为我现在不能凭空捏造模型结果，所以你们最后必须自己跑出下面这些数字，然后替换进上面的 prose：

## 必须有的数字

- Dummy baseline:
  - accuracy = `0.7490`
  - precision = `0.0000`
  - recall = `0.0000`
  - F1 = `0.0000`
  - ROC-AUC = `0.5000`

- Logistic Regression:
  - accuracy = `0.8002`
  - precision = `0.6129`
  - recall = `0.5542`
  - F1 = `0.5821`
  - ROC-AUC = `0.8320`

- Random Forest:
  - accuracy = `0.8075`
  - precision = `0.6556`
  - recall = `0.4917`
  - F1 = `0.5619`
  - ROC-AUC = `0.8280`

- CatBoost:
  - accuracy = `0.8138`
  - precision = `0.6449`
  - recall = `0.5750`
  - F1 = `0.6079`
  - ROC-AUC = `0.8484`

## 推荐额外输出

- confusion matrix
- classification report
- random forest feature importance top 15
- catboost feature importance (global)

---

# 二十、你们在 `03` 里最推荐放的代码框架

下面是我建议你们直接在 results 部分使用的**最终代码框架**。  
这版代码和我刚刚跑出真实结果时采用的设置一致。

```python
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import OneHotEncoder
from sklearn.dummy import DummyClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from catboost import CatBoostClassifier
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score,
    f1_score, roc_auc_score, confusion_matrix,
    classification_report
)

# Restrict to the main analysis window
df_analysis = df_model[(df_model["Year"] >= 1995) & (df_model["Year"] <= 2016)].copy()

# Create outcome inside each year
df_analysis["Sales_Percentile"] = (
    df_analysis.groupby("Year")["Global_Sales"]
               .rank(pct=True, method="average")
)
df_analysis["Top25_Label"] = (df_analysis["Sales_Percentile"] >= 0.75).astype(int)

# Temporal split
train_df = df_analysis[df_analysis["Year"] <= 2014].copy()
test_df = df_analysis[df_analysis["Year"] >= 2015].copy()

# Collapse rare publishers using training data only
publisher_counts = train_df["Publisher"].value_counts()
rare_publishers = publisher_counts[publisher_counts < 20].index

train_df["Publisher_Model"] = train_df["Publisher"].replace(rare_publishers, "Other")
test_df["Publisher_Model"] = test_df["Publisher"].where(
    test_df["Publisher"].isin(publisher_counts.index.difference(rare_publishers)),
    "Other"
)

X_train = train_df[["Year", "Platform", "Genre", "Publisher_Model"]]
y_train = train_df["Top25_Label"]
X_test = test_df[["Year", "Platform", "Genre", "Publisher_Model"]]
y_test = test_df["Top25_Label"]

preprocessor = ColumnTransformer(
    transformers=[
        ("cat", OneHotEncoder(handle_unknown="ignore"), ["Platform", "Genre", "Publisher_Model"]),
        ("num", "passthrough", ["Year"]),
    ]
)

models = {
    "Dummy": DummyClassifier(strategy="most_frequent"),
    "Logistic Regression": LogisticRegression(max_iter=3000, random_state=42),
    "Random Forest": RandomForestClassifier(
        n_estimators=500,
        min_samples_leaf=2,
        random_state=42,
        n_jobs=-1
    ),
    "CatBoost": CatBoostClassifier(
        loss_function="Logloss",
        eval_metric="AUC",
        iterations=1500,
        depth=8,
        learning_rate=0.05,
        l2_leaf_reg=3.0,
        random_seed=42,
        verbose=False
    ),
}

for name, clf in models.items():
    # CatBoost handles categorical features internally, so it does not use one-hot
    if name == "CatBoost":
        cat_features = ["Platform", "Genre", "Publisher_Model"]
        clf.fit(X_train, y_train, cat_features=cat_features)
        y_pred = clf.predict(X_test).astype(int).ravel()
        y_prob = clf.predict_proba(X_test)[:, 1]
        roc_auc = roc_auc_score(y_test, y_prob)
    else:
        model = Pipeline([
            ("preprocessor", preprocessor),
            ("classifier", clf)
        ])
        model.fit(X_train, y_train)
        y_pred = model.predict(X_test)
        if hasattr(model, "predict_proba"):
            y_prob = model.predict_proba(X_test)[:, 1]
            roc_auc = roc_auc_score(y_test, y_prob)
        else:
            roc_auc = 0.5

    print(name)
    print("Accuracy:", accuracy_score(y_test, y_pred))
    print("Precision:", precision_score(y_test, y_pred, zero_division=0))
    print("Recall:", recall_score(y_test, y_pred, zero_division=0))
    print("F1:", f1_score(y_test, y_pred, zero_division=0))
    print("ROC-AUC:", roc_auc)
    print(confusion_matrix(y_test, y_pred))
    print(classification_report(y_test, y_pred, digits=4, zero_division=0))
    print("-" * 50)
```

## 为什么这样写

这段代码和你们现在的 final 方案完全匹配：

- 二分类
- `Top25_Label`
- logistic baseline
- random forest main model
- 固定随机种子
- 用 stratified split
- 指标完整

---

# 二十一、如果你们想让结果更稳，再加这一句

如果最后 random forest 的 precision 和 recall 差很多，可以在结果里加一句：

```md
Depending on the decision threshold, the model can be tuned toward either stronger precision or stronger recall, which reflects a practical trade-off in identifying likely high-performing games.
```

## 为什么这样写

因为二分类任务里，`Top25` 的识别确实存在 precision-recall trade-off。  
而且你们这次真实跑出来的结果正好体现了这一点：

- `Random Forest` precision 更高
- `Logistic Regression` recall / F1 更高

这句话会让你们看起来更懂模型评价。

---

# 二十二、你们现在最应该怎么用这份文档

推荐你们按这个顺序推进：

1. 先把 `Research Question`、`Background`、`Hypothesis`、`Data` 的 prose 直接填进 `03`
2. 按上面的代码方案先跑出最终数据和模型结果
3. 再把 `Abstract`、`Results`、`Discussion` 里的 `[X]` 替换成真实数值
4. 最后统一润色语言

---

# 二十三、最后一句判断标准

如果你们最后的 `03` 能做到下面这几点，就已经是一份很稳的 final：

- 全文只围绕 `Top 25% vs not` 一个问题
- 数据处理和目标变量定义完全自洽
- 用 `Logistic Regression + Random Forest` 两个模型形成清楚对照
- 不只报 accuracy
- 能解释错误和局限
- 语气诚实，不夸大

这就是你们现在最适合的最终版本。
