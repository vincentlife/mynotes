
# tensorflow版本对应

tensorflow-gpu v1.9.0 | cuda9.0 |  cuDNN7.1.4可行  | 备注：7.0.4/ 7.0.5/ 7.1.2不明确

tensorflow-gpu v1.8.0 | cuda9.0 |  cuDNN  不明确 | 备注：7.0.4/ 7.0.5/ 7.1.2/ 7.1.4

tensorflow-gpu v1.7.0 | cuda9.0 |  cuDNN  不明确 | 备注：7.0.4/ 7.0.5/ 7.1.2/ 7.1.4

tensorflow-gpu v1.6.0 | cuda9.0 |  cuDNN  不明确 | 备注：7.0.4/ 7.0.5/ 7.1.2/ 7.1.4

tensorflow-gpu v1.5.0 | cuda9.0 |  cuDNN  不明确 | 备注：7.0.4/ 7.0.5/ 7.1.2/ 7.1.4

tensorflow-gpu v1.4.0 | cuda8.0 |  cuDNN 6.0 | 备注：6.0正常使用, 7.0.5不能用，5.1未知 

tensorflow-gpu v1.3.0 | cuda8.0 |  cuDNN 6.0 | 备注：6.0正常使用, 7.0.5不能用，5.1未知 

tensorflow-gpu v1.2.0 | cuda8.0 |  cuDNN 5.1 | 备注：5.1正常使用, 6.0/ 7.0.5 未知

tensorflow-gpu v1.1.0 | cuda8.0 |  cuDNN 5.1 | 备注：5.1正常使用, 6.0/ 7.0.5 未知

# 查看cuda和cudnn版本
cuda一般安装在 /usr/local/cuda/ 路径下，该路径下有一个version.txt文档，里面记录了cuda的版本信息
cat  /usr/local/cuda/version.txt 即可查询
同理，cudnn的信息在其头文件里
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2  即可查询