目前使用的代码分为两个来源：

**一、**陈老师GitHub——https://github.com/huanfachen/Travel_mode_prediction/tree/main/code

已经成功运行DNN_model_pipeline.py，还涉及以下模块

```python
Preprocess_data_DNN
Analysis_Neural_Net
Plot_Neural_Net
dnn
```

运行结果（以Original为例）包含：

1. 模型训练

   ![](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210724223249740.png)

2. 训练结果

   ![image-20210724223201581](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210724223201581.png)

3. 模型训练									

   |                             名称                             |                             图片                             |
   | :----------------------------------------------------------: | :----------------------------------------------------------: |
   | Original_dnn_mean_choice_prob_derivative_drive_cost_driving_total_.png | <img src="E:\USER_ermu\Documents\PycharmProjects\test_prediction\code\Plots\Original_dnn_mean_choice_prob_derivative_drive_cost_driving_total_.png" style="zoom: 33%;" /> |
   | Original_dnn_mean_choice_prob_drive_cost_driving_total_.png  | <img src="E:\USER_ermu\Documents\PycharmProjects\test_prediction\code\Plots\Original_dnn_mean_choice_prob_drive_cost_driving_total_.png" style="zoom:33%;" /> |
   |           Original_dnn_mean_drive_vot_hist___.png            | <img src="E:\USER_ermu\Documents\PycharmProjects\test_prediction\code\Plots\Original_dnn_mean_drive_vot_hist___.png" style="zoom:33%;" /> |
   |             Original_dnn_mean_pt_vot_hist___.png             | <img src="E:\USER_ermu\Documents\PycharmProjects\test_prediction\code\Plots\Original_dnn_mean_pt_vot_hist___.png" alt="Original_dnn_mean_pt_vot_hist___" style="zoom:33%;" /> |
   | Original_dnn_mean_subtitute_pattern_cost_driving_total__.png | <img src="E:\USER_ermu\Documents\PycharmProjects\test_prediction\code\Plots\Original_dnn_mean_subtitute_pattern_cost_driving_total__.png" alt="Original_dnn_mean_subtitute_pattern_cost_driving_total__" style="zoom:33%;" /> |

其中还有一些<font color='red'>**warning**</font>未解决，不过也可以运行：

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

**二、**GitHub——https://github.com/cjsyzwsh/dnn-for-economic-information

代码<font color='red'>2_analyze_model.py </font>中，若正常运行，则不会生成<font color='red'>”.pkl"</font>文件运行<font color='red'>3_plot.py</font>.

![image-20210725104256072](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210725104256072.png)

把上图部分注释掉，就可以生成<font color='red'>”.pkl"</font>文件，但会报错如下：

```
vot = m.util_derivative_test[drive_time,:,:] / m.util_derivative_test[drive_cost,:,:] / m.std[None, drive_time] * m.std[None, drive_cost] * time_correction
NameError: name 'time_correction' is not defined
```

根据以上报错，我直接在如下代码上方加一行		`time_correction=1`

![image-20210725110141894](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210725110141894.png)

```
RuntimeWarning: invalid value encountered in true_divide 
vot = m.util_derivative_test[drive_time,:,:] / m.util_derivative_test[drive_cost,:,:] / m.std[None, drive_time] * m.std[None, drive_cost] * time_correction

RuntimeWarning: Mean of empty slice. out=out, **kwargs)

RuntimeWarning: invalid value encountered in double_scalars ret = ret.dtype.type(ret / rcount)
```

3_plot也可以运行，生成以下四幅图

![image-20210725105520707](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210725105520707.png)

还是会报错：

![image-20210725110443579](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210725110443579.png)

上述Analysis 在模块analysis中，我用陈老师代码中的analysis替换后，运行plot生成以下内容：

![image-20210725111028192](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210725111028192.png)

**总结：**

​	目前所做工作如下图：

![](C:\Users\二木\AppData\Roaming\Typora\typora-user-images\image-20210725115540235.png)

​		已运行成功DNN_model_pipeline.py

​		正在尝试用Analysis_Neural_Net代替analysis

**主要问题：**

1. sys.exit()
2. github上的analysis，陈老师的analysis，还有陈老师的Analysis_Neural_Net ,三个模块作用相似吗，用哪一个更好一些？
3. 有没有新数据？新数据是什么类型，可以用程序序直接清洗吗？
4. 老师GitHub上，还有xgboost模型，也需要运行吗? 我在网上没有找到相同版本的xgboost，就还没有测试。
