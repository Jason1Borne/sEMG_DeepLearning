# 基于表面肌电信号的动作识别（深度学习）

## 1、sEMG的基础知识
**sEMG的产生：** 表面肌电信号是由**多个运动单元**发放的**动作电位序列**，在皮肤表面呈现的**时间上和空间上**综合叠加的结果。

**sEMG的特点：**
* 幅值一般和肌肉运动力度成正比，能精确的反映肌肉自主收缩力
* 超前于人体运动30-150ms产生

![肌电信号生成图片](https://github.com/malele4th/sEMG_DeepLearning/blob/master/picture/sEMG_generation.png)

**基于sEMG的动作识别一般处理流程（传统机器学习）：**

（1）离线采集sEMG
* 定义动作数量、动作类型
* 选择采集设备：Delsys(2000Hz)、Myo(100Hz)、OttoBock(100Hz)、高密度阵列式等
* 肌肉位置的选择、电极数量的选择：根据肌肉解剖位置调整电极
* 引导方式：图片、语音
* 采集流程：休息+动作循环采集
* 休息时间、动作时间，动作维持的力的大小，动作的姿势尽量保持一致

（2）数据预处理
* 10-350Hz带通滤波器，50Hz陷波器
* 标签修正：数据裁剪、最大面积法、极大似然修正
* 样本不均衡问题：休息动作的处理（通过阈值）
* 特征归一化：min-max标准化、标准差归一化
* 数据增强：加高斯噪声、翻转信号通道、时间窗+增量窗

（3）特征提取：时域、频域、时频域（tsfresh库）

（4）特征选择：
* 过滤法：方差选择法、相关系数法、卡方检验、互信息法，评估单个特征和结果值之间的相关程度，排序留下Top相关的特征部分
* 包裹型：递归特征删除法、基于学习模型的特征排序
* 嵌入型：正则化方法（L1正则化筛选特征）

（5）特征降维：
* PCA、LDA、SVD分解、流行学习LLE（非线性降维）、自编码器AE、T-SNE

（6）模型训练：
* KNN、LDA、DT、LR、NB、SVM、ANN
* RF、AdaBoost、GBDT、LightGBM、XGBoost
* AE、MLP、深层玻尔兹曼机、深层信念网络、CNN、RNN、LSTM、Inception、Attention
* 迁移学习、GAN

（7）控制决策：

## 2、数据集 

NinaPro 数据集

[NinaWeb](http://ninapro.hevs.ch/node/7)
[NinaPro数据下载及数据说明](https://datadryad.org//resource/doi:10.5061/dryad.1k84r)

