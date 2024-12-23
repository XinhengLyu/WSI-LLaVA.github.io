---
layout: project_page
permalink: /
title: WSI-LLaVA：A Multimodal Large Language Model for Whole Slide Image
authors:
   Yuci Liang*¹, Xinheng Lyu*², Meidan Ding¹, Wenting Chen³, Jipeng Zhang⁸, Yuexiang Ren⁵'⁶,<br> Song Wu¹'⁷, Sen Yang⁴, Xiyue Wang⁴, Xiaohan Xing⁴, Linlin Shen¹
affiliations:
    ¹Shenzhen University
    ²University of Nottingham Ningbo China
    ³City University of Hong Kong
    <br>
    ⁴Stanford University
    ⁵Nanchang University
    ⁶The First Affiliated Hospital of Nanchang University
    <br>
    ⁷South China Hospital affiliated to Shenzhen University
    ⁸Hong Kong University of Science and Technology
    <br>
    *Equal Contributors<br>
contact: "Xinheng.LYU@nottingham.edu.cn"
paper: https://arxiv.org/abs/2412.02141
Zhihu: https://zhuanlan.zhihu.com/p/12790617274
code: https://github.com/WSI-LLaVA
data: https://huggingface.co/
# title: >
#   <img src="../static/image/wsi-logo.png" alt="WSI Logo" style="height: 45px; vertical-align: middle; margin-right: 10px;">
#   WSI-LLaVA: A Multimodal Large Language Model for Whole Slide Image

# authors:
#     A. M. Turing
# affiliations:
#     King's College, Cambridge
# paper: https://www.cs.virginia.edu/~robins/Turing_Paper_1936.pdf
# zhihu: https://www.youtube.com/results?search_query=turing+machine
# code: https://github.com/topics/turing-machines
# data: https://huggingface.co/docs/datasets
---

<style>
    .center-box {
        display: flex;
        flex-direction: column;
        align-items: center; /* 水平居中 */
        justify-content: center; /* 垂直居中 */
        text-align: center;
        border: 2px solid #ccc; /* 边框 */
        padding: 20px; /* 内边距 */
        margin: 20px auto; /* 外边距，使其水平居中 */
        width: fit-content; /* 根据内容自适应宽度 */
        background-color: #ffffff; /* 背景颜色设置为白色 */
        border-radius: 8px; /* 圆角 */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 阴影 */
    }
    .center-box img {
        max-width: 100%; /* 图片最大宽度 */
        height: auto; /* 保持图片比例 */
    }
    .key-point {
    color: #007BFF; /* 设置圆点的颜色，蓝色为例 */
    font-size: 1.2rem; /* 圆点的大小 */
    margin-right: 10px; /* 圆点与文本的间距 */
    vertical-align: middle; /* 对齐文本中心 */
    }
    .description {
        margin-top: 15px; /* 减少段落顶部的间隔 */
        margin-bottom: 0px; /* 减少段落底部的间隔 */
        font-size: 20px; /* 调整为更大的字体大小 */
        line-height: 1.8; /* 增大行间距，增强可读性 */
        color: #333; /* 深灰色字体 */
        text-align: justify; /* 文字两端对齐 */
        font-family: "Times New Roman", Times, serif; /* 罗马字体 */
    }

    .section-title {
        font-size: 1.8rem; /* 字体大小 */
        font-weight: bold; /* 加粗字体 */
        margin-top:50px; /* 上方间距 */
        margin-bottom: 30px; /* 下方间距 */
        text-align: center; /* 居中对齐 */
        color: black; /* 字体颜色 */
        font-family: "Times New Roman"; /* 黑体字体 */
    }



    .bold-text {
        font-weight: bold; /* 加粗样式 */
    }
   
     .image-container {
            display: flex;
            justify-content: space-around; /* 调整间距，可以改为 center、flex-start 等 */
            align-items: center;
        }
        .image-container img {
            width:150px; /* 统一宽度 */
            height: 200px; /* 统一高度 */
            object-fit: contain; /* 保持图片比例且填充整个框 */
            margin: 0 10px; /* 设置图片之间的间距 */
        }
</style>

<h2 class="section-title" style="margin-top: -40px;">Examples of 11 Pathology VQA Tasks</h2>

