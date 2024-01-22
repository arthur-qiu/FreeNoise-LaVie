# FreeNoise-LaVie

This repository is the official implementation of [FreeNoise](https://arxiv.org/abs/2310.15169) in [LaVie](https://arxiv.org/abs/2309.15103).

**[FreeNoise: Tuning-Free Longer Video Diffusion via Noise Rescheduling](https://arxiv.org/abs/2310.15169)**
</br>
Haonan Qiu,
Menghan Xia*,
Yong Zhang,
Yingqing He,
Xintao Wang,
Ying Shan,
Ziwei Liu*
<p style="font-size: 0.8em; margin-top: -2em">*Corresponding Author</p>

**[LaVie: High-Quality Video Generation with Cascaded Latent Diffusion Models](https://arxiv.org/abs/2309.15103)**
</br>
Yaohui Wang†, 
Xinyuan Chen†, 
Xin Ma†, 
Shangchen Zhou, 
Ziqi Huang, 
Yi Wang, 
Ceyuan Yang, 
Yinan He, 
Jiashuo Yu, 
Peiqing Yang, 
Yuwei Guo, 
Tianxing Wu, 
Chenyang Si, 
Yuming Jiang, 
Cunjian Chen, 
Chen Change Loy, 
Bo Dai, 
Dahua Lin*, 
Yu Qiao*, 
Ziwei Liu*
<p style="font-size: 0.8em; margin-top: -2em">†Equal Contribution</p>
<p style="font-size: 0.8em; margin-top: -2em">*Corresponding Author</p>
</br>

<div align="center">
<img src=assets/A_polar_bear_playing_drum_kit_in_NYC_Times_Square,_4k,_high_resolution.gif>
<p>A polar bear playing drum kit in NYC Times Square, 4k, high resolution</p>

<img src=assets/A_knight_riding_a_horse_on_race_course.gif>
<p>A knight riding a horse on race course</p>

<img src=assets/A_jeep_car_is_running_on_the_snow,_night.gif>
<p>A jeep car is running on the snow, night</p>
</div>

## Installation
```
conda env create -f environment.yml 
conda activate lavie
```

## Download Pre-Trained models
Download pre-trained [LaVie models](https://huggingface.co/YaohuiW/LaVie/tree/main), [Stable Diffusion 1.4](https://huggingface.co/CompVis/stable-diffusion-v1-4/tree/main), [stable-diffusion-x4-upscaler](https://huggingface.co/stabilityai/stable-diffusion-x4-upscaler/tree/main) to `./pretrained_models`. You should be able to see the following:
```
├── pretrained_models
│   ├── lavie_base.pt
│   ├── lavie_interpolation.pt
│   ├── lavie_vsr.pt
│   ├── stable-diffusion-v1-4
│   │   ├── ...
└── └── stable-diffusion-x4-upscaler
        ├── ...
```


## Inference Base T2V with FreeNoise
Run following command to generate videos from base T2V model. 
```
cd base
bash pipelines/sample_freenoise.sh
```
In **configs/sample.yaml**, arguments for inference:

- **ckpt_path:** Path to the downloaded LaVie base model, default is `../pretrained_models/lavie_base.pt`

- **pretrained_models:** Path to the downloaded SD1.4, default is `../pretrained_models`

- **output_folder:** Path to save generated results, default is `../res/base`

- **seed:** Seed to be used, `None` for random generation

- **sample_method:** Scheduler to use, `ddim` is necessary for FreeNoise

- **guidance_scale:** CFG scale to use, default is `7.5`

- **num_sampling_steps:** Denoising steps, default is `50`

- **text_prompt:** Prompt for generation


## BibTex
```bibtex
@misc{qiu2023freenoise,
      title={FreeNoise: Tuning-Free Longer Video Diffusion Via Noise Rescheduling}, 
      author={Haonan Qiu and Menghan Xia and Yong Zhang and Yingqing He and Xintao Wang and Ying Shan and Ziwei Liu},
      year={2023},
      eprint={2310.15169},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```

```bibtex
@article{wang2023lavie,
      title={LAVIE: High-Quality Video Generation with Cascaded Latent Diffusion Models},
      author={Wang, Yaohui and Chen, Xinyuan and Ma, Xin and Zhou, Shangchen and Huang, Ziqi and Wang, Yi and Yang, Ceyuan and He, Yinan and Yu, Jiashuo and Yang, Peiqing and others},
      journal={arXiv preprint arXiv:2309.15103},
      year={2023}
}
```


## Disclaimer
We disclaim responsibility for user-generated content. The model was not trained to realistically represent people or events, so using it to generate such content is beyond the model's capabilities. It is prohibited for pornographic, violent and bloody content generation, and to generate content that is demeaning or harmful to people or their environment, culture, religion, etc. Users are solely liable for their actions. The project contributors are not legally affiliated with, nor accountable for users' behaviors. Use the generative model responsibly, adhering to ethical and legal standards.


## Support For Other Models
FreeNoise is supposed to work on other similar frameworks. An easy way to test compatibility is by shuffling the noise to see whether a new similar video can be generated (set eta to 0). If your have any questions about applying FreeNoise to other frameworks, feel free to contact [Haonan Qiu](http://haonanqiu.com/).

Current official implementation: [FreeNoise-VideoCrafter](https://github.com/AILab-CVC/FreeNoise), [FreeNoise-AnimateDiff](https://github.com/arthur-qiu/FreeNoise-AnimateDiff), [FreeNoise-LaVie](https://github.com/arthur-qiu/FreeNoise-LaVie) 


## Acknowledgements
Codebase built upon [LaVie](https://github.com/Vchitect/LaVie).


## License
The code is licensed under Apache-2.0, model weights are fully open for academic research and also allow **free** commercial usage. To apply for a commercial license, please contact vchitect@pjlab.org.cn.
