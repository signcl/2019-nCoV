# 2019-nCoV Hackathon 新冠肺炎关联指征数据集
本项目希望基于新冠肺病关联指征定义，筛选肺病CT影像公开数据集中的包含有关联指征的病例，进一步形成对应的关联指征数据集，以用于新冠肺病的CT影像模型构建。
## 新冠肺病CT影像指征词表
国家卫健委下发的《新型冠状病毒感染的肺炎诊疗方案（试行第三版）》的「胸部影像学」一栏中的说明：
早期呈现多发小斑片影及间质改变，以肺外带明显。进而发展为双肺多发磨玻璃影、浸润影，严重者可出现肺实变，胸腔积液少见。

依据目前阶段对呼吸科医学专家的咨询，我们应该关注的病理特征中英文对照如下：

优先指征：
- 磨玻璃影 - ground glass
- 实变 - consolidation
- 胸腔积液 - pleural effusion
- 浸润影 - infiltration

次级指征（无明确相关性）：
- 蜂窝肺 - honeycombing（honeycomb）
- 网格影 - reticular
- 小叶间隔增厚 - septal thickening
- 结节 - nodules
- 支气管扩张 - bronchiectasis
- 气胸 - pneumothorax
- 囊性变 - cyst

## 数据标注规范
为了方便统一训练模型，我们使用指定的 OpenBayes 数据格式进行建模，在医疗建模的分割模型上，我们使用的数据格式如下：

OpenBayes 数据格式以 meta.csv 为数据集的主要格式文件，文件以 csv 格式为主体：

- 第一行为字段类型和字段名称，格式为：[类型]_[名称]
- 第二行以及以后每一行为数据样本。

因为分割模型使用的数据和标注都是图片，所以每一行的数据样本中，写好对应图片的相对路径即可。每个特性分别使用一张对应大小的图片表示标注结果。

特性对应颜色取值：

- 磨玻璃影 - FF0000
- 蜂窝肺 - FFFF00
- 网格影 - FF00FF
- 小叶间隔增厚 - 00FFFF
- 结节 - 00FF00
- 实变 - 008000
- 支气管扩张 - FFFACD
- 气胸 - 7FFF00
- 胸腔积液 - 0000FF
- 囊性变 - 000080
- 浸润影 - 808000

## 样例说明

001_[标注特性].jpg 和 001.jpg 是相同大小的两张图片，001_[标注特性].jpg 中每个像素是 001.jpg 对应位置的标注。

为了以后数据校验，我们在图片文件夹中，还需要再放上原始 DICOM 或 MAT 文件（001.dcm），以防出现不一致。

    image_Label,image_Source
    patient_00/001_ground_glass.png,patient_00/001.png
    patient_00/001_honeycombing.png,patient_00/001.png

目录结构：

    .
    ├── meta.csv
    ├── patient_00
    │   ├── 001.png
    │   ├── 001.dcm
    │   └── 001_ground_glass.png
    │   └── 001_honeycombing.png

数据集：
* DeepLesion - 磨玻璃
* LUNA
* ChestX-ray8 - 胸腔积液 Effusion

需要查看
* [LIDC-IDRI](https://wiki.cancerimagingarchive.net/display/Public/LIDC-IDRI#194132fe653e4a7db00715f6f775c012)
* [Anti-PD-1_Lung](https://wiki.cancerimagingarchive.net/pages/viewpage.action?pageId=41517500#c0c9c53e1cf344258616034371440942)
* [Anti-PD-1_MELANOMA](https://wiki.cancerimagingarchive.net/pages/viewpage.action?pageId=37225348#c0c9c53e1cf344258616034371440942)
* CPTAC-CCRCC
* CPTAC-GBM
* CPTAC-HNSCC
* CPTAC-PDA
* CPTAC-UCEC
* NSCLC Radiogenomics
* TCGA-BLCA
* TCGA-COAD
* TCGA-HNSC
* TCGA-LUSC
* TCGA-UCEC
* DLCST