<div style="text-align: center; position: relative; margin: 0 auto;">

  <!-- 固定大小框 -->
  <div class="center-box" style="height: 500px; overflow: hidden; padding: 0; border: 1px solid #ddd; position: relative;">
    <!-- 图片显示区域 -->
    <img id="gallery-image" src="./static/image/table1.png" alt="vision-ex" style="width: 100%; height: 100%; object-fit: contain;">

    <!-- 左右切换按钮 -->
    <div id="left-area" style="position: absolute; left: 0; top: 0; width: 10%; height: 100%; cursor: pointer; display: flex; align-items: center; justify-content: center;" onclick="prevImage()">
      <i class="fas fa-chevron-left" style="font-size: 24px; color: gray;"></i>
    </div>
    <div id="right-area" style="position: absolute; right: 0; top: 0; width: 10%; height: 100%; cursor: pointer; display: flex; align-items: center; justify-content: center;" onclick="nextImage()">
      <i class="fas fa-chevron-right" style="font-size: 24px; color: gray;"></i>
    </div>
  </div>
</div>

<script src="https://kit.fontawesome.com/a076d05399.js"></script>

<script>
  // 图片列表
  const images = [
    "./static/image/table1.png",
    "./static/image/table2.png",
    "./static/image/table3.png",
    "./static/image/table4.png",
    "./static/image/table5.png",
    "./static/image/table6.png",
    "./static/image/table7.png",
    "./static/image/table8.png",
    "./static/image/table9.png",
    "./static/image/table10.png",
    "./static/image/table11.png"
  ];

  let currentIndex = 0;

  // 显示指定图片
  function showImage(index) {
    const imgElement = document.getElementById('gallery-image');
    imgElement.src = images[index];
    updateButtons();
  }

  // 切换到下一张图片
  function nextImage() {
    if (currentIndex < images.length - 1) {
      currentIndex++;
      showImage(currentIndex);
    }
  }

  // 切换到上一张图片
  function prevImage() {
    if (currentIndex > 0) {
      currentIndex--;
      showImage(currentIndex);
    }
  }

  // 更新按钮的显示状态
  function updateButtons() {
    document.getElementById('left-area').style.display = currentIndex === 0 ? 'none' : 'flex';
    document.getElementById('right-area').style.display = currentIndex === images.length - 1 ? 'none' : 'flex';
  }

  // 初始化
  showImage(currentIndex);
</script>

<!-- 
<img src="./static/image/radar6.png" alt="Radar Chart">
<p class="description">
    <span class="key-point">•</span> 
        In the radar chart displaying WSI-Precision metrics, WSI-LLaVA (our model) dominates with broader coverage and higher peaks in most diagnostic categories, particularly excelling in “Specific Feature Description,” “Staging," and “Prognosis." This suggests an excellent ability to accurately identify and describe critical pathological features and outcomes. Meanwhile, models like GPT-4o show considerably lower precision, particularly in detailed descriptions, which may limit their utility in nuanced diagnostic scenarios.
</p>
<p class="description">
    <span class="key-point">•</span> 
        WSI-Relevance rada rreveals that  also leads in relevance, with outstanding performance in “Staging” and “Treatment Recommendations,”underscoring its capability to deliver clinically pertinent information that aids in treatment planning and prognosis estimation. In contrast, while GPT-4o and WSI-VQA provide valuable insights in specific areas such as “Prognosis” and “Regional Structure Description,” they exhibit a balanced but generally lower relevance compared to our model, indicating a need for targeted improvements to enhance their practical application in clinical settings.
</p> -->

<h2 class="section-title" style="margin-top: 50px;">Key Contributions</h2>

 <p class="description">
                <span class="key-point">•</span> We introduce WSI-Bench, the first large-scale morphology-aware benchmark for gigapixel WSI understanding and evaluation, encompassing <span style="color:#005FCC;">180k VQA pairs</span> from <span style="color: #005FCC;">9,850 WSIs</span> across <span style="color: #005FCC;">30 cancer types</span>. This benchmark uniquely emphasizes morphological observations in evaluating WSI-level MLLMs.
  </p>
  <p class="description">
                <span class="key-point">•</span> We propose WSI-LLaVA, a novel framework for gigapixel WSI analysis that bridges the cross-modal gap between WSIs and textual descriptions. The framework introduces a three-stage training approach: WSI-text alignment, feature space alignment, and task-specific instruction tuning.
    </p>
   <p class="description">
                <span class="key-point">•</span> We develop WSI-specific evaluation metrics (WSI-Precision and WSI-Relevance) that provide a more accurate assessment of model performance in pathological contexts, addressing the limitations of traditional NLU metrics by verifying claim accuracy and response relevance.
  </p>
  <p class="description">
                <span class="key-point">•</span> Through comprehensive experiments, we demonstrate WSI-LLaVA’s superior performance compared to existing models, establishing a clear correlation between morphological capabilities and diagnostic accuracy.
  </p>
  


<h2 class="section-title" style="margin-top: 50px;">WSI-Bench</h2>
  <img src="./static/image/wsi-beach.png" alt="wsi-beach">
