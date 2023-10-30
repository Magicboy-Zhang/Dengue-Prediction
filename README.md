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
    - [ ] Record the parameters of the best NN

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

### Modeling

### Results

### Logs 日志

2023.10.30 Current lowest MAE: 13.99 目前的最低平均绝对值误差为 13.99

2023.10.30 Current lowest MAE: 13.99 目前的最低平均绝对值误差为 12.07

