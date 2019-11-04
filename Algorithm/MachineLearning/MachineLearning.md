# Metrics
## Confusion Matrix：混淆矩阵
True Positive：将正类预测为正类数
True Negative：将负类预测为负类数
False Positive：将负类预测为正类数，误报
False Negative：将正类预测为负类数，漏报
-|实际Positive|实际Negative
---|---|---
预测Positive|TP|FP
预测Negative|FN|TN

## Metrics
* Accuracy
$Accuracy = \frac{TP+TN}{TP+FP+FN+TN}$
* Precision：预测Positive中有多少预测对了
$Precision = \frac{TP}{TP+FP}$
* Recall: 实际Positive中有多少预测出来了
$Recall =\frac{TP}{TP+FN}$
* Sensitivity：真正率，即Recall
$Sensitivity = Recall$
* Specificity：真负率 = 1 - 误正率 
$specificity = 1- \frac{FP}{FP+TN} = \frac{TN}{FP+TN}$
* F-score： Precision和Recall的加权和
$F = \frac{(a^2+1)PR}{a^2 (P+R)}, \space F1 = \frac{2PR}{P+R}$
* ROC curve
    * 纵轴 True Positive Rate 
        $Sensitivity = Recall = TP \space Rate$
    * 横轴 False Positive Rate
        $FP \space Rate = \frac{FP}{FP+TN}$
    漏报少了，误报就多了
    这两个metric是不会受imbalanced data影响（Precision会）
    曲线下的面积(AUC)越大，或者说曲线更接近左上角，那么模型就越好
* PR curve
    * 纵轴Precision，横轴Recall
    * 曲线下的面积(AUC)越大，或者说曲线更接近右上角，那么模型就越好

<<<<<<< HEAD
“宁可错杀一千，不可放过一个”呀。所以我们可以设定在合理的Precision下，最高的Recall作为最优点，找到这个对应的Threshold点。
=======
“宁可错杀一千，不可放过一个”呀。所以我们可以设定在合理的Precision下，最高的Recall作为最优点，找到这个对应的Threshold点。

* Top-1 error 的意思是：假如模型预测某张动物图片（一只猫）的类别，且模型只输出1个预测结果，那么这一个结果正好能猜出来这个动物是只猫的概率就是Top-1正确率。猜出来的结果不是猫的概率则成为Top-1错误率。简单来说就是模型猜错的概率。
* Top-5 error 的意思是：假如模型预测某张动物图片（还是刚才那只猫），但模型会输出来5个预测结果，那么这五个结果中有猫这个分类的概率成为Top-5正确率，相反，预测输出的这五个结果里没有猫这个分类的概率则成为Top-5错误率。
>>>>>>> bc5972ede73426075c5b41eb2eda1b3471ca8f11