<p class="description" >
        In clinical practice, pathologists rely heavily on morphological features, particularly tissue and cellular structural abnormalities, for diagnosis. Current WSI models overlook these critical details, impacting diagnostic accuracy.So,We introduce WSI-Bench, a morphology-aware benchmark for gigapixel WSI evaluation across 3 pathological capabilities and 11 tasks, which encompasses about 180k VQA pairs from 9,850 WSI across 30 cancer types, sourced from 8,368 patients.
</p>




<h2 class="section-title" style="margin-top: 50px;"> WSI-Bench Construction</h2>
  <img src="./static/image/build_dataset_new.png" alt="build_dataset">
  <p class="description">
  Step 1: Remove gross descriptions and IHC results from pathology reports, retaining morphological descriptions and diagnostic conclusions, then generate enriched descriptions through reverse engineering. 
  </p>
   <p class="description"  style="margin-top: -10px;">
  Step 2: Construct VQA pairs from the refined reports to support comprehensive pathological tasks, enabling diverse analytical capabilities.
  </p>
   



<h2 class="section-title" style="margin-top: 50px;">Architecture</h2>
  <img src="./static/image/architecture_new4.png" alt="WSI-LLaVA">
<p class="description" >
        <p class="description">
    Model Architecture:The framework comprises three key components: the WSI Encoder, a projection layer,  a large language model.
    </p>
    <p class="description" style="margin-top: -10px;">
    Training Strategy: WSI-LLaVA adopts an innovative three-stage training approach for gigapixel WSI analysis, which includes:WSI-Text Alignmen,Feature Space Alignment,Task-Specific Instruction Tuning.
  </p>

   


<h2 class="section-title" style="margin-top: 50px;">WSI-Metrics</h2>


  <img src="./static/image/metric.png" alt="metric">
    <p class="description">
    While Natural Language Understanding (NLU) metrics are commonly used to evaluate medical language tasks, they fall short in accurately assessing performance due to pathology’s complex and often similar terminology. To address this limitation, we introduce two specialized WSI metrics: WSI-Precision, which verifies the accuracy of each claim derived from the ground truth against the model’s answers.
                WSI-Relevance, which assesses the alignment of each claim in the model’s responses with the ground truth to ensure their relevance.
      
  </p>


<h2 class="section-title" style="margin-top: 50px;">Experiments</h2>

  
 <p class="description" >
     We collect various WSI-level MLLMs to evaluate on our WSI-Bench dataset. These include pecialized models for WSI report generation, such as MI-Gen and Hist-Gen, as well as models designed for pathological VQA tasks, like Quilt-LLaVA and WSI-VQA. Additionally, we assess GPT-4o’s performance to evaluate a general-purpose MLLM. For models with input size constraints (e.g., QuiltLLaVA and GPT-4o), we resize the WSIs to 1024 × 1024 pixels to fit within their input processing capabilities. To ensure a fair comparison, all WSI MLLMs are trained on WSI-Bench’s training set and evaluated on its test set.(WSI-P: WSI-Precision, WSI-R: WSI-Relevance, Acc: accuracy, open: open-ended question, and close: close-ended question.) 
</p>

<div>
  <img src="./static/image/result1.png" alt="results">
  
  <img src="./static/image/result2.png" alt="results"  style="margin-bottom: 8px;">
  
  <img src="./static/image/result3.png" alt="results">
   </div>   



<h2 class="section-title">Citation</h2>
<pre style="background-color: #f8f8f8; padding: 15px; border-radius: 5px; font-family: monospace; font-size: 14px; overflow-x: auto;">
@article{liang2024wsi,
  title={WSI-LLaVA: A Multimodal Large Language Model for Whole Slide Image},
  author={Liang, Yuci and Lyu, Xinheng and Ding, Meidan and Chen, Wenting and Zhang, Jipeng and Ren, Yuexiang and He, Xiangjian and Wu, Song and Yang, Sen and Wang, Xiyue and others},
  journal={arXiv preprint arXiv:2412.02141},
  year={2024}
}
</pre>

       


<div class="image-container">
        <img src="./static/image/shenzhen.png" alt="Shenzhen" />
        <img src="./static/image/nuodinghan.png" alt="Nuodinghan" />
        <img src="./static/image/city.png" alt="City" />
        <img src="./static/image/stand.png" alt="Stand" />

    </div>

   <div class="image-container" style="margin-top: -70px;" >
      
      <img src="./static/image/nanchang.png" alt="Keji" />
      <img src="./static/image/fushuyiy.png" alt="Keji" />
      <img src="./static/image/huananyiy.png" alt="Keji" />  
      <img src="./static/image/keji.png" alt="Keji" />
  </div>

