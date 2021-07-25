目前使用的代码分为两个来源：

一、陈老师GitHub——https://github.com/huanfachen/Travel_mode_prediction/tree/main/code

已经成功运行DNN_model_pipeline.py，还涉及以下模块

```python
Preprocess_data_DNN
Analysis_Neural_Net
Plot_Neural_Net
dnn
```

运行结果（以Original为例）包含：

1. 模型训练

   Original dnn_Model.pkl
   Original_dnn_model_0.ckpt.data-00000-of-00001
   Original_dnn_model_0.ckpt.index
   Original_ dnn_model_0.ckpt.meta

2. 训练结果

   Original_dnn_0.csv
   Original_dnn_1.csv
   Original dnn 2.csv
   ......
   Original_dnn_9.csv
   Original dnn mean.csv

3. 模型训练			

   Original_dnn_mean_choice_prob_derivative_drive_cost_driving_total_.png	

   Original_dnn_mean_choice_prob_drive_cost_driving_total_.png	

   Original_dnn_mean_drive_vot_hist___.png				

   Original_dnn_mean_pt_vot_hist___.png

   Original_dnn_mean_subtitute_pattern_cost_driving_total__.png

其中还有一些warning未解决，不过也可以运行：

```
UserWarning: Attempting to set identical left == right == -8.536162387791736 results in singular transformations; automatically expanding.ax.set_xlim([np.percentile(avg_vot, 5), np.percentile(avg_vot, 95)])
UserWarning: Warning: 'partition' will ignore the 'mask' of the MaskedArray.a.partition(kth, axis=axis, kind=kind, order=order)
FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'._np_qint8 = np.dtype([("qint8", np.int8, 1)])
```

collate_result.py 运行失败，如下

```
'NoneType' object is not subscriptable；
'NoneType' object has no attribute 'startswith'
```

二、GitHub——https://github.com/cjsyzwsh/dnn-for-economic-information

代码2_analyze_model.py 中，若正常运行，则不会生成”.pkl"文件运行3_plot.py

```
# sys.exit()
# print(np.mean(np.sum(m.sw_change_0,axis=1)))
# print(np.mean(np.sum(m.sw_change_1,axis=1)))
# print(np.mean(np.sum(m.sw_change_2,axis=1)))
# print(np.mean(np.sum(m.sw_change_3,axis=1)))
```

把以上部分注释掉，就可以生成”.pkl"文件，但会报错如下：

```
vot = m.util_derivative_test[drive_time,:,:] / m.util_derivative_test[drive_cost,:,:] / m.std[None, drive_time] * m.std[None, drive_cost] * time_correction
NameError: name 'time_correction' is not defined
```

根据以上报错，我直接在如下代码上方加一行		`time_correction=1`

```
RuntimeWarning: invalid value encountered in true_divide 
vot = m.util_derivative_test[drive_time,:,:] / m.util_derivative_test[drive_cost,:,:] / m.std[None, drive_time] * m.std[None, drive_cost] * time_correction

RuntimeWarning: Mean of empty slice. out=out, **kwargs)

RuntimeWarning: invalid value encountered in double_scalars ret = ret.dtype.type(ret / rcount)
```

3_plot也可以运行，生成以下四幅图

model15_7000_3_vot_drive_test.png

model15_7000_3_vot_drive_train.png

model15_7000_vot_drive_test.png

model15_7000_vot_drive_train.png

全是空白的

还是会报错：

```
print(np.mean(m.mkt_share,axis = 0))
AttributeError:'Analysis' object has no attribute 'mkt_share'
```

上述Analysis 在模块analysis中，我用陈老师代码中的analysis替换后，运行plot生成以下内容：

model15_7000_3_vot_drive_test.png

model15_7000_3_vot_drive_train.png

model15_7000_vot_drive_test.png

model15_7000_vot_drive_train.png

都是有内容的图片

总结：

​	目前所做工作如下图：

​		已运行成功DNN_model_pipeline.py

​		正在尝试用Analysis_Neural_Net代替analysis

主要问题：

1. sys.exit()
2. github上的analysis，陈老师的analysis，还有陈老师的Analysis_Neural_Net ,三个模块作用相似吗，用哪一个更好一些？
3. 有没有新数据？新数据是什么类型，可以用程序序直接清洗吗？
4. 老师GitHub上，还有xgboost模型，也需要运行吗? 我在网上没有找到相同版本的xgboost，就还没有测试。