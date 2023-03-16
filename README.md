### 项目主要是记录llama.cpp学习的过程
#### 下载llama模型
运行 llama.sh 脚本进行下载，脚本参考 https://github.com/shawwn/llama-dl
- 主要参数修改  
PRESIGNED_URL：模型下载的地址，最好在官网申请，可选网络泄露版 https://ipfs.io/ipfs/Qmb9y5GCkTG7ZzbBWMu2BXwMkzyCKcUjtEKPpgdZ7GEFKm，测试过7B、13B,7B的md5不对，换成 https://agi.gpt4.org/llama/LLaMA 下载  
MODEL_SIZE：需下载的模型，逗号（，）分割  
TARGET_FOLDER：模型存放目录

- 博客参考  
  https://zhuanlan.zhihu.com/p/612623853  
  https://til.simonwillison.net/llms/llama-7b-m2

#### 编译llama.cpp
- 下载项目  
git clone https://github.com/ggerganov/llama.cpp.git

- 编译  
  #10表示线程  
  make -j10
- 可能遇到问题  
  - fatal error: stdatomic.h:没有那个文件或目录  
    升级gcc https://blog.csdn.net/zhizhengguan/article/details/107961426
  - error: 'CLOCK_MONOTONIC' undeclared （https://github.com/ggerganov/llama.cpp/issues/54）  
    尝试在 Makefile文件添加 -D_POSIX_C_SOURCE=199309L
    ```bash
        CFLAGS   = -I.              -O3 -DNDEBUG -std=c11   -fPIC -D_POSIX_C_SOURCE=199309L
        CXXFLAGS = -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC -D_POSIX_C_SOURCE=199309L
    ```
#### 运行
- 模型转换  
  替换 quantize.sh 脚本中 models 为刚才下载模型的目录
- 博客参考  
  https://til.simonwillison.net/llms/llama-7b-m2