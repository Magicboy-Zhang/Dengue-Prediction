# Dengue-Prediction 登革热病例数量预测

This is the project for a course named 'MH6804-PYTHON FOR DATA ANALYSIS' from Fintech Master program of NTU.
这是一个叫做‘MH6804 Python数据分析’的南洋理工大学金融科技硕士专业的项目。

### Checklist 清单:

  - Basic Objectives 基本目标:
    - [x] preprocessing 数据预处理
   
    - [ ] KNN K最近邻
          
    - Linear Model 线性模型
      - [x] General Linear Model 一般线性模型
      - [x] Ridge 岭回归线性模型
      - [x] Lasso LASSO线性模型
            
    - Tree-based model 树模型
      - [x] Decision Tree 决策树
      - [x] Random Forest 随机森林
      - [x] XGBoost
     
    - Neural Network 神经网络
      - [x] MBSG 小批量随机梯度下降
      - [x] Adam
          
  - Optional Objectives 可选目标:
    - [ ] Train a model to fill the missing values 为有大量缺失值的特征训练模型以填补缺失值
    - [ ] Consider drop column 'ndvi_ne' since it's highly correlated with other features but has most missing values 考虑直接删除有大量缺失值的列，因为此特征与其他关键特征高度相关
    - [ ] Add more epoches to NN, some models did not reach their limits 考虑增加训练周期，结果仍然会变得更好
    - [ ] Record the parameters of the best NN 记录最好神经网络的权重/参数
   
---

### Introduction 简介：

Dengue Fever is an acute viral infection primarily transmitted to humans through mosquito bites. This disease is typically prevalent in tropical and subtropical regions, especially in Southeast Asia, the Pacific Islands, Central and South America, and the Caribbean. The goal of this project is to train machine learning models that utilizes time, meteorology, and vegetation data to predict the potential number of Dengue Fever cases within a specific time frame. An effective model could assist health authorities and governments in early detection of potential outbreaks, enabling them to implement appropriate preventive measures, thus reducing the impact of the disease on public health and society, which is a crucial public health initiative.

登革热（Dengue Fever）是一种急性病毒性感染疾病，它主要通过蚊子叮咬传播给人类。这种疾病通常在热带和亚热带地区流行，尤其在东南亚、太平洋地区、中南美洲和加勒比地区。本项目尝试构建机器学习模型，通过时间，气象以及植被数据预测特定时间内可能出现的登革热病例数量。有效的模型将能够帮助卫生部门和政府早期发现潜在的疫情爆发，采取适当的预防措施，减少疫情对人们健康和社会的影响是一项重要的公共卫生工作。

---

### Dataset Description 数据集描述：

##### 原始数据所有的特征：

##### 城市及时间：

<font color="blue">City</font>: 城市，分别是sj圣胡安，波多黎各首都；iq伊基托斯，秘鲁东北部城市  
<font color="blue">Year</font>: 数据记录时的年份  
<span style="color:blue">Weekofyear</span>: 数据记录时的当年的周数  
<span style="color:blue">Week_start_date</span>: 数据记录时的具体时间  

##### 卫星植被（健康和密度）-标准化差异植被指数（NDVI）-NOAA的气候数据记录标准化差异植被指数（0.5x0,5度规模）[数据的空间分辨率，即每个数据点表示地球表面的0.5度纬度和0.5经度的区域]:

<span style="color:blue">Ndvi_ne</span>: 城市中心东北方像素/区域（相对于城市中心东北方向区域的植被情况）  
<span style="color:blue">Ndvi_nw</span>: 城市中心西北方像素/区域（相对于城市中心西北方向区域的植被情况）  
<span style="color:blue">Ndvi_se</span>: 城市中心东南方像素/区域（相对于城市中心东南方向区域的植被情况）  
<span style="color:blue">Ndvi:sw</span>: 城市中心西南方像素/区域（相对于城市中心西南方向区域的植被情况）  

##### PERSIANN卫星降水测量（0.25x0.25度规模）:

<span style="color:blue">Precipitation_amt_mm</span>: 总降水量  

##### NOAA（美国国家海洋和大气管理局）的GHCN（全球历史气候网络）每日气候预报系统再分析测量（0.5x0.5度规模）:

