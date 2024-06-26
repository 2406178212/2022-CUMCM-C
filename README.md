这是一个关于2022年大学生数学建模比赛（CUMCM）C题（**古代玻璃制品的成分分析与鉴别**）的**赛题讲解和论文复现**。在该项目中，针对赛题的每一个任务，借鉴优秀论文的做法，进行了求解，具体如下：

# 问题一的求解 #
1、对这些玻璃文物的表面风化与其玻璃类型、纹饰和颜色的关系进行分析；结合玻璃的类型，分析文物样品表面有无风化化学成分含量的统计规律，并根据风化点检测数据，预测其风化前的化学成分含量。

该赛题要求解决三个任务：
**①分析表面风化与其玻璃类型、纹饰和颜色的关系 
②分析不同玻璃类型下文物样品表面有无风化化学成分含量的统计规律 
③预测风化点风化前的化学成分含量**

思路：  
①对于第一小问，本质上属于**类别属性之间的相关性分析**，可用**卡方检验**进行分析，但需要注意卡方检验的适用条件，不满足的情况下考虑使用**Yates校正检验或Fisher精确检验**。  
②成分数据在单纯形空间取值，存在定和限制，传统统计方法失效，一般需要采用中心对数比CLR转换到欧式空间上。在进行**CLR变换**后，可考虑使用**方差分析**及**均值比较**对表面风化对各化学成分的影响进行研究。  
③本题风化前后样本量较少，机器学习算法效果不好，可在较强的分布假设下使用**总体分布匹配**的思想对风化前的化学成分进行预测。

# 问题二的求解 #
2、依据附件数据分析高钾玻璃、铅钡玻璃的分类规律；对于每个类别选择合适的化学成分对其进行亚类划分，给出具体的划分方法及划分结果，并对分类结果的合理性和敏感性进行分析。

该赛题要求解决三个任务：
**①分析高钾玻璃、铅钡玻璃的分类规律 
②对于每个类别的玻璃选择合适的化学成分对其进行亚类划分
③对分类结果的合理性和敏感性进行分析**

思路：  
①对于第一小问，可以考虑采用传统机器学习算法进行求解，如**决策树、随机森林、SVM**等。需要注意的是，要**给出哪些化学成分在玻璃分类起到了重要作用**，可参考**树模型的特征重要性**。  
②对化学成分进行**CLR变换**后，可先进行**特征筛选**，剔除信息量较少（或方差较小）的化学成分。为选出合适的化学成分，可考虑**对化学成分进行R型聚类**，再从各类中选择代表性化学成分**对样本进行Q型聚类**。注意要给出**亚类的划分方法**，可以通过**决策树、SVM等算法学习聚类的规则**。  
③可通过进行**对相关化学成分添加高斯噪声**进行敏感性测试，测试在不同程度扰动下分类结果的稳健性。

# 问题三的求解 #
3、对附件表单3中未知类别玻璃文物的化学成分进行分析，鉴别其所属类型，并对分类结果的敏感性进行分析。

该赛题要求解决两个任务：  
**①未知类别玻璃文物的类型鉴别
②分类结果的敏感性分析**

思路：  
①运用**问题二训练好的分类模型进行预测**
②可通过进行**对相关化学成分添加高斯噪声**进行敏感性测试，测试在不同程度扰动下分类结果的稳健性。

# 问题四的求解 #
4、针对不同类别的玻璃文物样品，分析其化学成分之间的关联关系，并比较不同类别之间的化学成分关联关系的差异性  

该赛题要求解决两个任务：  
**①分析不同玻璃类别的化学成分之间的关联关系
②不同类别之间的化学成分关联关系的差异性分析**

思路：  
①该问题本质上是**数值属性之间的相关性分析**，可考虑采用**皮尔逊相关系数、斯皮尔曼相关系数**等进行分析，选择具有**显著相关性的特征对**。考虑到上述相关系数仅能反映线性关系，还可以用**灰色关联分析**等研究其非线性关系。  
②差异性可通过找出**正负相关性在不同玻璃类型下不同的特征对**进行分析