<span style="color:blue">reanalysis_air_temp_k</span>：平均空气温度1（K）  
<span style="color:blue">reanalysis_avg_temp_k</span>：平均空气温度2（K）  
<span style="color:blue">reanalysis_dew_point_temp_k</span>：平均露点温度（K，指空气饱和并产生露水的温度，用于评估湿度）  
<span style="color:blue">reanalysis_max_air_temp_k</span>：最高空气温度（K）  
<span style="color:blue">reanalysis_min_air_temp_k</span>：最低空气温度（K）  
<span style="color:blue">reanalysis_precip_amt_kg_per_m2</span>：总降水量（千克每平方米）  
<span style="color:blue">reanalysis_relative_humidity_percent</span>：平均相对湿度  
<span style="color:blue">reanalysis_sat_precip_amt_mm</span>：总降水量（毫米）  
<span style="color:blue">reanalysis_specific_humidity_g_per_kg</span>：平均比湿（克每千克）  
<span style="color:blue">reanalysis_tdtr_k</span>：日温差（K）  

##### NOAA（美国国家海洋和大气管理局）的GHCN（全球历史气候网络）每日气候数据气象站测量：

<span style="color:blue">station_avg_temp_c</span>：当日平均温度（摄氏度）  
<span style="color:blue">station_diur_temp_rng_c</span>：当日昼夜温度范围（摄氏度）  
<span style="color:blue">station_max_temp_c</span>：当日最高气温（摄氏度）  
<span style="color:blue">station_min_temp_c</span>：当日最低气温（摄氏度）  
<span style="color:blue">station_precip_mm</span>：当日总降水量  

---

### Pre-processing 数据集预处理：

Loading the dataset, the target variable for this prediction is a continuous variable, so the goal is to train regression models. Data preprocessing is divided into two parts: generating standardized datasets for models like linear regression and non-standardized datasets for tree-based models.

First, by observing the dataset, we consider converting categorical variables into dummy variables. Therefore, we start by transforming the 'city' feature into dummy variables. Additionally, it is noticed that month can be derived from the 'Week_start_date' feature, and since the month can have a significant correlation with disease transmission (seasonal/temperature changes), the newly extracted 'month' feature is also converted into dummy variables. Finally, we remove unnecessary features like 'city,' 'year,' 'weekofyear,' and 'week_start_date' (do not consider time series). In the first attempt, we directly removed all data containing missing values and then proceeded with standardization.

Generating the non-standardized dataset follows basically the same process, except for not applying standardization in the final step.

In total, three new CSV files are generated:
  - 'label_drop_na_dengue.csv': Data containing the target variable with all missing value records removed.
  - 'scaled_feature_drop_na_dengue.csv': Data containing all features with missing value records removed and standardized.
  - 'feature_drop_na_dengue.csv': Data containing all features with missing value records removed withour standardized.

读取数据集，本次预测的变量为连续型变量，因此目的为训练回归模型。将数据集处理分为两类，分别生成标准化后的数据集，用于线性回归等模型；以及非标准化的数据集，用于树相关等模型。

首先观察数据集，考虑将其中的分类变量转换为哑变量，因此首先将特征city转换为哑变量。注意到能够从特征Week_start_date得到月份的数据，考虑到月份同样会与疾病的传播有很大程度的相关（季节/温度变化），因此将提取出来的新特征month也变成哑变量。最后，把无用的特征city，year，weekofyear，week_start_date（不考虑时间序列）删除。在第一次尝试中，我们直接删除了所有包含缺失值的数据，并随后进行了标准化。

生成非标准化的数据集基本遵循相同的流程，只是并未在最后阶段进行标准化。

总共生成三个新的csv文件：
  - label_drop_na_dengue.csv 删除了所有缺失值数据的包含了预测变脸的数据
  - scaled_feature_drop_na_dengue.csv 删除了所有缺失值数据并对所有特征标准化的数据
  - feature_drop_na_dengue.csv 删除了所有缺失值数据并未对所有特征标准化的数据

---

### Modeling 训练模型

### Results 结论

### Logs 日志

2023.10.30 Current lowest MAE: 13.99 目前的最低平均绝对值误差为 13.99

2023.10.30 Current lowest MAE: 12.07 目前的最低平均绝对值误差为 12.07

